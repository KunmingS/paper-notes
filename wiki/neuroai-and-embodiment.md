---
type: wiki
tags: [neuroai, embodiment, world-models, encoding-decoding, biomechanics]
---

# NeuroAI and Embodiment

This cluster collects the notes that explicitly sit at the brain–AI interface.

[[brain-vs-ai-world-models]] argues that both neocortex and cerebellum are general-purpose world models whose versatility parallels Transformer-based AI. Its three-element decomposition (circuit structure, I/O, learning algorithm) enables systematic cross-domain brain–AI comparison beyond the standard "CNN ≈ visual cortex" analogy.

[[embodied-neuroai-musculoskeletal]] supplies the counterweight: disembodied "brain in a jar" models miss how bodies shape computation. Feedback dominates even the "feedforward" LGN; biomechanics can offload control entirely (the dead trout in turbulence); the brain commands muscles, not joint positions. Tools like MuJoCo-MJX and full mouse/rat/fly musculoskeletal models now make whole-animal simulation tractable, with Drosophila — connectome plus tractable biomechanics — the leading candidate for a fully integrated neuromechanical model.

[[decoding-the-brain-mechanistic-models]] supplies the formal glue: encoding P(K|x) and decoding P(x|K) are two sides of a cascade that transforms implicit into explicit representations along the ventral stream. It reviews linear, Bayesian, and deep-learning decoders and argues for a shift from descriptive data-driven models to causal mechanistic ones that integrate normative frameworks.

Read together: world-model theory gives the computational thesis, embodiment supplies the biological constraint, and the encoding-decoding framework provides the mathematical language. All three point toward the same goal — a mechanistic, causal NeuroAI.
