# A Unifying Perspective on Neural Manifolds and Circuits for Cognition

> Langdon, C., Genkin, M. & Engel, T. A. *Nature Reviews Neuroscience* 24, 363–377 (2023).
> DOI: 10.1038/s41583-023-00693-x

---

## Core Question

How can the two dominant frameworks for understanding brain computation — **neural manifolds** (low-dimensional population dynamics) and **neural circuits** (connectivity-based mechanisms) — be unified to achieve a causal, testable understanding of cognition?

---

## Paper Type

**Perspective** — synthesizes theoretical and experimental work arguing that manifold and circuit approaches are inseparable, not competing paradigms.

---

## The Two Perspectives

### Circuit Perspective
- Emphasizes **connectivity** as the substrate for computation.
- Classical models: hand-crafted connectivity (e.g., clustered, ring) → specific dynamics (attractors, decision-making).
- **Strength**: Enables causal predictions — perturbations of connectivity/activity have testable behavioral effects.
- **Weakness**: Simple connectivity → homogeneous tuning; cannot explain the distributed mixed selectivity seen in large-scale recordings.

### Manifold Perspective
- Emphasizes **low-dimensional structure** in heterogeneous population activity.
- Dimensionality reduction reveals interpretable manifolds (rings, tori, branching trajectories) matching task topology.
- **Strength**: Compresses complex, heterogeneous single-neuron responses into interpretable population-level descriptions.
- **Weakness**: Purely descriptive — no causal mechanism, no unique predictions for perturbation experiments. Different statistical methods can yield contradictory conclusions.

---

## Key Concepts

### Neural Manifolds (Box 1)
- **State space**: N-dimensional space where each axis = one neuron's firing rate.
- **Manifold**: The low-dimensional surface that population activity actually explores.
- **Intrinsic dimensionality**: Minimal continuous variables needed to parameterize the manifold (e.g., 1 for a ring).
- **Linear dimensionality**: Number of orthogonal directions spanning the embedding subspace (can be much higher).
- Manifold geometry is jointly defined by the tuning curves of all neurons in the population.

### Distributed Mixed Selectivity
- Single neurons respond to combinations of multiple task variables with diverse temporal profiles.
- Only ~5–10% of PFC neurons show classical tonic persistent activity during working memory.
- This heterogeneity is the norm, not the exception, in cortical recordings.

### Low-Rank Connectivity (Box 3)
- **Rank-one connectivity**: J = m · nᵀ (outer product of two N-dimensional vectors).
- Activity along direction **n** drives activity along direction **m** → substrate for computation.
- Multiple rank-one terms compose higher-rank (but still low-dimensional) connectivity.
- Low-rank connectivity constrains dynamics to a low-dimensional manifold.
- Key insight: **low-dimensional manifolds can arise from low-dimensional connectivity structure**, even in large heterogeneous networks.

### Latent Circuits (Box 4)
- A low-dimensional dynamical system **latent** in the high-dimensional network.
- Embedding matrix **Q** maps between latent circuit nodes and high-dimensional activity patterns.
- Node i in latent circuit → direction q(i) in state space.
- Edge from j to i → outer product q(i)·q(j)ᵀ in full connectivity.
- Enables translating perturbations from low-dimensional circuit to high-dimensional network → **causal testing**.

---

## Case Studies

### 1. Head Direction System — Perfect Convergence

**Manifold**: Ring topology encoding head direction angle (1D circular variable).
- Mouse anterodorsal thalamus: ring manifold, nonlinearly embedded with complex multimodal tuning curves.
- *Drosophila* ellipsoid body: ring beautifully visible in circular neuropil structure; activity "bump" tracks heading.

**Circuit**: Ring attractor model (Skaggs et al., 1995; Zhang, 1996).
- Local excitation + global inhibition → persistent, unique bump.
- Landmark cells anchor to visual cues.
- Rotation cells (P-EN neurons) update bump via asymmetric connections for angular velocity integration.

**Convergence**: Electron microscopy + RNA profiling in *Drosophila* confirmed predictions at single-cell resolution:
- E-PG neurons sustain bump via local excitation.
- P-EN neurons rotate bump via asymmetric connections (left/right protocerebral bridge → clockwise/anticlockwise).
- Theoretical predictions from 20+ years ago validated experimentally.

**Key lesson**: Topology of connectivity can differ from spatial layout. Ring topology can exist without spatial ring arrangement (relevant for rodent system, which lacks topography).

### 2. Grid Cells — Converging but Not Yet Confirmed

