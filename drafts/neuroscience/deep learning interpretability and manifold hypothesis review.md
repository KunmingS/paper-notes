# Interpretability of Deep Learning Models and the Low-Dimensional Manifold Hypothesis: A Literature Review

## Introduction

Deep learning models have achieved remarkable performance across vision, language, and scientific domains, yet their internal mechanisms remain poorly understood. This opacity raises concerns about reliability, fairness, and safety, particularly in high-stakes applications. Two converging lines of research address this challenge from complementary angles: (1) **explainability and interpretability (XAI)** methods that aim to understand *what* models learn and *why* they make specific decisions; and (2) research on the **low-dimensional manifold hypothesis** applied to internal model representations, which seeks to understand *how* models organize information and whether exploiting low-dimensional structure can improve learning.

This review covers recent work (2022--2026) from top ML venues (NeurIPS, ICML, ICLR) and arXiv, organized thematically across both topics and their intersection.

---

## 1. Explainability and Interpretability of Deep Learning Models

### 1.1 Taxonomy and Landscape of XAI

The field of explainable AI has matured significantly. Several comprehensive surveys provide taxonomies of methods. Ali et al. (2023) present a broad overview categorizing XAI into *ante-hoc* (inherently interpretable) and *post-hoc* approaches, further subdividing post-hoc methods into model-specific vs. model-agnostic, and local vs. global explanations [1]. Longo et al. (2024) argue for "XAI 2.0," identifying open challenges including the need for interdisciplinary evaluation, human-centered design, and going beyond saliency maps [2]. Nauta et al. (2023) identify 12 conceptual properties for evaluating explanations (compactness, correctness, completeness, etc.) and advocate for quantitative evaluation rather than anecdotal evidence [3].

Rudin et al. (2022) make a principled distinction between *interpretable* models (inherently transparent) and *explainable* models (post-hoc explanations of black boxes), arguing that interpretable models should be preferred when possible for high-stakes decisions [4]. Ras et al. (2022) provide a "field guide" categorizing explainability methods into visualization-based, distillation-based, and intrinsic approaches [5].

### 1.2 Attribution Methods

Attribution methods assign importance scores to input features to explain individual predictions. Classical gradient-based methods include saliency maps, Integrated Gradients (Sundararajan et al., 2017), and GradCAM (Selvaraju et al., 2017). Perturbation-based methods like SHAP (Lundberg & Lee, 2017) and LIME (Ribeiro et al., 2016) remain widely used.

Recent work has focused on evaluating and improving these methods. Bodria et al. (2023) provide a comprehensive benchmark comparing explanation methods for black-box models, finding that no single method dominates across all evaluation criteria [6]. A persistent challenge is *faithfulness*: whether attributions accurately reflect the model's decision process rather than merely correlating with human intuition. Schwalbe & Finzel (2023) systematize the vast taxonomy of XAI methods and identify evaluation as the key bottleneck [7].

For LLMs specifically, Zhao et al. (2024) survey explainability techniques including attention-based explanations, input attributions via gradient methods, and probing approaches, noting that the scale and complexity of LLMs demand new interpretability paradigms beyond traditional saliency [8].

### 1.3 Concept-Based Explanations

Concept-based methods explain model decisions in terms of human-understandable semantic concepts rather than raw input features.

**TCAV (Testing with Concept Activation Vectors)** (Kim et al., 2018) pioneered this direction by learning concept directions in activation space and measuring their influence on predictions [9]. Wang & Lee (2022) extend this to spatial activation concept vectors (SACVs), enabling spatially-resolved concept attribution [10].

