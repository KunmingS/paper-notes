---
title: "The brain versus AI: World-model-based versatile circuit computation underlying diverse functions in the neocortex and cerebellum"
authors: Ohmae, S. & Ohmae, K.
year: 2024
source: drafts/neuroscience/brain-vs-ai-world-models.pdf
source_url: https://arxiv.org/abs/2411.16075
tags: [neuroai, world-models, predictive-coding, neocortex, cerebellum, prediction-error-learning, transformers, internal-models, model-based-rl, theory, review]
created: 2026-04-08
---

# Brain vs AI: World-Model-Based Versatile Circuit Computation

## TL;DR
A 79-page review (CIBR Beijing, arXiv 2411.16075) arguing that the neocortex *and* cerebellum are best understood as **prediction-error-learning RNNs** that acquire world models, and that modern AI keeps re-converging on this same design. The load-bearing move is methodological: decompose any circuit into **(i) circuit structure, (ii) input/output, (iii) learning algorithm**, and compare brain↔AI element-wise. Doing this beyond the tired "CNN ≈ V1" analogy yields a unified account of sensory, cognitive, and motor function via three processes — **Prediction, Understanding, Generation**.

## Key claims
- **Prediction-error-learning RNNs are the right theoretical primitive for neocortex** — strictly more biologically plausible than deep autoencoders (which are feedforward, lack temporal integration, and use global error signals). Predictive coding circuits (Rao & Ballard) and PredNet (Lotter) are concrete instances; PredNet beats autoencoders on next-frame prediction *and* spontaneously develops disentangled object-parameter codes (identity, view, rotation speed) in its compressed layer.
- **The cerebellum is also a prediction-error-learning RNN, just shallower (3-layer)** — and the same circuit predicts the future in motor control (forward + inverse internal models, Wolpert/Kawato/Ito lineage) and in language. A simulated 3-layer RNN matching cerebellar cytoarchitecture, trained *only* on next-word prediction, spontaneously develops **syntactic classification** (subject/verb/object) in its Purkinje layer (Ohmae K. & Ohmae S. 2024). This is offered as evidence that next-word prediction + syntactic processing are one computation, not two.
- **Convergent evolution in language AI vindicates the brain analogy.** The trajectory GNMT (supervised LSTM) → BERT (unsupervised masked-word) → GPT (unsupervised next-word) is read as AI being dragged toward brain-like learning. fMRI/ECoG studies (Caucheteux 2021; Goldstein 2022; 2023) show GPT-style next-word-prediction signals match neocortical language signals more closely than masked-word or supervised models — i.e., the brain looks more like GPT than like BERT.
- **GPT's repurposing of word *prediction* into sentence *generation* mirrors how the brain reuses one circuit for comprehension and production.** This is the authors' framing of "Generation" — the predictive function gets repointed for action planning, language generation, and imitation learning, plausibly via the mirror neuron system.
- **Model-based RL (Dreamer, Ha & Schmidhuber's "world models")** is the AI counterpart to the neocortex/cerebellum *feeding* the basal ganglia–dopamine system. Humans match model-based RL (not model-free) on Momennejad's transition-revaluation task, and the relevant model is supplied by prefrontal/parietal cortex and lateral cerebellum.
- **Attention in transformers may be a clue to neocortical local computation.** Transformers don't copy cortical wiring (feedforward, parallel input, additive→dot-product attention), but their information flow tracks neocortex closely enough that the authors argue cortical microcircuits should be probed for transformer-like attention motifs and self-attention in particular.
- **Scale matters in a non-trivial way.** Lottery ticket hypothesis + implicit regularization explain why scaled transformers don't overfit and acquire in-context learning; by analogy, neurodevelopmental disorders (autism etc.) may be re-cast as **probabilistic failures of learning stability** in large biological circuits, testable by perturbing brain-imitating ANNs.

## Methods (what's actually new)
- **Three-element decomposition** as a comparison protocol — applied uniformly across vision (autoencoder → predictive coding → PredNet → CNN-RNN → ViT), language (GNMT → BERT → GPT), reinforcement learning (DQN → Dreamer), and motor control (forward/inverse internal models vs. deep RL controllers).
- A **brain-imitating cerebellar ANN** (3-layer RNN matching granule/Purkinje/nucleus connectivity, with inferior-olive-style climbing-fiber error) used as an existence proof that one cerebellar circuit can do both next-word prediction and syntactic processing.
- No new wet-lab data — this is a theoretical synthesis review.

## Why it matters
Reframes the long-standing **internal model theory** (Wolpert/Kawato), **predictive coding** (Rao & Ballard, Friston), and **mirror neuron** literatures as three facets of one prediction-error-learning RNN architecture instantiated twice in the brain (deep in neocortex, shallow in cerebellum). The framing punches above its weight because it (a) gives [[wiki/learning-and-predictive-coding|predictive coding]] a concrete AI-side existence proof beyond toy demos, (b) treats the cerebellum as a *general-purpose* computational organ rather than a motor-only device, and (c) makes a falsifiable bet: the brain is closer to a prediction-error-trained transformer-RNN hybrid than to either a CNN or a vanilla deep autoencoder. It also suggests a research program — build cerebellum-faithful RNNs and break them — for [[wiki/neuroai-and-embodiment|neuroAI]] work on neurodevelopmental disorders.

Worth noting where the paper is weakest: the "neocortex ≈ GPT" claim leans heavily on a small set of fMRI/ECoG correlation studies, the cerebellar syntactic-emergence result is from the authors' own simulation, and the discussion of attention vs. neocortical microcircuits is speculative. The three-element framework itself is more of a useful lens than a theory.

## Related
- [[cell-type-prediction-and-novelty]] — predictive coding at the cell-type level in V1
- [[latent-knowledge-sensory-cortex]] — unsupervised statistical learning in sensory cortex
- [[decoding-the-brain-mechanistic-models]] — encoding/decoding as a complementary NeuroAI program
- [[embodied-neuroai-musculoskeletal]] — motor control and the cerebellum from the embodiment angle
- [[wiki/learning-and-predictive-coding]]
- [[wiki/neuroai-and-embodiment]]
