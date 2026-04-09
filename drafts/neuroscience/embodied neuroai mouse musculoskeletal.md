## Breaking the Jar: Why NeuroAI Needs Embodiment

> Brunton, B. W. & Tuthill, J. C. *The Transmitter* (July 21, 2025).
> https://www.thetransmitter.org/neuroai/breaking-the-jar-why-neuroai-needs-embodiment/

---

## Core Argument

The dominant "brain in a jar" framing in neuroscience — treating the brain as an isolated computational system — is fundamentally incomplete. The function of the brain is **inexorably shaped by the body**. NeuroAI must embrace **embodiment**: modeling neural systems together with the bodies they evolved to sense and control.

---

## Article Type

**Perspective / Opinion** — argues for integrating biomechanics and sensorimotor feedback into computational neuroscience and NeuroAI, drawing on recent tools and datasets.

---

## Three Pillars of Embodied Intelligence

### 1. Feedback

- Biological neural networks rely on **constant, multiscale feedback**, not simple feedforward processing.
- Key example: The vast majority of lateral geniculate nucleus (LGN) inputs are **not from the retina** — contradicting the textbook hierarchical model of vision.
- Animals continuously interact with fluctuating environments through recurrent neural connections and organ-to-organ feedback loops.
- Implication: Feedforward models of sensory processing miss the dominant mode of neural computation.

### 2. Biomechanics

- Specific body features critically influence — and simplify — neural control demands.
- Striking example: A **dead trout's body** undulates and surges upstream when placed in turbulent flow behind a rock. This requires **zero neural activity** — it arises entirely from the interaction between vortex shedding from the rock and the passive biomechanics of the fish body.
- Key insight: **Mechanical intelligence of the body can simplify the demands of nonlinear neural control.** The nervous system doesn't need to solve the full control problem because the body's physics does part of the work.
- Corollary: The brain does not directly control positions of knees, elbows, and shoulders — it controls **muscles**, which generate **forces** to move bodies. Models must respect this.

### 3. Modularity

- Despite advocating for integration, brains do exhibit **modular organization**.
- **Bottlenecks** — retinal ganglion cells, motor neurons — serve as natural interfaces between modules.
- This modularity is a feature, not a bug: it allows researchers to develop computational models at different resolutions that still interface coherently.
- Practical benefit: Not everything must be modeled at once; modules can be developed and validated independently, then composed.

---

## Historical and Community Context

- Embodiment is not a new idea in neuroscience, but it receives **insufficient attention** when studying higher-order cognitive functions.
- Recent momentum:
  - **Anthony Zador (CSHL)**: Proposed an **embodied Turing test** (2023) — evaluating intelligence through sensorimotor interaction with an environment rather than disembodied language.
  - **2024 NIH BRAIN NeuroAI Workshop**: Embodiment featured prominently as a priority.

---

## Tools and Technologies Enabling Embodied Modeling

