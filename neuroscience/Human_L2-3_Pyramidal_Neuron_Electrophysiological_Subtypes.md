# Electrophysiological Classification of Human Layer 2-3 Pyramidal Neurons Reveals Subtype-Specific Synaptic Interactions

> Planert, H., Mittermaier, F. X., Grosser, S. et al. *Nature Neuroscience* (2026).
> DOI: 10.1038/s41593-025-02134-7

---

## Background

The human cerebral cortex, particularly layer 2-3 (L2-3), is greatly expanded compared to other mammals, with increased pyramidal neuron diversity and enhanced corticocortical connectivity. While molecular (transcriptomic) and morphological subtypes of L2-3 glutamatergic pyramidal neurons have been described, a systematic classification based on electrophysiological properties — the functional phenotype most directly relevant to circuit computation — had not been performed. Previous rodent studies showed that pyramidal neuron subtypes (e.g., in L5) differ in long-range and local connectivity, but whether such subtype-specific wiring principles exist in the human cortex remained unknown. The key open question: does the functional diversity of human pyramidal neurons translate into specialized synaptic subnetworks within local microcircuits?

## Method

The authors performed an exceptionally large-scale study using multineuron whole-cell patch-clamp recordings in acute brain slices from human temporal cortex (middle temporal gyrus) obtained from 23 epilepsy surgery patients. Up to ten neurons were recorded simultaneously per experiment, yielding:

- **1,400+ L2-3 pyramidal neurons** characterized electrophysiologically
- **1,400+ monosynaptic connections** identified from ~9,800 tested potential connections
- ~53 neurons and ~62 connections per individual on average

From each neuron, 25 electrophysiological features were extracted (e.g., firing rate, spike shape, adaptation, sag current, input resistance). Unsupervised clustering (hierarchical clustering with bootstrap validation) was applied to classify neurons into electrophysiological types (e-types). Morphological reconstructions via biocytin filling complemented the electrophysiological data. Synaptic properties (amplitude, paired-pulse ratio, latency, kinetics) were analyzed for each connection, and connectivity patterns were examined as a function of pre- and postsynaptic e-type identity.

## Results

**Four electrophysiological subtypes** of L2-3 pyramidal neurons were robustly identified, distinguished primarily by:

- **Firing rate and adaptation** — ranging from low-frequency adapting to high-frequency non-adapting
- **Sag current magnitude** — reflecting differences in HCN channel expression
- **Input resistance and membrane time constant**

These e-types also showed morphological differences, providing independent validation of the classification.

Key synaptic findings:

- **Synaptic amplitudes** followed a log-normal distribution (many weak, few strong synapses), consistent across individuals
- **Subtype-specific synaptic interactions**: Connection probability, synaptic strength, paired-pulse ratio (short-term plasticity), and kinetics all varied systematically depending on the pre- and postsynaptic e-type combination. Some e-type pairs formed stronger, more facilitating connections while others were weaker and depressing.
- **Synaptic subnetworks**: The four e-types formed distinguishable connectivity motifs, suggesting they participate in different computational roles within the L2-3 microcircuit.
- **Conservation across individuals**: These microcircuit organization principles were preserved at the individual patient level, indicating they reflect genuine biological structure rather than inter-individual variability.

The correspondence between e-types and transcriptomic types (t-types) was found to be limited, suggesting that electrophysiological classification captures functional dimensions not fully predicted by gene expression alone — potentially reflecting post-translational regulation of ion channels and synaptic proteins.

The authors conclude that the functional diversity of human L2-3 pyramidal neurons generates a fine-grained network architecture with subtype-specific wiring rules, enabling differential computations within superficial cortical microcircuits.

## Four Electrophysiological Subtypes (E-types)

### 1. SlowAP (~1/3 of neurons, largest group)
- **Low rheobase** (easily excitable)
- **Slow AP upstroke** kinetics
- **Low AP amplitude**
- Synaptic properties: forms **sparse but strong** connections (~0.9 mV mean EPSP) with **depressing** short-term plasticity (PPR ~0.87). Receives fewer incoming connections overall.

### 2. FastAP
- **Fast AP upstroke and downstroke** kinetics
- **More negative resting membrane potential**
- Synaptic properties: homotypic connections are **weak** (~0.45 mV) and **facilitating** (PPR ~1.24). Preferentially projects onto LowRin neurons (21%) more than it receives back (12%).
- Morphology: **shortest total dendritic length**, lowest apical branching complexity.

### 3. DoubSpk (smallest group, rare)
- **Initial doublet spiking** pattern
- **Large ISI adaptation** (steep spike frequency adaptation)
- **Steep afterdepolarization slope**, low AP afterhyperpolarization
- Highest connectivity with LowRin neurons (22-26% connection probability).
- Morphology: **longest basal dendrites**, highest basal branching complexity.

### 4. LowRin
- **High rheobase** (least excitable)
- **Low input resistance**
- **Lower AP frequency**
- Synaptic properties: acts as a **convergence hub** — receives significantly more inputs from all other e-types. Incoming synapses are **weaker** (~0.58 mV) with **facilitating** short-term plasticity (PPR ~1.01).
- Morphology: **longest total dendritic length**, largest apical tuft, largest soma volume, highest apical branching complexity.

### Key Wiring Principles
- **LowRin** neurons are preferential receivers (integration hubs); **SlowAP** neurons form fewer but stronger, depressing connections.
- **FastAP→LowRin** connectivity is notably asymmetric (high forward, low reverse).
- E-type to transcriptomic type (t-type) correspondence is limited — electrophysiological classification captures functional dimensions not predicted by gene expression alone.
- These microcircuit organization principles are **conserved across individual patients**.

---

**Limitations**: Data come from epilepsy surgery tissue (though structural abnormalities were excluded); slice preparation truncates axons/dendrites (mitigated by quality control showing connectivity rates comparable to or exceeding prior studies).