**Manifold**: Toroidal topology in MEC grid cells.
- Neuropixels recordings from thousands of grid cells revealed torus manifold.
- Torus is rigid across environments and behavioral states (wake/sleep) → likely arises from connectivity, not input.
- Individual cells tuned to fixed locations on torus regardless of environment.

**Circuit**: 2D continuous attractor model.
- Cells on 2D torus with distance-dependent excitation.
- Multiple bumps form spontaneously → grid-like spatial firing.
- Velocity integration via asymmetric connections (analogous to rotation cells in head direction).

**Gap**: Direct anatomical connectivity measurements not yet available in mammals. Alternative models (periodic vs. aperiodic boundary conditions) could be tested via perturbation experiments (cortical cooling, inhibition gain manipulation).

**RNN insight**: Trained RNNs for path integration reveal hidden low-dimensional connectivity matching hand-crafted attractor models, but superimposed on random connectivity — not obvious from individual unit connections. **Theory was essential** for identifying this structure.

### 3. Cognitive Systems — Emerging Convergence via Low-Rank Theory

**Working memory** (PFC):
- Population activity contains a stable ring encoding remembered location in a subspace.
- Temporal variation occurs in orthogonal non-coding subspace → doesn't interfere with memory.
- Single neurons are heterogeneous because coding/non-coding subspaces are rotated relative to neural axes.

**Decision-making**:
- Branching manifold trajectories diverge at decision points.
- Topology mirrors task structure (e.g., sequential category decisions → branching manifold).

**Low-rank RNNs**: Engineered networks with low-rank connectivity produce dynamics on low-dimensional manifolds solving cognitive tasks.
- Low-rank connectivity implements causal interactions between distributed activity patterns.
- Latent circuit inference from neural data can recover this structure and generate testable predictions.
- Validated in RNNs via patterned perturbations of activity and connectivity.

---

## Critical Arguments

### Why Circuits Matter (Beyond Manifolds)
1. **Manifolds are not unique** — different dimensionality reduction methods yield different manifolds from the same data. Without mechanistic grounding, no objective way to adjudicate.
2. **Causal testing** requires circuit-level predictions. Perturbation experiments need to know *what* to perturb and *what* to expect.
3. **Theory guides discovery** — without prior intuition from circuit models, identifying low-dimensional structure in high-dimensional connectivity data is "extremely challenging."
4. **Clinical relevance** — mechanistic understanding enables interfacing with circuits to treat mental disorders.

### The Latent Circuit Framework
- Fits neural responses with a model: high-dimensional activity = embedding of low-dimensional dynamics from a nonlinear latent circuit.
- Simultaneously infers connectivity and embedding from data.
- Different from standard dimensionality reduction: incorporates biologically plausible nonlinearity, task inputs/outputs.
- Different from full RNN fitting: infers only the low-dimensional structure (better constrained, more interpretable).
- **Key result**: Latent circuit approach and regression-based demixing gave contradictory conclusions about irrelevant stimulus representations in context-dependent decision-making RNNs; only latent circuit predictions survived causal perturbation testing.

---

## Key Takeaways

1. **Manifolds and circuits are inseparable** — manifolds arise from low-dimensional connectivity structure; circuits are distributed across heterogeneous populations via low-rank connectivity.
2. **The fly head direction system** is the gold standard: 20-year-old ring attractor predictions confirmed at single-cell resolution.
3. **Grid cells** show the path forward: toroidal manifold established, circuit confirmation pending.
4. **Low-rank connectivity** bridges classical circuit models (few homogeneous nodes) with modern manifold descriptions (heterogeneous high-dimensional networks).
5. **Latent circuit inference** is a promising framework for extracting testable circuit mechanisms from neural data in cortical systems with mixed selectivity.
6. **Manifolds alone are insufficient** — they are descriptive, method-dependent, and lack causal power. The goal is not just dynamics on manifolds, but the circuit mechanisms generating those dynamics.

---

## Relation to Other Papers

- Connects to **Decoding the Brain** (Mathis et al., 2024) — encoding-decoding cascade relates to how information is transformed across circuit stages.
- Extends attractor network theory (Wang, 2002; Wong & Wang, 2006) from homogeneous to heterogeneous (distributed mixed selectivity) regimes.
- Complements the "computation through neural population dynamics" view (Vyas et al., 2020) by insisting on circuit grounding.
- Challenges the strong manifold-only view (Barack & Krakauer, 2021) that circuit-level understanding may be unnecessary.
