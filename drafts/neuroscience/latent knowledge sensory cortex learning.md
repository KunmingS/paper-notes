# Rapid Emergence of Latent Knowledge in the Sensory Cortex Drives Learning

> Drieu, C., Zhu, Z., Wang, Z., Fuller, K., Wang, A., Elnozahy, S. & Kuchibhotla, K. *Nature* (2025).
> DOI: 10.1038/s41586-025-08730-8

---

## Core Question

If animals learn task contingencies rapidly but sensory cortical cue representations change slowly, what is the auditory cortex (AC) actually doing during learning? Does it go beyond classical cue-related plasticity to encode higher-order signals that drive rapid associative learning?

---

## Paper Type

**Research article** — combines longitudinal two-photon calcium imaging, probabilistic optogenetic silencing, tensor decomposition, and a behavioral paradigm that dissociates learning from performance in mice.

---

## The Key Dissociation: Learning vs. Performance

- **Auditory go/no-go task**: lick to S+ (target tone) for reward, withhold to S- (foil tone) to avoid timeout.
- **Probe trials** (no reinforcement): reveal task knowledge without contamination by reinforcement feedback.
- **Result**: Task knowledge (measured in probe trials) emerges **rapidly within tens of trials**, but behavioral performance (in reinforced trials) improves only gradually over hundreds–thousands of trials.
- Reinforcement feedback paradoxically **masks** underlying task knowledge.

---

## AC Is the Default Learning Pathway (But Becomes Dispensable)

Probabilistic bilateral AC silencing (PV-ChR2, 90% of reinforced trials silenced):

1. **Performance impaired** on silenced trials throughout learning.
2. **Rapid learning impaired** — even on non-silenced probe trials, PV-ChR2 mice showed delayed acquisition, lower discrimination, longer lick latencies.
3. **AC becomes dispensable at expert level** — silencing effect wanes as mice master the task. Silencing AC only after reaching expert performance shows no deficit.
4. **Control**: Visual cortex silencing has no effect → specific to AC.

**Interpretation**: AC tutors subcortical structures (inferior colliculus, MGB, striatum) during learning; once associations are consolidated subcortically, AC is no longer needed.

---

## Six Neural Dynamics Discovered via Tensor Decomposition

Longitudinal 2-photon imaging of ~4,643 L2/3 excitatory neurons across learning and passive mice. Data organized as 4D tensor (neurons × within-trial time × across-trial learning × trial outcome), decomposed unsupervised into 6 dynamics:

### Passive Network (Dynamics 1–2, ~77% of passive cells)
- **Cell ensemble 1**: Non-selective tone-evoked activation that habituates over time.
- **Cell ensemble 2**: Non-selective tone-evoked suppression that habituates.
- Both decrease with repeated stimulus exposure (stimulus-specific adaptation).

### Learning Network — Sensory (Dynamics 3–4, ~31% of learning cells)
- **Cell ensemble 3**: S- selective tone responses, modest habituation.
- **Cell ensemble 4**: S+ selective tone responses throughout learning.
- Learning **counteracts habituation** and maintains stimulus selectivity.

### Learning Network — Higher-Order (Dynamics 5–6)
- **Cell ensemble 5 (Reward Prediction)**: ~7% of learning network.
- **Cell ensemble 6 (Action Suppression)**: ~31% of learning network.
- These are the paper's central discoveries (see below).

---

## Key Finding 1: Reward Prediction Signal

**Cell ensemble 5** shows **late-in-trial** activity (delayed from tone onset) on hit trials.

### Properties:
- **Not sensory**: Absent on miss trials (same S+ tone, no lick).
- **Not reward consumption**: Persists in probe hit trials (reward omitted).
- **Not licking/motor**: No response to spontaneous lick bouts outside task; absent on FA trials with similar licking.
- **Emerges within ~40 hit trials** — on the first day of training.
- **Peaks during acquisition, fades at expert level** — mirrors the AC dispensability timeline.
- Present on **knowledge-related FA errors** (RP+ trials) early in learning but not on impulsive/exploratory FAs (RP- trials).

