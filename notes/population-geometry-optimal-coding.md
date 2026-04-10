# Neural Population Geometry and Optimal Coding of Tasks with Shared Latent Structure

> Wakhloo, A. J., Slatton, W. & Chung, S. *Nature Neuroscience* (2025).
> DOI: 10.1038/s41593-025-02183-y

---

## Core Question

Which **geometric properties** of neural population activity determine how well a linear readout can generalize across multiple tasks that share a common latent structure? What does the **optimal** neural code look like, and how does it change over the course of learning?

---

## Paper Type

**Theory + data analysis** — derives an analytical formula decomposing generalization error into four geometric terms, validated on artificial networks, macaque visual cortex (V4/IT), and rat PFC/CA1 during learning.

---

## Setup

- Stimuli vary along **d latent dimensions** (e.g., object size, position, orientation).
- Each stimulus elicits a neural activity vector **x** (population firing rates).
- Binary tasks are formed by linearly separating the latent space with a hyperplane normal **T** (e.g., "big vs. small shapes").
- Different **T** vectors define different tasks on the same latent structure.
- Readout: supervised Hebbian rule (difference-of-means classifier) — biologically plausible, equivalent to a linear readout with weights set by correlations between neural activity and labels.

---

## The Four Geometric Terms

The average generalization error Eg is a **strictly decreasing function** of four statistics:

### 1. Neural–Latent Correlation (c)
- Normalized sum of squared covariances between neurons and latent variables.
- Measures how sensitive the population is to latent variable variations.
- Higher c → more signal in the neural code → lower error.

### 2. Signal–Signal Factorization (SSF, f)
- Measures alignment between coding directions of distinct latent variables.
- Favors **disentangled** representations: independent latent variables encoded along orthogonal, equal-variance directions (whitened representation).
- SSF contributes to **irreducible error** — doesn't vanish with more training samples.

### 3. Signal–Noise Factorization (SNF, s)
- Measures overlap between noise and coding directions.
- Favors noise orthogonal to signal subspace.
- Also contributes to irreducible error.

### 4. Neural Dimension (PR(Ψ))
- Participation ratio of the neural covariance = effective dimensionality.
- Higher dimension → less correlated trial-to-trial noise → better generalization.

### Learning Stage Dependence
- **Few-shot (early learning)**: Error dominated by correlation (c) and dimension (PR). Need high signal, low noise impact.
- **Many-shot (late learning)**: Error dominated by factorization terms (SSF, SNF). Need clean separation of latent variables from each other and from noise.
- This implies **optimal geometry changes with learning stage**.

---

## Key Results

### Artificial Neural Networks

**Random + trained MLPs**:
- Good quantitative agreement between analytical formula and empirical error.
- **Dimension–correlation tradeoff**: ReLU layers increase dimension but decrease correlation; linear layers do the opposite. These trade off to produce smooth error reduction.
- Trained networks learn to monotonically increase SSF and SNF across layers (random networks don't).
- Despite sharp layer-by-layer geometric changes, overall error changes are smooth — highlighting why **geometric decomposition is essential** (error alone doesn't reveal representational changes).

**Deep CNN for pose estimation (DeepLabCut)**:
- 24-dimensional latent space (12 mouse body markers × 2 coordinates).
- Generalization error decreases across layers.
- Dimension increases, correlation decreases across layers (same tradeoff).
- SSF and SNF improve monotonically.
- Formula captures R² = 0.988 of true error variance despite non-Gaussian data.

### Macaque V4 and IT (Ventral Stream)

- Data: multi-unit recordings from 2 monkeys viewing 64 objects (8 categories, d=6 latent variables: size, position, angle).
- Generalization error improves from pixels → V4 → IT.
- **Dimension** drops in V4 (relative to pixels), then recovers in IT.
- **Correlation** increases from pixels to V4/IT.
- **SNF sharply increases in IT** — latent-unrelated variability becomes increasingly orthogonal to coding directions through the ventral stream.
- Suggests noise orthogonalization is a key transformation in IT.

### Rat PFC and CA1 During Learning

- Rats learning continuous alternation task in W-maze over 8 sessions.
- Latent variables: x/y position and velocity.
- Readout error decreases over learning and correlates with behavioral performance (R² ≈ 0.5).

**Two phases of learning**:
1. **Sessions 1–4 (rapid learning)**: Nearly all geometric measures increase. Total dimension drops, but **task-relevant dimension increases** — irrelevant activity is compressed.
2. **Sessions 4–8 (plateau)**: Trends reverse — dimension increases, correlation decreases. SSF and task-relevant dimension continue to increase.

**Match to optimal coding predictions**: After initial convergence (session 4+), trends align with normative predictions — dimensionality increases, correlation decreases, matching the transition from few-shot to many-shot optimal geometry.

---

## Optimal Coding Theory

Key normative predictions:

1. **Optimal representations are disentangled** — independent latent variables are represented along orthogonal directions.
2. **Compression-to-expansion transition**: Early in learning (few samples), optimal codes compress less informative latent variables (low dimension, high correlation). Late in learning (many samples), optimal codes expand all variables (high dimension, lower correlation, flatter eigenspectrum).
3. The eigenspectrum of the optimal neural covariance transitions from **steep** (few dominant directions) to **flat** (many equal directions) as training data increases.
4. This reflects a rational strategy: only invest coding resources in a latent variable once you have enough data to learn its task relevance.

---

## Methods Notes

- Theory relies on **Gaussian equivalence principle** (GEP): generalization error of linear readouts on complex distributions ≈ that on matched Gaussian models. Validated empirically.
- Formula works in the regime where neurons, latent dimensions, and training samples are all large and of similar scale.
- Results hold for SVC classifiers too (strong correlation with Hebbian errors), suggesting geometric terms are informative beyond the specific readout rule.

---

## Key Takeaways

1. **Four geometric statistics** (correlation, SSF, SNF, dimension) fully determine linear readout generalization across tasks with shared latent structure.
2. **Factorization (disentangling) is optimal** — and contributes to irreducible error that persists regardless of sample size.
3. **Optimal geometry is learning-stage-dependent**: low-dimensional + high-correlation early → high-dimensional + factorized late. This is a normative prediction that matches biological data.
4. **Dimension–correlation tradeoff** is pervasive — in trained ANNs, DCNNs, and the ventral stream, transformations that increase dimension tend to decrease correlation and vice versa.
5. **SNF increases dramatically in IT** — noise orthogonalization may be a key computational role of higher visual areas.
6. **Geometric decomposition reveals hidden structure** that error curves alone miss.

---

## Relation to Other Papers

- Directly builds on **population geometry** concepts from Langdon et al. (2023) — the "manifold" perspective here is formalized into measurable geometric statistics with provable links to computation.
- Connects to **Cowley et al. (2016)** — dimensionality of V1 responses as a function of stimulus complexity; this paper extends to ask what dimensionality is *optimal* for multitask readout.
- The factorization/disentangling result formalizes the intuition in Langdon et al. that "low-rank connectivity implements causal interactions between distributed activity patterns on the manifold."
- Ventral stream results (V4 → IT noise orthogonalization) complement the hierarchical processing picture in **Mathis et al. (2024)**.
