# The Brain versus AI: World-model-based Versatile Circuit Computation Underlying Diverse Functions in the Neocortex and Cerebellum

> Ohmae, S. & Ohmae, K. *arXiv* 2411.16075 (2024).
> Affiliation: Chinese Institute for Brain Research (CIBR), Beijing, China

---

## Core Question

How do the neocortex and cerebellum — despite having uniform circuit structures — achieve such a diverse range of functions across sensory, cognitive, and motor domains? Can AI's general-purpose computation framework explain this versatility?

---

## Motivation

- AI has achieved remarkable versatility using general-purpose circuit computations (e.g., Transformers).
- The brain similarly uses uniform circuit architectures (cortical columns, cerebellar microcircuits) to support wildly different functions.
- Prior comparisons between brain and AI were limited to brain-inspired vision AI vs. visual neocortex.
- This paper broadens the comparison across all functional domains.

---

## Three-Element Framework

The authors decompose circuit computation into three elements to enable cross-domain comparison between brain and AI:

1. **Circuit structure** — the wiring/architecture (e.g., cortical layers, Transformer blocks)
2. **Inputs/Outputs** — what information flows in and out
3. **Learning algorithm** — how the system adapts (e.g., backprop, prediction error-driven plasticity)

By evaluating similarities for each element, they identify wide-ranging parallels and convergent evolution between biological and artificial systems.

---

## World-Model Theory

The central proposal: both the neocortex and cerebellum function as **world models** — they predict future events from past information and learn from prediction errors. This unifies their diverse functions under three core processes:

1. **Prediction** — generating future information (e.g., predicting sensory consequences of motor commands)
2. **Understanding** — interpreting the external world via compressed sensory representations (building internal models)
3. **Generation** — repurposing prediction machinery for diverse outputs (e.g., motor planning, imagination, language generation)

---

## Brain–AI Similarities

- Both use uniform architectures to handle diverse tasks.
- Both rely on prediction and prediction-error learning as a core computational principle.
- The neocortex's hierarchical processing parallels deep network architectures.
- The cerebellum's forward models parallel model-based RL and predictive control in AI.
- Convergent evolution: similar computational solutions emerged independently in biological and artificial systems.

---

## Neocortex vs. Cerebellum

- Both regions have remarkably **uniform internal circuitry** yet support diverse functions.
- **Neocortex**: hierarchical, recurrent, handles perception, cognition, language, motor planning.
- **Cerebellum**: feedforward-dominant, handles prediction, timing, motor coordination, and increasingly recognized cognitive roles.
- The paper integrates established theories:
  - **Internal model theory** (Wolpert, Kawato) — cerebellum as forward/inverse model
  - **Mirror neuron system** — neocortical prediction of others' actions
  - **Predictive coding** — hierarchical prediction error minimization in neocortex

---

## Key Insight

The versatility of both brain structures and AI systems stems from the same principle: a **general-purpose computational architecture** that can be repurposed for diverse tasks by changing inputs/outputs and training signals, while keeping the core circuit structure and learning algorithm constant.

---

## Significance

- Provides a unified framework connecting AI computation with both neocortex and cerebellum function.
- Goes beyond the standard "visual cortex ≈ CNN" analogy to encompass all functional domains.
- Proposes testable predictions about shared computational principles.
- Bridges internal model theory, predictive coding, and modern AI architectures under one roof.

---

## Notes

- 79-page paper — extensive review with detailed comparisons.
- arXiv preprint; not yet peer-reviewed.
- From CIBR Beijing — computational/theoretical neuroscience perspective.