**Concept Bottleneck Models (CBMs)** (Koh et al., 2020) represent a more structured approach: the model first predicts interpretable concepts, then uses these concepts to make the final prediction [11]. This enables both interpretable reasoning and human intervention at test time. Yuksekgonul et al. (2022) introduce **Post-hoc CBMs**, which convert any pre-trained black-box model into a concept bottleneck model without retraining, significantly broadening CBMs' applicability [12]. The Decoupling CBM (Zhang et al., 2024) addresses the fundamental tension between concept accuracy and label accuracy by decoupling their optimization [13]. Benou & Riklin-Raviv (2025) introduce spatially-aware CBMs that provide both *where* and *what* explanations [14].

Recent work scales CBMs to leverage vision-language models: AnyCBMs (Dominici et al., 2024) and open-vocabulary CBMs (Tan et al., 2024) use CLIP to automatically discover relevant concepts without manual annotation [15, 16].

### 1.4 Mechanistic Interpretability

Mechanistic interpretability aims to reverse-engineer the computational algorithms implemented by neural networks at the level of individual neurons, attention heads, and circuits.

**Superposition and polysemanticity.** A key insight from Elhage et al. (2022) is the **superposition hypothesis**: neural networks represent more features than they have neurons by encoding features in superposed, overlapping directions in activation space [17]. This explains polysemanticity (individual neurons activating for multiple unrelated concepts) and motivates the use of sparse autoencoders to disentangle features.

**Circuit discovery.** Conmy et al. (2023) propose **Automatic Circuit Discovery (ACDC)**, systematizing the process of identifying minimal subgraphs (circuits) responsible for specific model behaviors via activation patching [18]. Nanda et al. (2023) demonstrate *progress measures* for understanding grokking through mechanistic interpretability, identifying the formation of specific computational circuits [19]. Singh et al. (2024) study induction heads---a key circuit element for in-context learning---revealing what conditions must hold for their emergence [20].

**Causal abstraction.** Geiger et al. (2023) provide a theoretical foundation for mechanistic interpretability through **causal abstraction**, formalizing when a high-level algorithm is a faithful description of a neural network's computation [21].

### 1.5 Sparse Autoencoders for Interpretability

Sparse autoencoders (SAEs) have become one of the most promising tools for scaling mechanistic interpretability. By training an autoencoder with a sparsity constraint on the bottleneck to reconstruct model activations, SAEs decompose neural network representations into sparse, interpretable features.

**Foundational work.** Cunningham et al. (2023) demonstrate that SAEs applied to language model activations find highly interpretable, monosemantic features, providing evidence for the superposition hypothesis [22]. Bricken et al. (2023) from Anthropic train SAEs on a one-layer transformer and identify features corresponding to specific, interpretable concepts ("Towards Monosemanticity") [23].

**Scaling SAEs.** Gao et al. (2024) from OpenAI study how to scale SAEs, proposing k-sparse autoencoders that fix the number of active features per input, addressing the challenge of balancing reconstruction quality and sparsity [24]. He et al. (2024) train a suite of 256 SAEs across all layers of Llama-3.1-8B ("Llama Scope"), extracting millions of features [25].

**SAE-based circuit analysis.** Dunefsky et al. (2024) introduce **transcoders** that map MLP inputs to outputs directly in feature space, enabling clean circuit analysis in terms of interpretable features rather than neurons [26]. Kissane et al. (2024) extend SAE analysis to attention layer outputs, showing interpretable decomposition is possible throughout the transformer [27].

**Limitations and critiques.** Ma et al. (2026) critically examine whether SAE-discovered features truly correspond to reasoning mechanisms, finding that some purported "reasoning features" may instead capture superficial cues [28]. This highlights an important open question about the reliability of SAE-based interpretability.

### 1.6 Representation Engineering

Beyond analyzing individual features, **representation engineering** operates on the geometry of representation space. Zou et al. (2023) introduce representation engineering as a top-down approach to understanding and controlling neural network behavior by identifying directions in activation space corresponding to high-level properties (e.g., honesty, harmfulness) [29]. This enables **activation steering** or **control vectors**: adding a fixed direction to activations at inference time to control model behavior without retraining. This approach has been applied to safety steering of LLMs (Bhattacharjee et al., 2024) [30].