| Tool | Description |
|------|-------------|
| **MuJoCo** | Physics engine simulating biomechanics of skeletons, muscles, and tendons; originally developed for robotics |
| **MuJoCo-MJX** | GPU-accelerated JAX implementation making whole-body virtual animal training computationally tractable |
| **Biomechanical datasets** | Full-body biomechanical models now exist for **rats, mice, and flies** |
| **Mouse musculoskeletal model** | First fully articulated whole-body musculoskeletal model of the mouse, including all four limbs, spine, head, and tail with full 3D kinematics and kinetics ([Ramalingasetty et al., IEEE Access 2021](https://ieeexplore.ieee.org/document/9638502)) |

---

## Papers Citing the Mouse Musculoskeletal Model (~45 on Google Scholar)

Source: [Google Scholar citations](https://scholar.google.com/scholar?cites=314920179510442633&as_sdt=2005&sciodt=0,5&hl=en)

### Neuromechanical Simulation & Virtual Animals

| Paper                                                                                                                                                                              | Authors                                       | Journal         | Year      | Cited by | Key Contribution                                                                                                                     |     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- | --------------- | --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------ | --- |
| [A virtual rodent predicts the structure of neural activity across behaviours](https://www.nature.com/articles/s41586-024-07633-4)                                                 | Aldarondo D, Merel J, Marshall JD, et al.     | Nature          | 2024      | 79       | DeepMind virtual mouse — RL-trained neural network controller produces neural activity patterns matching real mouse brain recordings |     |
| [MIMIC-MJX: Neuromechanical Emulation of Animal Behavior](https://arxiv.org/abs/2511.20532)                                                                                        | Zhang CY, Yang Y, Sirbu A, et al.             | ArXiv           | 2025      | 3        | GPU-accelerated neuromechanical emulation framework for animal behavior                                                              |     |
| [Massively Parallel Imitation Learning of Mouse Forelimb Musculoskeletal Reaching Dynamics](https://pmc.ncbi.nlm.nih.gov/articles/PMC12676374/)                                    | Leonardis E, Nagamori A, et al.               | ArXiv           | 2025      | —        | Imitation learning applied to mouse forelimb musculoskeletal reaching                                                                |     |
| [FARMS: Framework for Animal and Robot Modeling and Simulation](https://pmc.ncbi.nlm.nih.gov/articles/PMC10827226/)                                                                | Arreguit J, Tata Ramalingasetty S, Ijspeert A | bioRxiv         | 2023/2025 | 17       | General framework for animal and robot neuromechanical simulation (from same lab)                                                    |     |
| [An integrated neuromechanical model of the mouse to study neural control of locomotion](https://ir.library.osaka-u.ac.jp/repo/ouka/all/92326/P71-AMAM2023-tataramalingasetty.pdf) | Ramalingasetty ST, Markin SN, et al.          | AMAM Conference | 2023      | 1        | Conference paper extending the original model to study locomotor neural control (from same lab)                                      |     |

### Reviews & Perspectives

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [Integration of feedforward and feedback control in the neuromechanics of vertebrate locomotion: a review](https://journals.biologists.com/jeb/article-abstract/226/15/jeb245784/325856) | Ijspeert AJ, Daley MA | J Exp Biology | 2023 | 75 | Major review on neuromechanical control of vertebrate locomotion combining experimental, simulation, and robotic studies |
| [Embodied sensorimotor control: computational modeling of the neural control of movement](https://www.annualreviews.org/content/journals/10.1146/annurev-bioeng-102723-020454) | Almani MN, Lazzari J, Walker JD, et al. | Annu Rev Bioeng | 2026 | — | Review of how sensorimotor control arises from interacting neural populations, feedback mechanisms, and body biomechanics |
| [NeuroAI for AI safety](https://arxiv.org/abs/2411.18526) | Mineault P, Zanichelli N, Peng JZ, Arkhipov A, et al. | ArXiv | 2024 | 18 | Argues neuroscience-informed approaches (including embodiment) are key for AI safety |

### Embodied Spiking Neural Network Models

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [Embodied bidirectional simulation of a spiking cortico-basal ganglia-cerebellar-thalamic brain model and a mouse musculoskeletal body model](https://www.frontiersin.org/journals/neurorobotics/articles/10.3389/fnbot.2023.1269848/full) | Kuniyoshi Y, et al. | Front Neurorobot | 2023 | 9 | Full brain model coupled with mouse body model, distributed across supercomputer Fugaku |
| [Deploying and Optimizing Embodied Simulations of Large-Scale Spiking Neural Networks on HPC Infrastructure](https://www.frontiersin.org/journals/neuroinformatics/articles/10.3389/fninf.2022.884180/full) | Feldotto B, et al. | Front Neuroinform | 2022 | 20 | HPC infrastructure for embodied spiking network simulations |
| [Gradient Descent Optimization of Embodied SNNs](https://repository.tudelft.nl/file/File_8316498e-5531-45a2-bdaa-1f8476c63eb4?preview=1) | Brand J | TU Delft thesis | — | — | Training spiking neural networks for embodied control |

### Biomechanical Modeling & Muscle Function

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [A novel biomechanical model of the proximal mouse forelimb predicts muscle activity in optimal control simulations of reaching](https://journals.physiology.org/doi/abs/10.1152/jn.00499.2024) | Gilmer JI, et al. | J Neurophysiol | 2025 | 6 | Detailed forelimb biomechanical model predicting muscle activity during reaching |
| [JiSuJi, a virtual muscle for small animal simulations, accurately predicts force from naturalistic spike trains](https://pmc.ncbi.nlm.nih.gov/articles/PMC12262632/) | Jiang W, et al. | bioRxiv | 2025 | — | Virtual muscle model for small animals driven by realistic spike trains |
| [ArborSim: Articulated, branching, OpenSim routing for constructing models of multi-jointed appendages](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1012243) | Fu X, et al. | PLoS Comput Biol | 2024 | 7 | Tool for modeling complex muscle-tendon architecture in multi-jointed limbs |
| [Motor unit mechanisms of speed control in mouse locomotion](https://pmc.ncbi.nlm.nih.gov/articles/PMC12485791/) | Thomas K, et al. | bioRxiv | 2025 | 3 | How motor units control locomotion speed in mice |
| [muSim: A goal-driven framework for elucidating the neural control of movement through musculoskeletal modeling](https://www.biorxiv.org/content/10.1101/2024.02.02.578628.abstract) | Almani MN, Lazzari J, Saxena S | bioRxiv | 2024 | 9 | Framework connecting motor cortex goals to musculoskeletal execution in dynamic environments |
| [Neuro-musculoskeletal modeling reveals muscle-level neural dynamics of adaptive learning in sensorimotor cortex](https://www.biorxiv.org/content/10.1101/2024.09.11.612513.abstract) | DeWolf T, Schneider S, et al. | bioRxiv | 2024 | 20 | Reveals how sensorimotor cortex dynamics couple to muscle-level control during adaptive learning |
| [A real-time control system of upper-limb human musculoskeletal model with environmental integration](https://ieeexplore.ieee.org/abstract/document/10185016/) | Saputra AA, et al. | IEEE Access | 2023 | 11 | Real-time musculoskeletal simulation with environment coupling |
| [Passive responses in mouse hind leg locomotion](https://www.cell.com/current-biology/abstract/S0960-9822(24)01716-0) | Hooper SL, et al. | Current Biology | 2025 | — | Passive joint/muscle forces are important in mouse leg movements — measured in anesthetized mice |

### Cat/Locomotion Biomechanics

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [Effects of spinal transection and locomotor speed on muscle synergies of the cat hindlimb](https://physoc.onlinelibrary.wiley.com/doi/abs/10.1113/JP288089) | Klishko AN, et al. | J Physiol | 2025 | 4 | Muscle synergy changes after spinal injury during cat locomotion |
| [Role of forelimb morphology in muscle sensorimotor functions during locomotion in the cat](https://physoc.onlinelibrary.wiley.com/doi/abs/10.1113/JP287448) | Rahmati SM, et al. | J Physiol | 2025 | 3 | How forelimb shape affects sensorimotor function in cat walking |
| [Mechanisms of adaptive interlimb coordination to sudden ground loss: a neuromusculoskeletal modeling study](https://www.biorxiv.org/content/10.1101/2025.11.11.687930.abstract) | Shinohara K, et al. | bioRxiv | 2025 | — | Modeling how animals adapt limb coordination when ground disappears |

### Bio-inspired Robotics

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [Design and Control of a Rat Robot](https://link.springer.com/chapter/10.1007/978-3-032-07448-5_8) | Pham H, Jackson C, Nourse W, Quinn R | Conf Biomimetic and Biohybrid Sys | 2026 | — | Biologically inspired rat robot (2.5x scale) with hindlimbs based on musculoskeletal data |
| [Canonical motor microcircuit for control of a rat hindlimb](https://link.springer.com/chapter/10.1007/978-3-031-20470-8_31) | Jackson C, Nourse WRP, Heckman CJ, et al. | Conf Biomimetic and Biohybrid Sys | 2022 | 5 | Neural circuit-inspired controller for rat hip joint |
| [Design of a rat robotic forelimb](https://link.springer.com/chapter/10.1007/978-3-031-72597-5_17) | Pham H, Jackson CB, et al. | Conf Biomimetic and Biohybrid Sys | 2024 | 1 | Robotic rat forelimb design based on biomechanical data |
| [Neural Circuit Architectural Priors for Quadruped Locomotion](https://arxiv.org/abs/2410.07174) | Bhattasali NX, et al. | ArXiv | 2024 | 2 | Using neural circuit structure as inductive bias for quadruped RL policies |

### Experimental Methods & Morphology

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [High-resolution in vivo kinematic tracking with customized injectable fluorescent nanoparticles](https://www.science.org/doi/abs/10.1126/sciadv.adu9136) | Ulutas EZ, et al. | Sci Adv | 2025 | 2 | Novel kinematic tracking method using fluorescent nanoparticles |
| [Comparative morphology of the whiskers and faces of mice and rats](https://journals.biologists.com/jeb/article/226/19/jeb245597/333454) | Bresee CS, et al. | J Exp Biol | 2023 | 20 | Detailed morphological comparison relevant to whisker simulation models |
| [Distribution of motoneuronal pools controlling forelimb muscles in the cervical spinal cord of Acomys cahirinus](https://anatomypubs.onlinelibrary.wiley.com/doi/abs/10.1002/ar.70096) | Veshchitskii A, et al. | Anat Rec | 2025 | — | Mapped spinal motoneuron pools innervating forelimb muscles |
| [Inductive analysis of the spatial distribution characteristics of neurons that innervate skeletal muscle](https://journals.lww.com/nrronline/fulltext/2026/06000/inductive_analysis_of_the_spatial_distribution.81.aspx) | Gu X, et al. | Neural Regen Res | 2026 | — | Spatial distribution of neurons controlling skeletal muscle and correlation with muscle phenotype |

### Neural Prosthetics & Clinical

| Paper | Authors | Journal | Year | Cited by | Key Contribution |
|-------|---------|---------|------|---------|-----------------|
| [Predictive Modeling of 3D Forelimb Reaching Movements in Mice for Enhanced Closed-Loop Neural Prostheses](https://link.springer.com/chapter/10.1007/978-3-031-77588-8_139) | Wochner I, Picard C, Estebanez L, et al. | ICNR Conference | 2024 | — | Mouse reaching movement prediction for brain-machine interfaces |

### Other (Theses, Paleontology)

| Paper | Authors | Year | Key Contribution |
|-------|---------|------|-----------------|
| [Modeling the neural control of movement with a virtual rodent](https://search.proquest.com/openview/885ee4d73644c1c72e97df3ac0f27383/1?pq-origsite=gscholar&cbl=18750&diss=y) | Aldarondo D | 2024 | PhD thesis (Harvard) — foundation for the Nature 2024 virtual rodent paper |
| [Uncovering neural architectures enabling robust and flexible motor control in Drosophila](https://infoscience.epfl.ch/entities/publication/9c116dd2-84d8-4a2a-ac51-40baa4d4d2ab/files) | Hurtak FI | 2025 | PhD thesis (EPFL) — Drosophila motor control architectures |
| [Biomechanical and neural influences on locomotor gait control in mice](https://discovery.ucl.ac.uk/id/eprint/10207494/) | Mitrevica Z | 2025 | PhD thesis (UCL) — biomechanical + neural gait control in mice |
| [Motor unit control of mouse locomotion](https://repository.gatech.edu/entities/publication/8b31b4c2-e4f5-4bb2-8853-4ed5425fb847) | Thomas K | 2025 | PhD thesis (Georgia Tech) — motor unit neuromuscular control |
| [Modeling and Control of Continuum Appendages](https://deepblue.lib.umich.edu/items/23f215ff-89f8-413c-9593-8263d9fd842d) | Fu X | 2024 | PhD thesis (U Michigan) — modeling tails and flexible appendages |
| [A computational modeling approach to study the neuromechanics of terrestrial locomotion](https://infoscience.epfl.ch/bitstreams/5c7385a1-fa63-4272-80a3-bb280d5fb7eb/download) | Tata Ramalingasetty S | 2022 | PhD thesis (EPFL) — by the original paper's first author |
| [Decoupling fossil trackways from trackmaker identity in locomotion studies](https://www.tandfonline.com/doi/abs/10.1080/10420940.2024.2431023) | Krapovickas V | Ichnos | 2024 | Uses musculoskeletal modeling concepts to infer locomotion of extinct animals from fossil tracks |
| [Biomechanics Simplifies Whisker-Based Tactile Sensing and Motor Control](https://search.proquest.com/openview/2cf659eab475617916ea5a97a938f764/1?pq-origsite=gscholar&cbl=18750&diss=y) | Luo Y | 2023 | PhD thesis — how whisker biomechanics reduces neural control demands |

---

## Case Study: *Drosophila* as the Model for Full Neuromechanical Integration

- The fruit fly is the **nearest prospect** for a fully integrated neuromechanical model.
- Recent completions:
  - **Connectome of the fly brain** (full wiring diagram)
  - **Connectome of the ventral nerve cord** (motor control center)
- These enable **in silico experiments** impossible in living animals.
- Target application: Sensorimotor control during **walking** — how neural circuits integrate feedback from sensory neurons with feedforward motor commands when encountering perturbations (e.g., uneven terrain).

---

## Caution on Foundation Models

- Emerging "foundation models" trained on large neural and video datasets risk **diverging from biological mechanisms**.
- These models learn statistical patterns in data but may not capture the causal structure of embodied control.
- Critical distinction: The brain controls muscles (forces), not joint positions — foundation models that skip this level of description may be biologically misleading.

---

## Key Tensions and Open Questions

- **Do researchers need to model every bodily system simultaneously?** The authors acknowledge this is impractical but argue modularity helps — different subsystems can be modeled at appropriate resolutions and composed.
- **Convergent tools, open datasets, and collaborative science cultures** now make embodied approaches feasible despite the complexity.

---

## Personal Takeaways

- The dead trout example is a vivid illustration of how biomechanics can offload computation from the nervous system — a concrete case of "morphological computation."
- The LGN feedback point is important: even the most "feedforward" sensory pathway is dominated by feedback. This should update priors about how to model any neural circuit.
- *Drosophila* is uniquely positioned because it has both a complete connectome AND tractable biomechanics — the gap between neural wiring and behavior can potentially be fully bridged.
- The warning about foundation models is timely: learning to predict neural data is not the same as understanding how brains control bodies.
