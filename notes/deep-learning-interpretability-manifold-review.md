---
title: "Interpretability of Deep Learning Models and the Low-Dimensional Manifold Hypothesis: A Literature Review"
authors: unknown
year: 2026
source: drafts/neuroscience/deep learning interpretability and manifold hypothesis review.md
tags: [interpretability, manifold-hypothesis, sparse-autoencoders, neural-collapse, lora, mechanistic-interpretability, deep-learning]
created: 2026-04-08
---

# Deep Learning Interpretability and the Manifold Hypothesis

## TL;DR
Thematic review of 2022–2026 XAI and manifold-hypothesis work, connecting attribution, concept bottlenecks, mechanistic interpretability, sparse autoencoders, and representation engineering to neural collapse, LoRA, and loss landscape geometry.

## Key claims
- Interpretability splits into ante-hoc interpretable models vs post-hoc explanations; faithfulness is the central evaluation bottleneck.
- Superposition explains polysemanticity; SAEs recover monosemantic features and scale to frontier models (Llama Scope, transcoders), but some purported features may be misleading (Ma et al. 2026).
- Neural collapse reveals a simplex ETF terminal geometry; weight-decay-induced low-rank bias can make deep NC suboptimal.
- LoRA and PEFT operationalize the low intrinsic dimensionality of task adaptation; model soups exploit loss-landscape mode connectivity.
- Representation engineering and TCAV succeed because high-level properties correspond to approximately linear directions on a low-dimensional activation manifold.

## Why it matters
Frames interpretability and the manifold hypothesis as complementary lenses: low-dimensional geometric structure is *why* linear probes, SAEs, and steering vectors work.

## Related
- [[neural-manifolds-review]]
- [[population-geometry-optimal-coding]]
- [[decoding-the-brain-mechanistic-models]]
- [[wiki/interpretability-and-representation]]
- [[wiki/population-geometry-and-manifolds]]