---

## 2. The Low-Dimensional Manifold Hypothesis in Model Layers

### 2.1 Background: The Manifold Hypothesis

The **manifold hypothesis** posits that high-dimensional data (e.g., images, text embeddings) lie on or near low-dimensional manifolds embedded in the ambient space. For deep learning, this extends to internal representations: hidden layer activations, despite being high-dimensional, often have low effective (intrinsic) dimensionality. Understanding and exploiting this structure can improve training, generalization, and efficiency.

### 2.2 Intrinsic Dimensionality of Representations

A body of work measures the effective dimensionality of learned representations. Li et al. (2018) showed that the *intrinsic dimensionality* of the optimization problem for neural networks is much lower than the number of parameters, meaning that good solutions can be found in surprisingly low-dimensional subspaces of parameter space [31]. Aghajanyan et al. (2021) extended this to fine-tuning, showing that pre-trained models have very low intrinsic dimensionality for downstream tasks---a key theoretical motivation for LoRA [32].

Recent work by Jia et al. (2022) reviews dimensionality reduction techniques broadly, noting that deep representations naturally tend toward lower effective dimensionality in later layers [33]. The phenomenon of **dimensional collapse**---where representations occupy a lower-dimensional subspace than expected---has been studied as both a feature and a bug, depending on context.

### 2.3 Neural Collapse and Representation Geometry

**Neural collapse (NC)** (Papyan et al., 2020) describes a striking geometric phenomenon in the terminal phase of training: (1) within-class features converge to their class means, (2) class means form a **simplex equiangular tight frame (ETF)**, (3) classifiers align with class means, and (4) the model converges to nearest-class-mean classification [34].

This has spawned extensive follow-up work:

- **Deep neural collapse.** Zangrando et al. (2024) provide a unified theoretical framework connecting deep NC (propagation of collapse to earlier layers) to **implicit low-rank bias** induced by L2 regularization, establishing quantitative relations between feature clustering and weight matrix rank [35].

- **NC vs. low-rank bias.** Sukenik et al. (2024, NeurIPS) reveal a fundamental tension: while neural collapse predicts symmetric simplex structure, weight decay induces low-rank bias that can make deep NC *suboptimal* [36]. Garrod & Keating (2024) extend this analysis to cross-entropy loss, finding that NC persists even when low-rank bias is present, though in a modified form [37].

- **Dynamics and generalization.** Xu et al. (2023) study training dynamics under square loss, showing convergence to solutions with minimum product of Frobenius norms, connecting normalization, low rank, and neural collapse to generalization bounds [38].

- **Low-rank learning by design.** Baker et al. (2024) show that gradient rank collapse---where gradients in fully-connected layers develop low-rank structure---is an inherent feature of network architecture and activation linearity, not just a late-training phenomenon [39].

- **Applications.** Neural collapse insights have been applied to: federated learning (fixing classifiers to ETF structure to avoid bias; No Fear of Classifier Biases, Li et al., 2023 [40]), long-tailed recognition (Inducing NC, Liu et al., 2023 [41]), out-of-distribution detection (NECO, Ben Ammar et al., 2023 [42]), and understanding prompt tuning in vision-language models (Zhu et al., 2023 [43]).

### 2.4 Low-Rank Adaptation (LoRA) and Efficient Fine-Tuning

**LoRA (Low-Rank Adaptation)** (Hu et al., 2022) operationalizes the low intrinsic dimensionality hypothesis for parameter-efficient fine-tuning: instead of updating all model weights, LoRA freezes the pre-trained weights and adds trainable low-rank decomposition matrices (W = W_0 + BA, where B and A are low-rank) [44]. This reduces trainable parameters by orders of magnitude while achieving competitive performance.

The LoRA family has expanded rapidly:

