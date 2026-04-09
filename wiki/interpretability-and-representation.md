---
type: wiki
tags: [interpretability, manifold-hypothesis, sparse-autoencoders, neural-collapse, lora, deep-learning]
---

# Interpretability and Representation

[[deep-learning-interpretability-manifold-review]] is the single note in this cluster but covers two large literatures and their intersection.

On the interpretability side, the review traces XAI from attribution methods (saliency, Integrated Gradients, SHAP) through concept-based explanations (TCAV, Concept Bottleneck Models, post-hoc CBMs, CLIP-based variants) to mechanistic interpretability: the superposition hypothesis, circuit discovery (ACDC), causal abstraction, and sparse autoencoders scaled to frontier models (Llama Scope, transcoders, attention-layer SAEs). Representation engineering and activation steering treat high-level properties as linear directions in activation space.

On the manifold-hypothesis side, it covers intrinsic dimensionality, neural collapse (simplex ETF geometry and its tension with weight-decay-induced low-rank bias), LoRA and PEFT as operationalizations of low-dimensional task adaptation, and loss-landscape mode connectivity underpinning model soups and merging.

The review's synthesis is that low-dimensional geometric structure is *why* interpretability tools work: SAEs discover a sparse overcomplete basis for a low-dimensional manifold of meaningful features; linear probes and steering vectors succeed because concepts correspond to directions in that manifold; LoRA works because task differences live in a low-rank subspace. Open challenges include faithfulness (Ma et al. 2026 cautions that some SAE "reasoning features" are misleading), scaling to frontier models, and formal bounds connecting intrinsic dimensionality to generalization.

This cluster has natural ties to [[wiki/population-geometry-and-manifolds]] — the neuroscience and ML sides of the same geometric story.
