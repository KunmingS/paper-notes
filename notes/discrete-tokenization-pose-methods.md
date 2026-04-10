# Discrete Tokenization Family for Pose Estimation

A growing family of methods represents human poses as **discrete tokens** via VQ-VAE or related quantization schemes, rather than predicting continuous coordinates or heatmaps independently per joint. The shared insight: discrete codebooks constrain predictions to valid pose configurations, enforcing structural consistency and improving robustness under occlusion.

---

## 1. PCT — Human Pose as Compositional Tokens

**Paper:** Human Pose as Compositional Tokens  
**Authors:** Zigang Geng, Chunyu Wang, Yixuan Wei, Ze Liu, Houqiang Li, Han Hu  
**Venue:** CVPR 2023  
**Code:** [Gengzigang/PCT](https://github.com/Gengzigang/PCT)

### Motivation

Conventional pose representations (coordinate vectors, heatmaps) treat joints independently, ignoring inter-joint dependencies. When a keypoint is occluded, heatmap-based methods produce diffuse or multi-modal activation maps, causing the predicted location to shift unpredictably across frames.

### Architecture

PCT uses a **two-stage pipeline**: a VQ-VAE tokenizer learns discrete pose tokens, then a classifier predicts token classes from image features.

**Stage I — Tokenizer (VQ-VAE):**

- **Encoder:** Linear projection maps each joint's (x, y) coordinates into a high-dimensional space, followed by 4 MLP-Mixer blocks that fuse features across all joints simultaneously. A final linear projection across the joint dimension extracts **M = 34** token features, each in R^512. Each token captures a learned sub-structure of interdependent joints — not a single joint.
- **Codebook:** A shared codebook C of **V = 2048** entries, each in R^512. Each token is quantized to its nearest codebook entry via L2 distance. The codebook is updated with exponential moving average (EMA, decay = 0.9) of encoder outputs. A ReservoirSampler maintains representative samples for periodic k-means re-estimation.
- **Decoder:** 1 MLP-Mixer block projects quantized token features back to joint coordinates, reconstructing the full 2D pose.
- **Training losses:** Smooth L1 reconstruction loss + commitment loss (beta-weighted L2 between token features and codebook entries with stop-gradient).
- **Occlusion handling:** Random joint masking during training — masked joints are replaced with a learned `invisible_token`, teaching the encoder to produce valid tokens even when joints are missing.
- **Image guidance (optional):** Backbone features at joint locations are concatenated with positional features (guide_ratio = 0.5) to enhance discrimination. Can be removed for a cleaner model.

**Stage II — Classifier:**

- **Backbone:** Swin Transformer V2 (pretrained with SimMIM, then with heatmap supervision on COCO). Frozen during Stage II.
- **Classification head:** 2 residual conv blocks modulate backbone features → flatten and project into M × N token feature matrix → 4 MLP-Mixer blocks → logits L in R^{M × V}. Each of the 34 token positions is classified into one of 2048 codebook entries.
- **Decoding:** Soft token features S = L × C are fed to the frozen decoder to reconstruct joint coordinates.
- **Training losses:** Cross-entropy on token classes + smooth L1 on reconstructed joints.

### Key Design Choices

| Parameter | Value |
|-----------|-------|
| Tokens per pose (M) | 34 |
| Codebook size (V) | 2048 |
| Token dimension | 512 |
| Encoder blocks | 4 MLP-Mixer |
| Decoder blocks | 1 MLP-Mixer |
| Backbone | Swin V2 (Base / Large / Huge) |

### Why It Avoids Keypoint Shift

1. **Structural constraint:** Each token encodes multiple interdependent joints; the codebook restricts outputs to learned valid configurations.
2. **VQ snapping:** Small perturbations in encoder output are quantized to the same codebook entry, preventing gradual frame-to-frame drift.
3. **Holistic decoding:** The decoder reconstructs all joints jointly from token features, so an occluded joint's position is determined by the full set of tokens.

### Results

| Benchmark | Metric | Score |
|-----------|--------|-------|
| COCO val (Huge) | AP | 78.2 |
| COCO test-dev (Huge) | AP | 77.1 |
| CrowdPose | AP_OC | 38.2 (vs 26.6 HRNet) |
| Human3.6M (3D) | MPJPE | 50.8 mm |

---

## 2. Di2Pose — Discrete Diffusion for Occluded 3D Pose

**Paper:** Di2Pose: Discrete Diffusion Model for Occluded 3D Human Pose Estimation  
**Authors:** Weiquan Wang, Jun Xiao, Chunping Wang, Wei Liu, Zhao Wang, Long Chen  
**Venue:** NeurIPS 2024  
**arXiv:** 2405.17016

### Motivation

Continuous diffusion models for 3D HPE have an unrestricted search space, requiring massive training data and still generating biomechanically unrealistic poses under occlusion. Di2Pose constrains the search space to physically viable configurations via discrete tokenization combined with a discrete diffusion process that explicitly models occlusion.

### Architecture

**Stage 1 — Pose Quantization:**

- **Encoder:** 4 Local-MLP blocks (a novel alternative to MLP-Mixer). Each Local-MLP block uses a **Joint Shift block (JS-Block)** that captures local interactions among X = 3 neighboring joints by shifting features along joint connection directions, followed by Channel MLP. This models local skeletal topology rather than PCT's fully global mixing. Embedding dimension D = 2048.
- **Quantization:** Uses **Finite Scalar Quantization (FSQ)** instead of standard VQ-VAE. Token features are projected to d = 5 dimensions, each bounded via tanh and rounded to integer levels. Levels per channel: [7, 5, 5, 5, 5], yielding an **implied codebook size |C| = 7 × 5 × 5 × 5 × 5 = 4,375**. FSQ eliminates the need for codebook learning and avoids codebook collapse entirely.
- **Number of tokens:** N = 100 per pose.
- **Decoder:** 1 Local-MLP block, embedding dimension 512.
- **Loss:** Cross-entropy reconstruction loss.
- **Reconstruction accuracy:** 13.6 MPJPE (better than PCT's 15.2).

**Stage 2 — Discrete Diffusion Process:**

- **Forward process:** Corrupts clean tokens k_0 into noisy tokens k_S over S = 100 steps using a custom **occlude-and-replace transition matrix**:
  - Probability γ_s: token becomes an `[OCC]` token (simulating occlusion)
  - Probability β_s: token is uniformly replaced by a random valid token (modeling pose ambiguity)
  - Probability α_s: token stays unchanged
- **Reverse process (Pose Denoiser):** 21-layer, 16-head transformer (dim 1024). Uses AdaLN conditioning on diffusion timestep + multi-head cross-attention to image features from a frozen image encoder.
- **Inference:** All tokens start as `[OCC]` or random → iteratively denoised conditioned on the input image.
- **Loss:** Variational lower bound + auxiliary denoising loss (λ = 5e-4).

### Key Design Choices

| Parameter | Value |
|-----------|-------|
| Tokens per pose (N) | 100 |
| Codebook size (implied) | 4,375 (FSQ) |
| FSQ levels | [7, 5, 5, 5, 5] |
| Encoder blocks | 4 Local-MLP |
| Diffusion steps | 100 |
| Denoiser | 21-layer transformer |

### Key Distinction from PCT

- **FSQ replaces VQ-VAE:** No learned codebook, no codebook collapse, no EMA updates.
- **Local-MLP replaces MLP-Mixer:** Captures local skeletal topology via joint shifting rather than fully global mixing.
- **Diffusion-based generation:** Instead of single-pass classification, Di2Pose iteratively refines tokens from noise, which better handles multi-modal uncertainty under occlusion.

### Results

| Benchmark | Metric | Score |
|-----------|--------|-------|
| Human3.6M | MPJPE | 49.2 mm (single-frame SOTA) |
| 3DPW | MPJPE | 79.3 mm |
| 3DPW-Occ | MPJPE | 79.6 mm |
| 3DPW-AdvOcc@80 | MPJPE | 153.6 mm (next-best: 189.3) |

---

## 3. HiPART — Hierarchical Pose AutoRegressive Transformer

**Paper:** HiPART: Hierarchical Pose AutoRegressive Transformer for Occluded 3D Human Pose Estimation  
**Authors:** Hongwei Zheng, Han Li, Wenrui Dai, Ziyang Zheng, Chenglin Li, Junni Zou, Hongkai Xiong  
**Venue:** CVPR 2025  
**arXiv:** 2503.23331

### Motivation

Existing 2D-to-3D lifting methods operate on sparse 2D skeletons (e.g., 16-17 joints), which provide limited information when joints are occluded. HiPART generates hierarchical multi-scale 2D poses — from sparse to dense to fine — using autoregressive token generation, providing richer spatial information for 3D lifting.

### Architecture

**Stage 1 — Multi-Scale Skeletal Tokenization (MSST):**

Inspired by VQ-VAE-2 (hierarchical VQ-VAE), MSST builds a two-level codebook over skeleton representations at different granularities.

- **Joint hierarchy:**
  - J_s = 16 sparse joints (standard skeleton)
  - J_d = 48 dense joints (intermediate)
  - J_f = 96 fine joints (from 3D mesh vertices via coarsening + camera projection)
- **Two encoders:** E_f (fine encoder) and E_d (dense encoder) sequentially project fine pose x_f into dense embeddings z_d ∈ R^{48 × 128} and sparse embeddings z_s ∈ R^{16 × 128}.
- **Sparse codebook:** C_s with K_s = 2048 vectors. z_s is quantized to sparse tokens q_s.
- **Dense codebook:** C_d with K_d = 2048 vectors. After upsampling the quantized sparse representation and concatenating with z_d, the result is quantized to dense tokens q_d.
- **Skeleton-aware Alignment:** Strengthens cross-scale token connections:
  - *Part-wise Local Alignment (LA):* InfoNCE contrastive loss matching sparse and dense tokens within the same body part.
  - *Global Alignment (GA):* InfoNCE loss aligning entire sparse and dense representations.

**Stage 2 — Hierarchical AutoRegressive Modeling (HiARM):**

- **Generation order:** Center-to-Periphery — generation starts from the skeletal center (root/hip) and proceeds outward to extremities (hands, feet). Joints farther from root have higher uncertainty, so generating center first provides better context.
- **Token pairs:** Each generation step produces 1 sparse token + r = 3 dense tokens for one body part.
- **Sparse-to-Dense:** The sparse token is generated first (autoregressive), then r dense tokens are generated **in parallel** conditioned on the sparse token. This reduces autoregressive steps from 1 + r to 2 per pair (49% inference speedup).
- **Transformer:** Pose-aware Generative Transformer with:
  - Local Self-Attention Blocks (LSAB) for intra-pair modeling
  - Global Cross-Scale Attention Blocks (GCSAB) for inter-pair modeling
- Generated hierarchical 2D poses (sparse + dense) are concatenated and fed to a vanilla spatial transformer for 2D-to-3D lifting.

### Key Design Choices

| Parameter | Value |
|-----------|-------|
| Sparse tokens per pose | 16 |
| Dense tokens per pose | 48 |
| Sparse codebook size | 2048 |
| Dense codebook size | 2048 |
| Token dimension | 128 |
| Encoder | MLP-Mixer blocks |

### Key Distinction from PCT

- **Hierarchical VQ-VAE-2** instead of single-level codebook: captures pose at multiple spatial granularities.
- **Autoregressive generation** with anatomically-motivated ordering (center-to-periphery), rather than single-pass classification.
- **Cross-scale alignment** via contrastive learning ensures coherent multi-resolution tokens.

### Results

| Benchmark | Metric | Score |
|-----------|--------|-------|
| Human3.6M (CPN det.) | MPJPE | 42.0 mm (single-frame SOTA) |
| 3DPW | MPJPE | 77.2 mm |
| 3DPW-Occ | MPJPE | 75.4 mm |

---

## 4. TokenHMR — Tokenized Human Mesh Recovery

**Paper:** TokenHMR: Advancing Human Mesh Recovery with a Tokenized Pose Representation  
**Authors:** Sai Kumar Dwivedi, Yu Sun, Priyanka Patel, Yao Feng, Michael J. Black  
**Venue:** CVPR 2024  
**Code:** [tokenhmr.is.tue.mpg.de](https://tokenhmr.is.tue.mpg.de)

### Motivation

In human mesh recovery (HMR), a paradox exists: improving 2D accuracy can worsen 3D accuracy due to biases in pseudo-ground-truth data and incorrect camera projection models. TokenHMR constrains regression to valid pose space via tokenization and introduces a threshold-adaptive loss that avoids overfitting to these biases.

### Architecture

**Pose VQ-VAE Tokenizer:**

- **Input:** SMPL body pose parameters θ = [θ_1, ..., θ_21], each θ_i ∈ R^6 (6D rotation representation for 21 body joints).
- **Encoder:** 1 ResNet block + 4 1D convolutional layers → latent z = E(θ).
- **Codebook:** K = 2048 entries, each in R^256.
- **Tokens per pose:** M = 160 (each quantized to one of 2048 entries).
- **Decoder:** Mirror architecture (1 ResNet block + 4 1D deconvolutions) → reconstructed SMPL pose.
- **Training data:** AMASS + MOYO motion capture datasets.
- **Losses:** L1 reconstruction on pose + L1 on 3D joints (λ_RE = 50) + embedding loss + commitment loss.
- **Reconstruction accuracy:** MVE 8.3 mm, MPJPE 2.2 mm on AMASS test set.

**Threshold-Adaptive Loss Scaling (TALS):**

- Determines effective error thresholds (ε_J2D for 2D keypoints, ε_θ for SMPL pseudo-GT) by evaluating errors when ground-truth bodies are projected with the incorrect HMR camera model.
- When loss > threshold: standard supervision guides training.
- When loss < threshold: loss impact is minimized, preventing overfitting to camera/pose bias.

**HMR Regression as Token Classification:**

- Built on HMR2.0 (ViT backbone).
- Body pose prediction head: 4 blocks of (2 MLPs + GELU). Predicts **token indices** instead of continuous pose parameters.
- Frozen decoder converts predicted tokens → continuous SMPL parameters.
- Separate heads for global orientation, hand pose, body shape, camera.

### Key Design Choices

| Parameter | Value |
|-----------|-------|
| Tokens per pose (M) | 160 |
| Codebook size (K) | 2048 |
| Token dimension | 256 |
| Encoder | ResNet block + 4 × 1D Conv |
| Backbone | ViT (HMR2.0) |

### Key Distinction from PCT

- Operates in **SMPL parameter space** (joint rotations) rather than Cartesian coordinates.
- Recovers full 3D **mesh** (not just skeleton).
- TALS loss specifically addresses the pseudo-GT bias problem in mesh recovery.
- The discrete prior provides a **uniform distribution** over valid poses, unlike Gaussian/GMM priors used in prior HMR methods.

### Results

| Benchmark | Metric | Score |
|-----------|--------|-------|
| EMDB (test) | MPJPE | 88.1 mm (7.6% improvement over HMR2.0) |
| EMDB (test) | PA-MPJPE | 49.8 mm (11.5% improvement) |
| 3DPW | MPJPE | 70.5 mm |

---

## 5. UniPose — Unified Multimodal Pose Framework

**Paper:** UniPose: A Unified Multimodal Framework for Human Pose Comprehension, Generation and Editing  
**Authors:** Yiheng Li, Ruibing Hou, Hong Chang, Shiguang Shan, Xilin Chen  
**Venue:** CVPR 2025  
**arXiv:** 2411.16781

### Motivation

Existing pose methods operate in isolation — separate models for estimation, generation, and understanding. UniPose unifies pose comprehension (describing a pose in text), generation (producing a pose from text/image), and editing (modifying a pose given instructions) in a single LLM-based framework by treating poses as discrete tokens in the language model's vocabulary.

### Architecture

**Pose Tokenizer (VQ-VAE):**

- **Input:** SMPL pose p = [γ, θ] where γ ∈ R^6 (root orientation) and θ ∈ R^{6K} (K joint rotations in 6D representation).
- **Encoder:** Several 1D convolutional layers → latent z = E(θ) ∈ R^{L_p × d_p}.
- **Codebook:** B_p with M = 2048 discrete vectors. Nearest-neighbor quantization.
- **Tokens per pose:** L_p = 80.
- **Decoder:** Several 1D deconvolutional layers → reconstructed SMPL pose.
- **Training data:** AMASS + MOYO (following TokenHMR).
- **Loss:** L_vq = reconstruction + embedding + commitment.

**Visual Processor (Mixture of Encoders):**

- **CLIP-ViT:** Global visual features for semantic understanding.
- **Pose-specific ViT:** Fine-grained pose features, pretrained on pose estimation.
- Features concatenated along channel dimension and projected to LLM embedding dimension.

**Pose-aware Language Model:**

- **LLM backbone:** LLaVA-1.6V.
- **Vocabulary expansion:** Text vocabulary V_t extended with pose vocabulary V_p (2048 codebook indices become new tokens). Unified vocabulary V = {V_t, V_p}.
- **Mixed Attention:** Causal attention for text tokens (standard autoregressive). **Bidirectional attention** within pose token sequences — because pose tokens encode spatial positions, not sequential data. Pose tokens attend to each other freely but only to preceding text tokens.
- **Parallel pose generation:** L_p learnable pose queries enable prediction of all 80 pose tokens in a single forward step (not sequential autoregressive).
- **Fine-tuning:** LoRA on the LLM.

### Key Design Choices

| Parameter | Value |
|-----------|-------|
| Tokens per pose (L_p) | 80 |
| Codebook size (M) | 2048 |
| Encoder/Decoder | 1D Conv / 1D Deconv |
| LLM backbone | LLaVA-1.6V |
| Attention for pose tokens | Bidirectional |

### Key Distinction from PCT

- Poses become **first-class tokens in an LLM vocabulary**, enabling cross-modal reasoning (text ↔ pose ↔ image).
- **Bidirectional attention** for pose tokens recognizes their spatial (non-sequential) nature.
- Supports **pose editing** — modify a pose via natural language instructions.
- Multi-task unified framework rather than a single-task estimator.

### Capabilities

| Task | Description |
|------|-------------|
| Pose Comprehension | Generate text description from pose/image |
| Pose Generation | Produce pose from text or image |
| Pose Editing | Modify pose given natural language instructions |
| Pose-Difference | Describe differences between two poses |

---

## Comparison

| Model | Venue | Task | Quantization | Codebook | Tokens/Pose | Encoder | Generation |
|-------|-------|------|-------------|----------|-------------|---------|------------|
| **PCT** | CVPR 2023 | 2D/3D HPE | VQ-VAE (EMA) | 2048 | 34 | MLP-Mixer | Single-pass classification |
| **Di2Pose** | NeurIPS 2024 | Occluded 3D HPE | FSQ | 4375 (implied) | 100 | Local-MLP | Discrete diffusion |
| **HiPART** | CVPR 2025 | Occluded 3D HPE | VQ-VAE-2 | 2048 + 2048 | 16 + 48 | MLP-Mixer | Autoregressive (center→periphery) |
| **TokenHMR** | CVPR 2024 | Mesh recovery | VQ-VAE | 2048 | 160 | ResNet + 1D Conv | Single-pass classification |
| **UniPose** | CVPR 2025 | Unified comprehension/generation/editing | VQ-VAE | 2048 | 80 | 1D Conv | Parallel (LLM) |

### Shared Principles

1. **Discrete codebooks as structural priors** — All methods restrict predictions to a finite set of learned valid (sub-)configurations, preventing biomechanically impossible outputs.
2. **Holistic encoding** — Encoders process all joints jointly (via MLP-Mixer, Local-MLP, or convolutions), so each token captures inter-joint dependencies rather than isolated keypoints.
3. **Classification replaces regression** — Predicting discrete token indices is more robust than regressing continuous coordinates, especially under occlusion where the mapping is ambiguous.
4. **Frozen decoder at inference** — The decoder (trained in Stage I) provides a fixed, high-quality mapping from tokens back to coordinates/parameters, decoupling representation learning from prediction.

### Evolution of Ideas

```
PCT (2023)
├── Introduced compositional tokens + VQ-VAE for pose
├── Single-level codebook, MLP-Mixer, classification
│
├──► TokenHMR (2024)
│    └── Extended to SMPL mesh space, added TALS loss for bias correction
│
├──► Di2Pose (2024)
│    ├── Replaced VQ-VAE with FSQ (no codebook collapse)
│    ├── Replaced MLP-Mixer with Local-MLP (local skeletal topology)
│    └── Added discrete diffusion with occlusion-aware noise
│
├──► HiPART (2025)
│    ├── Hierarchical VQ-VAE-2 (multi-scale sparse→dense)
│    ├── Cross-scale contrastive alignment
│    └── Autoregressive generation (center-to-periphery)
│
└──► UniPose (2025)
     ├── Pose tokens in LLM vocabulary
     ├── Bidirectional attention for spatial tokens
     └── Unified comprehension + generation + editing
```