- **DoRA** (Liu et al., 2024) decomposes weight updates into magnitude and direction components, better mimicking full fine-tuning behavior [45].
- **DyLoRA** (Valipour et al., 2023) enables dynamic rank selection without retraining [46].
- **Sparse LoRA** (Ding et al., 2023) combines low-rank structure with sparsity for further efficiency [47].
- **LoRA surveys** (Mao et al., 2024) document the exponential growth of LoRA variants and applications [48].

The broader PEFT (parameter-efficient fine-tuning) landscape (Ding et al., 2023, Nature Machine Intelligence) contextualizes LoRA within adapter methods, prefix tuning, and prompt tuning, all of which exploit low-dimensional structure in the adaptation space [49].

### 2.5 Loss Landscape Geometry

The loss landscape of neural networks exhibits low-dimensional structure that impacts training and generalization.

**Mode connectivity.** Draxler et al. (2018) and Garipov et al. (2018) showed that different local minima are connected by low-loss paths, suggesting the loss landscape has a simple, low-dimensional structure despite high parameter dimensionality [50, 51]. **Linear mode connectivity**---where solutions found from the same pre-trained initialization can be linearly interpolated without loss increase---has become an important concept for understanding transfer learning and model merging.

Recent work has leveraged this for practical applications: model soups (averaging multiple fine-tuned models) and model merging techniques (e.g., task arithmetic) exploit the low-dimensional structure of the loss landscape around pre-trained initializations.

### 2.6 Manifold Regularization and Disentanglement

Several methods explicitly enforce or exploit low-dimensional manifold structure during training:

- **Manifold Mixup** (Verma et al., 2019) interpolates hidden representations to regularize the model, encouraging smoother decision boundaries on the data manifold [52].
- **Spectral regularization** constrains the singular values of weight matrices, encouraging low-rank solutions.
- **Deep manifold-regularized learning** (Nguyen et al., 2022) combines manifold learning with deep networks for multi-modal data, using manifold structure to improve phenotype prediction [53].
- **Disentangled representations** (Bengio et al., 2013; Higgins et al., 2017) aim to learn representations where independent generative factors map to separate dimensions, inherently producing structured, low-dimensional feature spaces.

---

## 3. The Intersection: Interpretability Through Manifold Structure

A growing body of work connects the two themes, using geometric and low-dimensional properties of representations to explain and improve models.

### 3.1 Low-Dimensional Structure Enables Interpretability

The fact that representations are approximately low-dimensional makes them more amenable to interpretation. Sparse autoencoders (Section 1.5) can be viewed as discovering the low-dimensional manifold of "meaningful features" within the high-dimensional activation space. The success of SAEs suggests that the effective feature space is much lower-dimensional than the ambient activation space, with interpretable features forming a sparse, overcomplete basis.

Similarly, concept activation vectors (TCAV, Section 1.3) work because meaningful concepts correspond to *directions* in a relatively low-dimensional manifold of activations. The linear probing paradigm---training linear classifiers on hidden representations to detect concepts---succeeds precisely because concepts are linearly separable in the learned representation space.

### 3.2 Neural Collapse as a Window into Model Understanding

Neural collapse provides a geometric interpretability lens: the simplex ETF structure of learned features reveals that well-trained classifiers organize features in maximally separated, symmetric configurations. This connects to:

- **Feature quality metrics:** Measuring proximity to NC geometry quantifies representation quality.
- **Understanding training dynamics:** NC explains *why* certain training choices (e.g., weight decay, normalization) improve generalization---they push representations toward the optimal geometric structure.
- **The low-rank connection:** The tension between NC and low-rank bias (Sukenik et al., 2024) reveals fundamental trade-offs in how models balance feature discriminability against implicit dimensionality reduction [36].

### 3.3 LoRA and the Geometry of Task Adaptation

LoRA's success provides evidence that the "task difference" between a pre-trained model and a fine-tuned model lies in a low-rank subspace. This has interpretability implications:

