# From MEI to VEI: Inception Loops and Bipartite Invariance in Mouse V1

## Core Question

How does the visual system recognize stable features despite continuous changes in sensory input (distance, pose, illumination, etc.)? Answering this requires understanding two dimensions:
- **Selectivity**: What stimulus does a neuron prefer most?
- **Invariance**: What variations can a neuron tolerate while maintaining a strong response?

---

## Paper 1: Walker et al. 2019 — Inception Loops Discover What Excites Neurons Most

> Walker, E. Y. et al. *Nature Neuroscience* 22, 2060–2065 (2019).
> DOI: 10.1038/s41593-019-0517-x

### Background

Traditional approaches to understanding V1 neurons had key limitations:

1. **Linear models (LN model)**: Assume neurons are linear filters. The estimated receptive field (RF) is typically a Gabor filter (alternating light/dark stripes). But cortical neurons are highly nonlinear — linear models have poor predictive power.
2. **Manual search**: Present hand-designed stimuli (gratings, natural images) and observe responses. But the image space is infinite-dimensional and cannot be exhaustively sampled.

Core problem: finding the optimal stimulus for a nonlinear neuron requires searching an intractably high-dimensional image space, but experimental time is severely limited.

### Method: Inception Loop

A closed-loop paradigm: record → model → generate → verify.

- **Day 1**: Present ~5,100 natural images to awake mice; record V1 L2/3 responses with two-photon calcium imaging (~5,300–8,500 neurons/mouse, 5 mice).
- **Overnight**: Train a CNN model (digital twin) to predict neuronal responses (achieves 77.8% of oracle performance). Use gradient ascent to find the Most Exciting Input (MEI) for each target neuron.
- **Day 2**: Present MEIs back to the same neurons in the same mouse to verify model predictions.

### Results

1. **MEIs are not Gabors**: Most V1 MEIs exhibit complex spatial features — sharp corners, checkerboard patterns, pointillist textures, curved strokes. This shows that V1 neurons have nonlinear feature selectivity (pixel interactions matter; responses cannot be decomposed into independent per-pixel contributions).
2. **MEIs are highly specific**: Each MEI strongly activates only its target neuron, not others.
3. **MEIs outperform all other stimuli**: MEI > linear RF > best Gabor > best natural image crop.
4. **Accurate model predictions**: Pearson r = 0.68 between predicted and observed responses to MEIs.

### Limitation

MEI identifies only a single optimal image per neuron. It does not reveal the invariance dimension — what variations the neuron tolerates.

---

## Paper 2: Ding, Tran et al. 2026 — Functional Bipartite Invariance in Mouse V1 Receptive Fields

> Ding, Z., Tran, D. et al. *Nature Neuroscience* (2026).
> DOI: 10.1038/s41593-026-02213-3

### Background

Building on the 2019 MEI work, this paper tackles the invariance problem. The classical framework includes:
- **Simple cells**: Respond to a bar/edge at a specific position, orientation, and phase. No invariance.
- **Complex cells**: Respond to a specific orientation and spatial frequency regardless of phase. Phase invariant.

However, the real picture in V1 is likely far more complex than this simple/complex dichotomy. A systematic method to explore neuronal invariances was lacking.

### Method

Extends the inception loop from MEI to **Varied Exciting Inputs (VEIs)**:

1. **Large-scale recording**: Two-photon calcium imaging of ~33,700 V1 L2/3 neurons responding to ~5,100 natural images (14 mice). Median model performance CCnorm = 0.71.
2. **VEI synthesis**: For each neuron, starting from MEI, generate 20 images that simultaneously:
   - Activate the target neuron at ≥ 85% of MEI response
   - Are maximally dissimilar from each other in pixel space
3. **In vivo verification**: Present VEIs back to the same neurons.

Parameterized models to quantify invariance:
- **VEIs_full** (full-texture): Model the RF as a shift-invariant texture detector (random crops from an optimized texture canvas).
- **VEIs_partial** (bipartite): Split the RF into a **fixed subfield** (locked spatial pattern from MEI) + a **variable subfield** (shift-invariant texture crops).

Additional analyses:
- CUB bird dataset (with segmentation masks) to test alignment with natural object boundaries.
- MICrONS dataset (electron microscopy + functional recordings) to examine synaptic connectivity.

### Results

1. **VEIs effectively capture invariance**: VEIs activate target neurons at ~75% of MEI response in vivo. V1 population decoding accuracy between VEI pairs = 80%.

2. **Discovery of bipartite invariance**: Most V1 neurons are neither simple nor complex cells. They exhibit a novel bipartite receptive field structure:

| Subfield | Invariance | Spatial frequency preference |
|----------|-----------|---------------------------|
| Fixed (locked pattern) | None | Low frequency (coarse structure) |
| Variable (shift-tolerant) | Shift invariant | High frequency (fine texture) |

This cannot be explained by simple/complex cell mixtures or center-surround mechanisms.

3. **Alignment with object boundaries**: The bipartite RF division aligns with object–background boundaries in natural images. 99.1% of V1 neurons prefer images containing boundaries over single gratings, especially boundaries defined by spatial frequency differences. This suggests a contribution to figure-ground segmentation.

4. **Synaptic hierarchy of invariance** (MICrONS analysis):
   - Synaptically connected pairs show higher MEI/VEI similarity than proximity-matched controls (like-to-like connectivity).
   - Postsynaptic neurons exhibit greater invariance than presynaptic neurons → invariance builds across synaptic stages.
   - Neurons with lower invariance form more synaptic connections → they serve as building blocks for downstream invariant representations.

---

## Relationship Between the Two Papers

```
Traditional methods (manually test gratings, etc.)
    | Limitation: cannot search high-dimensional image space
    v
Walker 2019: Inception Loop + MEI
    | Found that V1 neurons prefer complex nonlinear features
    | But only identified 1 optimal image per neuron
    v
Ding et al. 2026: VEIs (20 diverse but strongly activating images)
    | Discovered bipartite invariance: fixed + variable subfield
    | Aligned with object boundaries → figure-ground segmentation
    | Invariance increases along synaptic hierarchy
```

## Key Concepts

- **MEI (Most Exciting Input)**: The single image that maximally activates a given neuron.
- **VEI (Varied Exciting Input)**: A set of dissimilar images that all strongly activate the same neuron, revealing its invariance.
- **Inception Loop**: Closed-loop paradigm: record → model → synthesize stimuli → verify in vivo.
- **Digital Twin**: A CNN model trained to predict a neuron's response to arbitrary images.
- **Simple Cell**: No invariance. Sensitive to specific position, orientation, and phase.
- **Complex Cell**: Phase invariant. Responds to a preferred orientation/spatial frequency regardless of phase.
- **Spatial Frequency**: How rapidly a pattern changes across space. High = fine detail; Low = coarse structure.
- **Phase**: The position of light/dark parts within one cycle of a periodic pattern.
- **Bipartite Invariance**: RF divided into two subfields — one fixed (low frequency, no invariance) and one variable (high frequency, shift invariant).
- **MICrONS**: Large-scale dataset combining functional recordings with electron microscopy synaptic reconstruction.
