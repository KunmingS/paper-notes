# Sparse Autoencoders for Vision Model Interpretability: A Summary of Recent Findings

## Overview

Sparse Autoencoders (SAEs), originally developed as a tool for mechanistic interpretability of large language models, have recently been extended to vision models and vision-language models. This document summarizes the key findings from recent research (2024–2026) applying SAEs to models such as CLIP, DINOv2, and Vision-Language-Action (VLA) architectures.

---

## Key Findings

### 1. Training Objectives Shape Internal Representations

Stevens et al. (2025) trained SAEs on both CLIP and DINOv2 and conducted a comparative analysis of the features each model learns. The central finding is that **language supervision fundamentally changes what a vision model learns to represent**.

CLIP develops robust, abstract cultural and geographic features. For example, a single SAE feature (CLIP-24K/6909) consistently activates on Brazilian imagery — Rio de Janeiro's skyline, the national flag, Copacabana's iconic sidewalk tiles — while remaining inactive for visually similar but culturally distinct images such as Machu Picchu or the Argentinian flag. DINOv2, trained with purely visual self-supervision, has no equivalent: its closest matching feature turns out to activate most strongly on images of lamps, revealing that it has not learned "Brazil" as a coherent concept.

CLIP also learns **style-agnostic representations**, recognizing the same concept across photographs, paintings, and illustrations. This suggests that bridging vision and language during training enables the model to develop human-like abstractions that purely visual training does not produce.

### 2. SAE Features Have Causal, Not Merely Correlational, Validity

A persistent concern with interpretability methods is whether discovered features actually drive model behavior. Stevens et al. (2025) addressed this through controlled intervention experiments:

- **Species classification**: When SAE features corresponding to specific bird markings were modified, the model's species classification changed predictably, confirming a causal link between the feature and the output.
- **Semantic segmentation**: Suppressing a "sand" feature in DINOv2 caused the segmentation head to reclassify those patches as "earth/ground" or "water" — both reasonable alternatives — while leaving other patches unaffected. This demonstrates that SAE feature vectors are approximately orthogonal and causally meaningful.

These results provide evidence that vision transformers learn decomposable, interpretable representations even without explicit supervision toward interpretability.

### 3. SAEs Significantly Improve Monosemanticity in Vision-Language Models

Pach et al. (2025), published at NeurIPS 2025, introduced a comprehensive framework for evaluating monosemanticity in visual representations. Their key findings include:

- SAEs trained on CLIP's vision encoder substantially increase the monosemanticity of individual neurons, with **sparsity** and **wide latent dimensions** being the most influential factors.
- SAE interventions applied to CLIP's vision encoder can **directly steer multimodal LLM outputs** (e.g., LLaVA) without modifying the language model. This opens a practical pathway for controlling multimodal system behavior through interpretable visual features.

### 4. Universal Concepts Exist Across Vision Models

The Universal Sparse Autoencoder (USAE) framework, presented at ICML 2025, trains a single overcomplete SAE that can reconstruct and interpret internal activations from multiple vision models simultaneously. The results reveal:

- **Shared universal concepts** span different architectures, training objectives, and datasets.
- These concepts range from low-level features (colors, textures) to higher-level structures (object parts, whole objects).
- Some features are unique to specific models, reflecting the influence of their training regime.

Complementary work on DINOv2 shows that SAE features exhibit hierarchical organization aligned with semantic ontologies (e.g., WordNet): deeper layers capture superordinate concepts (e.g., "whale" activating for both orcas and grey whales), while earlier layers capture finer-grained distinctions.

### 5. Caution: Correlation vs. Causation in Feature Interpretation

A critical line of work warns against naive interpretation of SAE features. Research on causal interpretation of SAE features in vision transformers reveals that:

- Many SAE features **cannot be understood solely by observing where they activate**; one must also consider *why* they activate.
- Input attribution methods applied to individual features yield causal explanations that often diverge from correlational activation maps, revealing context dependencies and complex encoded concepts.
- This prevents mislabeling features or overlooking the true factors driving model representations.