- The rank of LoRA adaptations is informative about task complexity and similarity.
- Analyzing the subspace spanned by LoRA updates can reveal *what* the model needs to learn for a specific task.
- Model merging via linear interpolation in parameter space works because different tasks share a low-dimensional manifold of useful representations.

### 3.4 Representation Engineering on Manifolds

Representation engineering (Section 1.6) implicitly leverages manifold structure: steering vectors and control vectors correspond to directions on the representation manifold. The effectiveness of linear steering suggests that high-level behavioral properties (honesty, safety, style) are encoded as approximately linear directions in a low-dimensional subspace of activations. This provides both interpretability (identifying what directions correspond to what properties) and control (manipulating those directions).

---

## 4. Discussion and Open Challenges

### 4.1 Bridging Interpretability and Theory

A fundamental gap remains between the practical success of interpretability tools (SAEs, probes, concept vectors) and theoretical understanding of *why* they work. The low-dimensional manifold hypothesis provides a partial explanation: if models learn low-dimensional, structured representations, then linear probes and sparse decompositions should succeed. But formal guarantees are lacking.

### 4.2 Faithfulness and Reliability

A critical concern across all interpretability methods is **faithfulness**: do explanations accurately reflect the model's actual computation? Ma et al. (2026) demonstrate that SAE features can be misleading [28], and similar concerns apply to attribution methods. Developing rigorous faithfulness metrics remains an open challenge.

### 4.3 Scaling Interpretability

Most mechanistic interpretability work focuses on small-to-medium models. Scaling to frontier models with hundreds of billions of parameters remains extremely challenging. SAEs offer a promising direction, but the sheer number of features (millions) and the computational cost of training and interpreting them are significant barriers.

### 4.4 Exploiting Low-Dimensional Structure

While LoRA and neural collapse demonstrate that low-dimensional structure exists and can be exploited, more direct methods for leveraging manifold structure during training are under-explored. Future directions include:

- **Manifold-aware architectures** that explicitly parameterize representations on low-dimensional manifolds.
- **Adaptive dimensionality** that allows different layers or tasks to use different effective dimensionalities.
- **Connecting intrinsic dimensionality to generalization** with formal bounds.

### 4.5 Unifying the Two Fields

The intersection between interpretability and manifold learning is ripe for further development. Understanding *why* representations collapse to low-dimensional manifolds, *what* structure these manifolds have, and *how* this structure relates to model capabilities and behaviors could unify our understanding of deep learning.

---

## 5. Search Methodology

- **Databases searched:** Semantic Scholar, OpenAlex, arXiv
- **Search queries:** "mechanistic interpretability transformer circuits," "sparse autoencoder language model features," "explainability attribution deep learning," "concept bottleneck model," "neural collapse low rank representation," "LoRA low rank adaptation," "loss landscape mode connectivity," "manifold hypothesis neural network representations," "representation engineering," "intrinsic dimensionality deep learning," "TCAV concept activation vectors"
- **Date range:** 2022--2026 (with foundational works from earlier years included via citation chains)
- **Number of results screened:** ~300+
- **Selection criteria:** Relevance to deep learning interpretability or low-dimensional manifold hypothesis in model representations; preference for top venues (NeurIPS, ICML, ICLR, Nature MI, JMLR) and high-citation papers

---

## References

[1] Ali, S., Abuhmed, T., El-Sappagh, S., et al. "Explainable Artificial Intelligence (XAI): What we know and what is left to attain Trustworthy Artificial Intelligence." *Information Fusion* 99, 101805 (2023). DOI: 10.1016/j.inffus.2023.101805

[2] Longo, L., Brcic, M., Cabitza, F., et al. "Explainable Artificial Intelligence (XAI) 2.0: A manifesto of open challenges and interdisciplinary research directions." *Information Fusion* 106, 102301 (2024). DOI: 10.1016/j.inffus.2024.102301

[3] Nauta, M., Trienes, J., Pathak, S., et al. "From Anecdotal Evidence to Quantitative Evaluation Methods: A Systematic Review on Evaluating Explainable AI." *ACM Computing Surveys* 55(13s), 1-42 (2023). DOI: 10.1145/3583558

