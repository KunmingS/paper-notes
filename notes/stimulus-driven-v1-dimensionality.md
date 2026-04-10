# Stimulus-Driven Population Activity Patterns in Macaque Primary Visual Cortex

> Cowley, B. R., Smith, M. A., Kohn, A. & Yu, B. M. *PLOS Computational Biology* 12, e1005185 (2016).
> DOI: 10.1371/journal.pcbi.1005185

---

## Core Question

How does the **dimensionality** of V1 population activity relate to stimulus complexity, and to what extent do population responses to different stimuli occupy **similar dimensions** of the firing rate space?

---

## Paper Type

**Research article** — applies PCA-based dimensionality analysis to V1 recordings from macaque monkeys, with comparisons to a V1 receptive field model and a deep CNN.

---

## Motivation

Dimensionality reduction is widely used in neural population analysis, but its outputs had not been systematically validated in a brain area with well-characterized stimulus-response relationships. V1 is ideal for this: inputs can be controlled, single-neuron tuning is well understood, and RF models exist for comparison. The goal is to establish that PCA dimensionality yields **interpretable, sensible results** before applying it to less understood brain areas.

---

## Key Concepts

### Population Firing Rate Space
- N-dimensional space (one axis per neuron).
- Population activity at each time = a point in this space.
- PCA identifies **basis patterns** — orthogonal directions of maximal variance.
- Each basis pattern describes a characteristic way neurons covary.
- **Dimensionality** = number of basis patterns needed to explain a variance threshold (e.g., 90%).

### Pattern Aggregation Method (novel contribution)
- Aggregates basis patterns from responses to different stimuli as columns in a matrix.
- Computes effective rank (number of linearly independent columns) using a rank threshold.
- Quantifies how much responses to different stimuli **share** the same dimensions.
- **Similarity index** s: s > 0 = more overlapping than chance; s < 0 = more orthogonal than chance.

---

## Key Results

### 1. Dimensionality Scales with Stimulus Complexity

**Gratings (parametric)**:
- Dimensionality increases sub-linearly with the number of grating orientations.
- For 2 consecutive orientations (30 apart): dimensionality = 1.62x that of 1 orientation (not 2x), meaning ~half the basis patterns are shared.
- Slope change after 6 orientations (180 offset = opposite drift directions) → population uses similar but not identical patterns for opposite drift directions (consistent with ~16/183 neurons being direction-selective).

**Movies (three classes)**:
- Stimulus complexity measured by PCA dimensionality of pixel intensities: **gratings < natural < noise**.
- Population response dimensionality followed the same ordering.
- This ordering did NOT follow from mean firing rates (which had a different order).

**Variance vs. dimensionality dissociation**:
- Noise movie: highest dimensionality, lowest variance (small ball in state space).
- Gratings/natural: lower dimensionality, higher variance (elongated ellipsoid).
- Key insight: dimensionality and variance capture different properties.

### 2. Population Responses Share a Limited Repertoire of Basis Patterns

- Gratings and natural movie basis patterns significantly overlap (s > 0.39, p < 10^-5).
- Noise movie basis patterns largely **contain** the patterns for gratings and natural (s > 0.32).
- Each stimulus also recruits a small number of unique patterns.
- Summary (Venn diagram, Fig 4D): the circuit expresses a **limited repertoire** of basis patterns; different stimuli recruit different subsets.

Notable exceptions in basis pattern structure:
- Natural movie: top basis pattern has all same-sign coefficients → reflects global luminance changes.
- Gratings/noise: top pattern dominated by two strongly-modulated neurons.

### 3. Time-Resolved Dynamics

- **Within 1-second windows**: noise > gratings ≈ natural in dimensionality.
- Natural movie appears low-dimensional at short timescales due to **temporal correlations** (consecutive frames are self-similar). Shuffling frames restores expected ordering.
- **Growing time windows** (1s → 30s):
  - Gratings: dimensionality plateaus quickly → reuses same patterns.
  - Natural/noise: dimensionality grows continuously → recruits new patterns over time.
- Basis pattern similarity across time windows: highest for gratings, lowest for noise.
- Moment-to-moment stimulus dimensionality fluctuations only weakly correlated with neural dimensionality fluctuations (mean ρ = 0.20).

### 4. V1 Receptive Field Model Comparison

Model: Gabor filter → half-rectification → suppressive filter → normalization → exponential nonlinearity.

- Dimensionality trends across orientations and movies **matched** population data for most components.
- **Discrepancy**: The exponential output nonlinearity drastically reduced dimensionality by exaggerating variance anisotropy. Certain nonlinearities (exponentiation) affect dimensionality more than others (divisive normalization).
- Variance ordering discrepancy: model showed greater variance for gratings than natural (due to temporal frequency matching of Gabor filters); real data did not.

### 5. Parametric Stimulus Manipulations (Model Predictions)

- **Decreasing contrast** → decreased dimensionality (mean luminance dominates).
- **Phase randomization** (natural → pink noise) → decreased dimensionality (removes higher-order structure, leaving only low-frequency correlations).
- **Flattening power spectrum** (pink noise → white noise) → increased dimensionality (uncorrelated pixels drive more activity patterns).

### 6. Deep CNN: Predictions for Ventral Stream

- Layer 1 (V1-like): dimensionality ordering matches V1 data (gratings < natural < noise).
- Deeper layers: gratings and noise dimensionality **decrease**; natural dimensionality **increases**.
- Prediction: as you go up the ventral stream (V1 → V4 → IT), neurons become more sensitive to natural image features and less to artificial stimuli, so natural movie dimensionality should increase relative to artificial stimuli.

---

## Methods Notes

- Recordings: 61 neurons (monkey 1), 81 neurons (monkey 2), macaque V1.
- Stimuli: 12 drifting sinusoidal gratings (30 intervals), 30s gratings movie, 30s natural movie, 30s noise movie.
- Analysis on **trial-averaged** responses (PSTHs) in 20ms bins.
- Dimensionality defined by cumulative variance threshold (primarily 90%) and rank threshold (t = 0.5).
- Only **relative** comparisons of dimensionality are meaningful (absolute values depend on thresholds).

---

## Key Takeaways

1. **Dimensionality tracks stimulus complexity** — V1 population responses faithfully preserve the complexity ordering of visual stimuli.
2. **V1 uses a shared repertoire of basis patterns** across different stimulus classes, with small stimulus-specific additions. This suggests the circuit has a constrained set of activity patterns shaped by network structure.
3. **Temporal structure matters** — natural scenes appear low-dimensional at short timescales due to temporal correlations, but recruit diverse patterns over longer durations.
4. **Nonlinearities selectively affect dimensionality** — exponential nonlinearities compress dimensionality; normalization does not. This has implications for interpreting dimensionality across brain areas with different nonlinear transformations.
5. **Deep CNN predicts ventral stream trends** — dimensionality of responses to natural vs. artificial stimuli should invert along the visual hierarchy.
6. **PCA yields interpretable results in V1** — validates its use for population analysis in less-understood brain areas.

---

## Relation to Other Papers

- Provides the empirical V1 ground-truth for the dimensionality/manifold concepts discussed in **Langdon et al. (2023)** — here the "manifold" is studied from the perspective of its dimensionality and basis pattern structure.
- The pattern aggregation method quantifies the "limited repertoire" idea, which connects to the claim in Langdon et al. that low-dimensional manifolds arise from constrained circuit connectivity.
- Deep CNN analysis anticipates the hierarchical encoding-decoding framework in **Mathis et al. (2024)** — progressive transformation from V1-like representations to object-level representations.