### 6. SAE Applications in Robotics (VLA Models)

Lan et al. (2025) applied SAEs to Vision-Language-Action models used in robotic manipulation. Their findings are more sobering:

- The **majority** of extracted SAE features correspond to memorized sequences from specific training demonstrations, rather than generalizable concepts.
- However, a subset of features do correspond to interpretable **motion primitives** (e.g., pre-grasp alignment) and **semantic properties**, and these features can be causally steered to modify closed-loop robot behavior.

### 7. Identifying "Conceptual Blindspots" in Generative Models

Recent work trains large-scale SAEs (32,000 features) on DINOv2 to systematically compare concept prevalence between real images and images generated by diffusion models. This approach enables quantitative identification of concepts that generative models fail to produce accurately — moving beyond anecdotal observation of failure modes toward structured diagnostics.

---

## Open Challenges

1. **Faithfulness**: Do SAE features reliably reflect the model's actual computational mechanisms, or can they be misleading? Ma et al. (2026) showed that some purported "reasoning features" in LLMs may capture superficial cues rather than genuine reasoning — similar concerns apply in vision.
2. **Scalability**: Training and interpreting millions of SAE features on large-scale vision models remains computationally expensive.
3. **From features to circuits**: Most vision SAE work focuses on identifying individual features. Connecting these into computational circuits (as done in LLM mechanistic interpretability) is largely unexplored for vision models.
4. **Non-localized features**: Some SAE features in vision transformers are spatially non-localized — their highest-activation patches scatter across the image — making standard interpretation methods inadequate.

---

## References

1. **Stevens, S., Chao, W.-L., Berger-Wolf, T., & Su, Y.** (2025). "Interpretable and Testable Vision Features via Sparse Autoencoders." arXiv:2502.06755. — *SAE comparison of CLIP vs. DINOv2; causal validation of vision features.*

2. **Pach, M., Karthik, S., Bouniot, Q., Belongie, S., & Akata, Z.** (2025). "Sparse Autoencoders Learn Monosemantic Features in Vision-Language Models." NeurIPS 2025. arXiv:2504.02821. — *Monosemanticity evaluation framework; SAE steering of multimodal LLMs via vision encoder.*

3. **Universal Sparse Autoencoders: Interpretable Cross-Model Concept Alignment.** ICML 2025. — *Joint SAE across multiple vision models discovering shared universal concepts.*

4. **Lim, H., Choi, J., Choo, J., & Schneider, S.** (2025). "Sparse Autoencoders Reveal Selective Remapping of Visual Concepts During Adaptation." ICLR 2025. — *PatchSAE for CLIP ViT; analysis of how adaptation changes concept associations.*

5. **Causal Interpretation of Sparse Autoencoder Features in Vision.** (2025). arXiv:2509.00749. — *Demonstrates that causal (ERF-based) explanations differ from correlational activation maps for vision SAE features.*

6. **Lan, M. et al.** (2025). "Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models." arXiv:2603.19183. — *SAE applied to robotic VLA models; most features are memorized, but some are interpretable motion primitives.*

7. **Olson et al.** (2025). "Probing the Representational Power of Sparse Autoencoders in Vision Models." ICCV 2025 Workshop. — *Systematic evaluation of SAEs on DINOv2, CLIP, and ResNet; hierarchical feature analysis.*

8. **Towards Multimodal Interpretability: Learning Sparse Autoencoders on CLIP.** LessWrong / MATS Program (2024). — *Early exploration of SAE on CLIP's vision encoder; feature visualization and ultra-low-frequency cluster analysis.*

9. **Ma, G., Liang, Z., Chen, I.Y., & Sojoudi, S.** (2026). "Falsifying Sparse Autoencoder Reasoning Features in Language Models." arXiv:2601.05679. — *Critical examination of SAE feature reliability (LLM-focused but with implications for vision).*