[4] Rudin, C., Chen, C., Chen, Z., et al. "Interpretable machine learning: Fundamental principles and 10 grand challenges." *Statistics Surveys* 16, 1-68 (2022). DOI: 10.1214/21-SS133

[5] Ras, G., Xie, N., van Gerven, M., Doran, D. "Explainable Deep Learning: A Field Guide for the Uninitiated." *Journal of Artificial Intelligence Research* 73, 329-397 (2022). DOI: 10.1613/jair.1.13200

[6] Bodria, F., Giannotti, F., Guidotti, R., et al. "Benchmarking and survey of explanation methods for black box models." *Data Mining and Knowledge Discovery* 37, 1719-1778 (2023). DOI: 10.1007/s10618-023-00933-9

[7] Schwalbe, G. & Finzel, B. "A comprehensive taxonomy for explainable artificial intelligence: a systematic survey of surveys on methods and concepts." *Data Mining and Knowledge Discovery* 37, 530-573 (2023). DOI: 10.1007/s10618-022-00867-8

[8] Zhao, H., Chen, H., Yang, F., et al. "Explainability for Large Language Models: A Survey." *ACM Transactions on Intelligent Systems and Technology* 15(2), 1-38 (2024). DOI: 10.1145/3639372

[9] Kim, B., Wattenberg, M., Gilmer, J., et al. "Interpretability Beyond Feature Attribution: Quantitative Testing with Concept Activation Vectors (TCAV)." *ICML* (2018). arXiv: 1711.11279

[10] Wang, A. & Lee, W.-N. "Exploring Concept Contribution Spatially: Hidden Layer Interpretation with Spatial Activation Concept Vector." arXiv:2205.11511 (2022). DOI: 10.48550/arXiv.2205.11511

[11] Koh, P.W., Nguyen, T., Tang, Y.S., et al. "Concept Bottleneck Models." *ICML* (2020). arXiv: 2007.04612

[12] Yuksekgonul, M., Wang, M., Zou, J. "Post-hoc Concept Bottleneck Models." *ICLR* (2022). DOI: 10.48550/arXiv.2205.15480

[13] Zhang, R., Du, X., Yan, J., Zhang, S. "The Decoupling Concept Bottleneck Model." *IEEE TPAMI* 46, (2024). DOI: 10.1109/TPAMI.2024.3489597

[14] Benou, I. & Riklin-Raviv, T. "Show and Tell: Visually Explainable Deep Neural Nets via Spatially-Aware Concept Bottleneck Models." *CVPR* (2025). DOI: 10.1109/CVPR52734.2025.02798

[15] Dominici, G., Barbiero, P., Giannini, F., et al. "AnyCBMs: How to Turn Any Black Box into a Concept Bottleneck Model." *xAI* (2024). DOI: 10.48550/arXiv.2405.16508

[16] Tan, A., Zhou, F., Chen, H. "Explain via Any Concept: Concept Bottleneck Model with Open Vocabulary Concepts." *ECCV* (2024). DOI: 10.48550/arXiv.2408.02265

[17] Elhage, N., Hume, T., Olsson, C., et al. "Toy Models of Superposition." *Transformer Circuits Thread*, Anthropic (2022). arXiv: 2209.10652

[18] Conmy, A., Mavor-Parker, A.N., Lynch, A., et al. "Towards Automated Circuit Discovery for Mechanistic Interpretability." *NeurIPS* (2023). DOI: 10.48550/arXiv.2304.14997

[19] Nanda, N., Chan, L., Lieberum, T., et al. "Progress measures for grokking via mechanistic interpretability." *ICLR* (2023). DOI: 10.48550/arXiv.2301.05217