### Causal Role (closed-loop optogenetics):
- **Post-hit silencing**: Weakened stimulus-action association, delayed discrimination learning.
- **Post-FA silencing**: Even stronger impairment — delayed discrimination, impaired probe accuracy.
- **Post-VC silencing**: No effect (control).
- Silencing occurs **after** the lick response → cannot affect current trial, only subsequent learning.

**Conclusion**: Reward prediction activity in AC serves as a **teaching signal** for associative learning, critical on both correct (hit) and incorrect (FA) trials.

---

## Key Finding 2: Action Suppression Signal

**Cell ensemble 6** shows late-in-trial activity specifically on **correct reject** (CR) trials.

### Properties:
- **Abruptly drops at first lick** on FA trials — tied to moment of suppression failure.
- **Absent on miss trials** — not general "no-lick" signal; contingency-specific (S- only).
- **Drops during disengagement** — reflects active cognitive process, not passive absence of licking.
- **Stable throughout training** despite increasing CR rate → all-or-none, tied to performance not learning.

### Causal Role:
- **Full-trial AC silencing on S- trials**: Increases both FA rate AND lick probability.
- **Tone-only AC silencing**: Increases FA rate but NOT lick probability.
- The difference confirms that the **late-in-trial** (post-tone) activity specifically drives lick suppression.

---

## No Cortical Map Expansion

Contrary to the classical model of sensory cortical learning:
- **No increase** in tonotopic map representation of S+ or S- after learning (modest decrease).
- **No increase** in fraction of neurons responding to S+/S-.
- **Decreased** response amplitude in neurons initially tuned to S+/S-.
- Learning networks showed **less** local tonotopic change than passive networks.
- Stimulus identity could be decoded from AC from day 1 with no improvement → no perceptual sharpening needed.

---

## Spatial Organization

- Reward prediction and action suppression ensembles are **spatially clustered** within AC.
- But they are **uncoupled from tonotopy** — reward prediction neurons don't preferentially have S+ as best frequency, nor do action suppression neurons prefer S-.
- Equal proportions of S+/S- preferring neurons in both ensembles.
- → **Higher-order functional segregation** within sensory cortex, independent of stimulus selectivity.

---

## Neural Decoding of Error Types

Using the reward prediction signal to classify individual FA trials:
- **RP+ FAs** (reward prediction present): Knowledge-related errors — mouse incorrectly expects reward on S-.
- **RP- FAs** (no reward prediction): Impulsive/exploratory errors.
- RP+ errors peak during acquisition phase, disappear by expert phase.
- Neural activity reveals the **cognitive driver** of errors that behavior alone cannot distinguish.

---

## Key Takeaways

1. **Sensory cortex is a "sensory-enriched associative cortex"** — not just for perception, but for higher-order computations that drive rapid associative learning.
2. **Two separable, causal higher-order signals** in AC:
   - Reward prediction (cell ensemble 5) → drives rapid learning (tens of trials).
   - Action suppression (cell ensemble 6) → drives slower performance improvement.
3. **No cortical map expansion** is needed for learning simple discriminations — the classical cue-plasticity model is insufficient.
4. **AC is the default learning pathway but becomes dispensable** at expert level — potentially tutoring subcortical structures.
5. **Latent knowledge** exists in the brain before behavioral expression — learning and performance are neurally dissociable.
6. **Higher-order ensembles are spatially clustered but functionally uncoupled from sensory tuning** — suggesting an organizational principle where associative and sensory computations coexist but are separable within the same cortical network.

---

## Relation to Other Papers

- Challenges the classical view that sensory cortex contributes to learning primarily via cue-related representational plasticity (map expansion, tuning shifts).
- The rapid emergence of reward prediction connects to **Wakhloo et al. (2025)** — the normative prediction that optimal codes are low-dimensional with high correlation early in learning aligns with the rapid, focused emergence of the reward prediction signal.
- The tensor decomposition approach to identifying separable dynamics relates to the manifold perspective in **Langdon et al. (2023)** — here, distinct dynamics correspond to functionally separable low-dimensional signals within the same neural population.
- The finding that ~30% of AC neurons remain passive/habituating despite learning echoes the "limited repertoire of basis patterns" idea from **Cowley et al. (2016)** — the circuit maintains unused capacity.
