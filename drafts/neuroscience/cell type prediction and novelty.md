# Cell-type-specific Encoding of Prediction and Reward in Cortical Microcircuits during Novelty Detection

> Sharafeldin, A. & Choi, H. *bioRxiv* (2025).
> DOI: 10.1101/2025.05.13.653877

---

## Core Question

How do distinct cortical cell types (excitatory neurons, VIP and SST interneurons) contribute to novelty detection, and can their roles be explained by a unified framework combining predictive coding and reinforcement learning?

---

## Background

- The brain must detect novel or unexpected stimuli to adaptively allocate attention and learning resources.
- **Predictive coding** posits that the cortex maintains internal predictions and signals prediction errors when expectations are violated.
- **Reinforcement learning (RL)** provides a framework for how reward signals shape behavior and learning.
- Different interneuron subtypes (VIP, SST, PV) form canonical microcircuit motifs (e.g., VIP→SST disinhibition), but their specific computational roles in novelty detection remained unclear.

---

## Methods

- **Computational model** of cortical microcircuits that integrates predictive coding with reinforcement learning.
- Each cell type (excitatory, VIP, SST) is assigned a specific algorithmic role grounded in biological plausibility.
- **Validation** against experimental data from the Allen Brain Map — Visual Behavior dataset (publicly available).
- **Ablation studies** to test the functional necessity of specific circuit motifs (e.g., removing VIP→SST disinhibition).
- **Learning rules**: Adaptation and Hebbian learning are used to model contextual novelty responses.

---

## Key Findings

1. **Cell-type-specific roles**: The model assigns distinct computational functions to each interneuron subtype:
   - Excitatory neurons encode prediction errors.
   - VIP interneurons signal reward-related or surprise signals.
   - SST interneurons contribute to maintaining predictions and gating information flow.

2. **VIP-SST disinhibitory circuit is critical**: Ablation studies reveal that this canonical motif balances energy efficiency (suppressing redundant activity) with representational capacity (allowing novel signals through).

3. **Reproduces experimental data**: The model successfully matches experimentally observed activity patterns across cell types during visual novelty paradigms.

4. **Adaptation + Hebbian learning**: These mechanisms explain contextual novelty responses (e.g., stimulus-specific adaptation), though not all forms of novelty detection are captured.

5. **Unified framework**: Combining predictive coding (normative) with RL (reward-driven) provides a more complete picture than either framework alone.

---

## Significance

- Bridges the gap between abstract computational theories (predictive coding, RL) and biological circuit-level implementation.
- Provides testable predictions about how specific interneuron subtypes should respond during novelty detection tasks.
- Demonstrates that normative principles can be grounded in identified cell types and circuit motifs.

---

## Limitations

- Not all types of novelty responses are explained by adaptation and Hebbian learning alone.
- The model is validated on visual cortex data; generalizability to other cortical areas is not tested.
- Simplifications in circuit architecture (e.g., omitting PV interneurons' detailed role).

---

## Data & Code

- Experimental data: Allen Brain Map — Visual Behavior dataset
- Code: Available on GitHub (see paper for link)