[20] Singh, A.K., Moskovitz, T., Hill, F., et al. "What needs to go right for an induction head? A mechanistic study of in-context learning circuits and their formation." arXiv:2404.07129 (2024). DOI: 10.48550/arXiv.2404.07129

[21] Geiger, A., Potts, C., et al. "Causal Abstraction: A Theoretical Foundation for Mechanistic Interpretability." arXiv:2301.04709 (2023). DOI: 10.48550/arXiv.2301.04709

[22] Cunningham, H., Ewart, A., Riggs, L., et al. "Sparse Autoencoders Find Highly Interpretable Features in Language Models." arXiv:2309.08600 (2023). DOI: 10.48550/arXiv.2309.08600

[23] Bricken, T., Templeton, A., Batson, J., et al. "Towards Monosemanticity: Decomposing Language Models With Dictionary Learning." *Transformer Circuits Thread*, Anthropic (2023).

[24] Gao, L., Dupré la Tour, T., Tillman, H., et al. "Scaling and evaluating sparse autoencoders." arXiv:2406.04093 (2024). DOI: 10.48550/arXiv.2406.04093

[25] He, Z., Shu, W., Ge, X., et al. "Llama Scope: Extracting Millions of Features from Llama-3.1-8B with Sparse Autoencoders." arXiv:2410.20526 (2024). DOI: 10.48550/arXiv.2410.20526

[26] Dunefsky, J., Chlenski, P., Nanda, N. "Transcoders Find Interpretable LLM Feature Circuits." arXiv:2406.11944 (2024). DOI: 10.48550/arXiv.2406.11944

[27] Kissane, C., Krzyzanowski, R., Bloom, J.I., et al. "Interpreting Attention Layer Outputs with Sparse Autoencoders." arXiv:2406.17759 (2024). DOI: 10.48550/arXiv.2406.17759

[28] Ma, G., Liang, Z., Chen, I.Y., Sojoudi, S. "Falsifying Sparse Autoencoder Reasoning Features in Language Models." arXiv:2601.05679 (2026). DOI: 10.48550/arXiv.2601.05679

[29] Zou, A., Phan, L., Chen, S., et al. "Representation Engineering: A Top-Down Approach to AI Transparency." arXiv:2310.01405 (2023).

[30] Bhattacharjee, A., Ghosh, S., Rebedea, T., Parisien, C. "Towards Inference-time Category-wise Safety Steering for Large Language Models." arXiv:2410.01174 (2024). DOI: 10.48550/arXiv.2410.01174

[31] Li, C., Farkhoor, H., Liu, R., Yosinski, J. "Measuring the Intrinsic Dimension of Objective Landscapes." *ICLR* (2018). arXiv: 1804.08838

[32] Aghajanyan, A., Gupta, S., Zettlemoyer, L. "Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning." *ACL* (2021). DOI: 10.18653/v1/2021.acl-long.568

[33] Jia, W., Sun, M., Lian, J., Hou, S. "Feature dimensionality reduction: a review." *Complex & Intelligent Systems* 8, 2663-2693 (2022). DOI: 10.1007/s40747-021-00637-x

[34] Papyan, V., Han, X.Y., Donoho, D.L. "Prevalence of neural collapse during the terminal phase of deep learning training." *PNAS* 117(40), 24652-24663 (2020). DOI: 10.1073/pnas.2015509117

[35] Zangrando, E., Deidda, P., Brugiapaglia, S., et al. "Provable Emergence of Deep Neural Collapse and Low-Rank Bias in L2-Regularized Nonlinear Networks." arXiv (2024).

[36] Sukenik, P., Mondelli, M., Lampert, C.H. "Neural Collapse versus Low-rank Bias: Is Deep Neural Collapse Really Optimal?" *NeurIPS* (2024). DOI: 10.48550/arXiv.2405.14468

[37] Garrod, C. & Keating, J.P. "The Persistence of Neural Collapse Despite Low-Rank Bias: An Analytic Perspective Through Unconstrained Features." arXiv:2410.23169 (2024). DOI: 10.48550/arXiv.2410.23169

