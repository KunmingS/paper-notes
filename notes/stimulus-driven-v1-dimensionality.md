---
title: "Stimulus-Driven Population Activity Patterns in Macaque Primary Visual Cortex"
authors: "Cowley, B. R., Smith, M. A., Kohn, A. & Yu, B. M."
year: 2016
source: drafts/neuroscience/stimulus driven population activity V1.md
tags: [V1, visual-cortex, dimensionality, population-geometry, PCA, basis-patterns]
created: 2026-04-08
---

# Stimulus-Driven Population Dimensionality in Macaque V1

## TL;DR
PCA of macaque V1 populations shows that response dimensionality tracks stimulus complexity (gratings < natural < noise) and that V1 reuses a limited repertoire of basis patterns across stimulus classes.

## Key claims
- Dimensionality scales sub-linearly with number of grating orientations; ~half of basis patterns are shared between nearby orientations.
- Stimulus complexity ordering (gratings < natural < noise) is preserved in the neural dimensionality ordering.
- Variance and dimensionality are dissociable (noise movies: high dim, low variance).
- A novel pattern-aggregation method quantifies basis-pattern overlap; noise movies largely contain the patterns used for gratings and natural movies.
- V1 RF model reproduces the trends; exponential output nonlinearities collapse dimensionality more than divisive normalization.
- Deep CNN predicts ventral-stream trends: natural movies should gain relative dimensionality along V1→V4→IT.

## Why it matters
Provides a V1 ground truth validating PCA-based manifold analyses, and introduces the "limited repertoire" view of population codes that anchors later manifold and optimal coding work.

## Related
- [[neural-manifolds-review]]
- [[population-geometry-optimal-coding]]
- [[unifying-manifolds-and-circuits]]
- [[inception-loop-bipartite-invariance]]
- [[wiki/visual-cortex-and-coding]]
