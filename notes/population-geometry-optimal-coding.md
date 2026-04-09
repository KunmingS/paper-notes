---
title: "Neural Population Geometry and Optimal Coding of Tasks with Shared Latent Structure"
authors: "Wakhloo, A. J., Slatton, W. & Chung, S."
year: 2025
source: drafts/neuroscience/population geometry and optimal coding.md
tags: [population-geometry, neural-manifolds, optimal-coding, generalization, disentangling, learning, theory]
created: 2026-04-08
---

# Population Geometry and Optimal Coding with Shared Latent Structure

## TL;DR
Derives an analytical decomposition of linear-readout generalization error into four geometric terms — neural-latent correlation, signal-signal factorization, signal-noise factorization, and neural dimension — and shows that optimal representation geometry changes with learning stage.

## Key claims
- Generalization error is a strictly decreasing function of the four geometric statistics.
- Disentangled (factorized) representations minimize irreducible error; noise should be orthogonal to signal.
- Few-shot optima prefer low-dimensional, high-correlation codes; many-shot optima prefer high-dimensional, flatter eigenspectra.
- Validated on trained MLPs, DeepLabCut CNNs (R² = 0.988), macaque V4/IT (SNF sharply rises in IT), and rat PFC/CA1 over learning.
- A dimension–correlation tradeoff is pervasive; geometric decomposition reveals structure hidden by error curves alone.

## Why it matters
Turns the manifold framework into a normative theory of learning: gives measurable geometric quantities predicting generalization and matches biological learning dynamics.

## Related
- [[neural-manifolds-review]]
- [[unifying-manifolds-and-circuits]]
- [[stimulus-driven-v1-dimensionality]]
- [[latent-knowledge-sensory-cortex]]
- [[deep-learning-interpretability-manifold-review]]
- [[wiki/population-geometry-and-manifolds]]