[38] Xu, M., Rangamani, A., Liao, Q., et al. "Dynamics in Deep Classifiers Trained with the Square Loss: Normalization, Low Rank, Neural Collapse, and Generalization Bounds." *Research* 6, 0024 (2023). DOI: 10.34133/research.0024

[39] Baker, B.T., Pearlmutter, B.A., Miller, R.L., et al. "Low-Rank Learning by Design: the Role of Network Architecture and Activation Linearity in Gradient Rank Collapse." arXiv:2402.06751 (2024). DOI: 10.48550/arXiv.2402.06751

[40] Li, Z., Shang, X., He, R., Lin, T., Wu, C. "No Fear of Classifier Biases: Neural Collapse Inspired Federated Learning with Synthetic and Fixed Classifier." arXiv:2303.10058 (2023). DOI: 10.48550/arXiv.2303.10058

[41] Liu, X., Zhang, J., Hu, T., et al. "Inducing Neural Collapse in Deep Long-tailed Learning." arXiv:2302.12453 (2023). DOI: 10.48550/arXiv.2302.12453

[42] Ben Ammar, M., Belkhir, N., Popescu, S., et al. "NECO: NEural Collapse Based Out-of-distribution Detection." arXiv:2310.06823 (2023). DOI: 10.48550/arXiv.2310.06823

[43] Zhu, D., Li, Z., Zhang, M., et al. "Understanding Prompt Tuning for V-L Models Through the Lens of Neural Collapse." arXiv:2306.15955 (2023). DOI: 10.48550/arXiv.2306.15955

[44] Hu, E.J., Shen, Y., Wallis, P., et al. "LoRA: Low-Rank Adaptation of Large Language Models." *ICLR* (2022). arXiv: 2106.09685

[45] Liu, S.-Y., Wang, C.-Y., Yin, H., et al. "DoRA: Weight-Decomposed Low-Rank Adaptation." arXiv:2402.09353 (2024). DOI: 10.48550/arXiv.2402.09353

[46] Valipour, M., Rezagholizadeh, M., Kobyzev, I., Ghodsi, A. "DyLoRA: Parameter-Efficient Tuning of Pre-trained Models using Dynamic Search-Free Low-Rank Adaptation." *EACL* (2023). DOI: 10.18653/v1/2023.eacl-main.239

[47] Ding, N., Lv, X., Wang, Q., et al. "Sparse Low-rank Adaptation of Pre-trained Language Models." *EMNLP* (2023). DOI: 10.18653/v1/2023.emnlp-main.252

[48] Mao, Y., Ge, Y., Fan, Y., et al. "A survey on LoRA of large language models." *Frontiers of Computer Science* 18, (2024). DOI: 10.1007/s11704-024-40663-9

[49] Ding, N., Qin, Y., Yang, G., et al. "Parameter-efficient fine-tuning of large-scale pre-trained language models." *Nature Machine Intelligence* 5, 220-235 (2023). DOI: 10.1038/s42256-023-00626-4

[50] Draxler, F., Veschgini, K., Salmhofer, M., Hamprecht, F.A. "Essentially No Barriers in Neural Network Energy Landscape." *ICML* (2018). arXiv: 1803.00885

[51] Garipov, T., Izmailov, P., Podoprikhin, D., et al. "Loss Surfaces, Mode Connectivity, and Fast Ensembling of DNNs." *NeurIPS* (2018). arXiv: 1802.10026

[52] Verma, V., Lamb, A., Beckham, C., et al. "Manifold Mixup: Better Representations by Interpolating Hidden States." *ICML* (2019). arXiv: 1806.05236

[53] Nguyen, N.D., Huang, J., Wang, D. "A deep manifold-regularized learning model for improving phenotype prediction from multi-modal data." *Nature Computational Science* 2, 38-46 (2022). DOI: 10.1038/s43588-021-00185-x
