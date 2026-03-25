# Neural Manifolds in Neuroscience: A Thematic Review of Low-Dimensional Population Dynamics

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Search Methodology](#2-search-methodology)
3. [Foundations: The Population Doctrine and Low-Dimensional Structure](#3-foundations)
4. [Dimensionality Reduction Methods: From PCA to Deep Latent Models](#4-methods)
5. [Manifold Geometry, Coding Theory, and Topology](#5-geometry-topology)
6. [Motor Cortex Manifolds and Dynamics](#6-motor)
7. [Sensory Manifolds](#7-sensory)
8. [Cognitive Manifolds: Working Memory, Decision-Making, and Context](#8-cognitive)
9. [Attractor Dynamics and Topological Structure](#9-attractors)
10. [Learning and Plasticity on the Neural Manifold](#10-plasticity)
11. [Computational Models: Low-Rank RNNs and Trained Networks](#11-computational)
12. [Manifold Alignment, Brain-Machine Interfaces, and Cross-Individual Dynamics](#12-alignment-bmi)
13. [Unifying Manifolds and Circuits](#13-unifying)
14. [Discussion: Criticisms, Limitations, and Future Directions](#14-discussion)
15. [References](#15-references)

---

## 1. Introduction {#1-introduction}

A central challenge in systems neuroscience is to understand how the coordinated activity of large populations of neurons gives rise to perception, cognition, and behaviour. Over the past two decades, advances in multi-electrode recording technologies, calcium imaging, and Neuropixels probes have made it possible to simultaneously monitor hundreds to thousands of neurons. A striking empirical finding from these recordings is that although neural activity lives in a high-dimensional space (one dimension per neuron), the population dynamics typically occupy a much lower-dimensional subspace -- a **neural manifold**.

The concept of a neural manifold provides a geometric and dynamical vocabulary for understanding brain computation. Rather than asking what each neuron "represents," the manifold perspective asks how the collective trajectory of the population through state space relates to behaviour, computation, and circuit structure. This framework has proven remarkably productive, yielding insights into motor control, sensory processing, memory, decision-making, navigation, and brain-machine interfaces.

This review surveys the field thematically, covering foundational concepts, methodological advances, applications across brain systems, and the emerging effort to link manifold-level descriptions to the underlying circuit connectivity. We focus on how researchers explain and interpret manifold structure -- the methods used to uncover it, the geometric and dynamical principles that govern it, and the biological implications that follow.

---

## 2. Search Methodology {#2-search-methodology}

### Databases and queries

Systematic searches were conducted across PubMed and Semantic Scholar (S2) in March 2026.

**PubMed queries (all with `--sort date --max 15 --abstract`):**

| # | Query |
|---|-------|
| 1 | "neural manifold population dynamics low-dimensional" |
| 2 | "neural manifold geometry topology brain" |
| 3 | "motor cortex neural manifold latent dynamics" |
| 4 | "sensory cortex neural manifold visual olfactory" |
| 5 | "working memory decision making neural manifold prefrontal" |
| 6 | "continuous attractor manifold head direction grid cells" |
| 7 | "neural manifold learning plasticity brain-machine interface" |
| 8 | "low-rank recurrent neural network manifold connectivity" |
| 9 | "neural manifold alignment preserved dynamics across individuals" |
| 10 | "LFADS CEBRA latent factor neural population" |
| 11 | "topological data analysis persistent homology neural activity" |
| 12 | "neural population geometry optimal coding representational" |
| 13 | "nonlinear manifold neural population activity behavior" |
| 14 | "neural manifold brain-computer interface decoder stability" |
| 15 | "neural circuit manifold connectivity low-rank dynamics" |

**Semantic Scholar queries (relevance-sorted, author-targeted):**

| # | Query |
|---|-------|
| S1 | "Gallego cortical population dynamics preserved across time" |
| S2 | "Churchland Cunningham Shenoy neural population dynamics" |
| S3 | "Ostojic low-rank recurrent network manifold" |
| S4 | "Chung Abbott neural population geometry manifold capacity" |
| S5 | "CEBRA joint embedding behavior neural latent" |

### Screening and selection

A total of approximately 180 unique records were screened. Papers were selected based on relevance to the 16 pre-defined sub-fields, prioritising primary research articles and high-impact reviews. Foundational papers known from domain knowledge were added to ensure comprehensive coverage of the field's intellectual history. The final bibliography contains 95 papers spanning 1997--2026.

---

## 3. Foundations: The Population Doctrine and Low-Dimensional Structure {#3-foundations}

### From single neurons to populations

The classical "neuron doctrine" held that the single neuron is the fundamental computational unit of the brain, and that understanding neural coding requires characterising the tuning properties of individual cells [1]. This approach was enormously productive in sensory systems -- orientation tuning in V1, place cells in hippocampus -- but ran into difficulties in motor cortex, where single neurons exhibit complex, heterogeneous, and often puzzling response profiles.

The shift towards a population-level perspective was catalysed by the recognition that the activity of many neurons is highly correlated, and that these correlations carry information about the computation being performed [2,3]. Cunningham and Yu [2] provided an influential review arguing that dimensionality reduction should be the standard first step in analysing neural population data, because the intrinsic dimensionality of the population activity is typically far lower than the number of recorded neurons.

### The neural manifold hypothesis

The neural manifold hypothesis states that task-relevant neural computation is carried out by dynamics confined to a low-dimensional subspace -- the manifold -- embedded in the high-dimensional space of all possible activity patterns [2,3,4]. This low-dimensional structure arises because neurons share common inputs, are recurrently connected, and are constrained by the dynamics of the circuit. The manifold is not merely a convenient summary; it reflects genuine constraints on what patterns of co-activation the circuit can produce.

Shenoy, Sahani, and Churchland [3] articulated the "dynamical systems" perspective on motor cortex, arguing that neural activity should be understood not as representing movement parameters, but as the time-varying state of a dynamical system whose evolution is governed by the circuit's recurrent connectivity. This view naturally leads to the manifold framework: the state trajectory lives on a low-dimensional manifold determined by the system's dynamics.

### Empirical evidence for low dimensionality

Empirical studies consistently find that neural population activity during behaviour can be well approximated by a small number of latent dimensions, typically 5-15 for motor tasks and 10-30 for more complex cognitive tasks [2,5]. This low dimensionality has been observed across species (rodents, primates, songbirds, C. elegans), brain areas (motor cortex, prefrontal cortex, hippocampus, visual cortex), and recording modalities (multi-electrode arrays, calcium imaging, ECoG) [4,5,6].

Mitchell-Heggs et al. [4] provided a comprehensive review of neural manifold analysis methods for studying brain circuit dynamics, covering both healthy and disease states. They noted that while manifold methods have been transformative, the field needs more rigorous methods for estimating the true intrinsic dimensionality of neural data. Altan et al. [7] addressed this directly, developing methods for estimating manifold dimensionality from multi-electrode recordings and showing that dimensionality estimates are sensitive to noise, trial averaging, and the time window of analysis.

### High dimensionality and low dimensionality are compatible

An important recent contribution by Schmutz et al. [8] demonstrated analytically that high-dimensional neuronal activity and low-dimensional latent dynamics can be "two sides of the same coin." Using a solvable recurrent neural network model, they showed that low-rank connectivity can produce latent dynamics on a low-dimensional manifold while the full neuronal activity is high-dimensional, because individual neurons combine a shared low-dimensional signal with private, high-dimensional variability. This resolves an apparent tension between large-scale recording studies showing high-dimensional activity and the manifold framework's emphasis on low-dimensional dynamics.

---

## 4. Dimensionality Reduction Methods: From PCA to Deep Latent Models {#4-methods}

### Linear methods

The simplest approach to identifying neural manifolds is principal component analysis (PCA), which finds the orthogonal directions of maximum variance in the population activity. PCA has been widely used since the earliest multi-electrode studies and remains a standard first-pass analysis [2].

Gaussian Process Factor Analysis (GPFA) [9] extends PCA by incorporating temporal smoothness, modelling the latent factors as Gaussian processes. This yields smoother single-trial trajectories and provides a principled way to separate signal from noise. GPFA was instrumental in revealing the rotational dynamics in motor cortex discovered by Churchland et al. [10].

Demixed PCA (dPCA) [11] addresses the problem of mixed selectivity by decomposing population activity into components that are associated with specific task variables (e.g., stimulus identity vs. time), while remaining linear and computationally simple. dPCA has been widely adopted for cognitive neuroscience data where neurons encode multiple variables simultaneously.

### Nonlinear methods and deep learning

Linear methods assume the manifold is a flat subspace, but neural manifolds are often curved. De and Chaudhuri [12] proved analytically that common population codes (such as neurons with localised tuning curves encoding a circular variable) produce manifolds that are extremely nonlinear -- so curved that linear dimensionality reduction requires far more dimensions than the manifold's intrinsic dimensionality. Fortunato et al. [13] provided direct experimental evidence that nonlinear manifolds underlie neural population activity during behaviour, showing that nonlinear methods can capture structure missed by PCA.

**LFADS (Latent Factor Analysis via Dynamical Systems)** [14] represented a paradigm shift by using a sequential variational autoencoder to infer single-trial latent dynamics. LFADS models the latent state as evolving according to a nonlinear dynamical system, with the observed spike counts generated from the latent state through a Poisson observation model. It has been widely adopted for motor cortex data, revealing dynamics obscured by trial-to-trial variability.

**CEBRA (Consistent Embeddings of high-dimensional Recordings using Auxiliary variables)** [15] takes a different approach, using contrastive learning to produce latent embeddings that are jointly informed by neural and behavioural data. CEBRA can operate in a supervised mode (using behavioural labels) or a self-supervised mode (using temporal structure alone). It has demonstrated the ability to produce consistent latent spaces across subjects and sessions, and to decode variables such as position from hippocampal recordings at state-of-the-art accuracy.

**MARBLE (Manifold Analysis with Representation learning By Lie symmetries and Equivariance)** [16] introduced geometric deep learning to the problem of neural manifold analysis. MARBLE decomposes on-manifold dynamics into local flow fields and maps them into a common latent space using unsupervised learning on the manifold's tangent bundle. This approach is explicitly designed to respect the manifold's geometry, yielding interpretable and consistent representations across conditions and subjects.

Other nonlinear approaches include variational autoencoders (VAEs) [17], UMAP for visualisation, and the extended Poisson-GPLVM for unsupervised decoding of hippocampal data [18]. Abbaspourazad et al. [19] developed DFINE, a method that models nonlinear latent dynamics while allowing flexible causal and non-causal inference, addressing the practical need for methods that work in real-time BCI applications.

---

## 5. Manifold Geometry, Coding Theory, and Topology {#5-geometry-topology}

### Neural population geometry

The geometry of neural manifolds -- their shape, curvature, dimensionality, and relative arrangement -- carries information about the computations being performed. Chung and Abbott [20] developed the "neural population geometry" framework, which provides quantitative tools for relating the geometric properties of neural representations to computational capacity. A key concept is **manifold capacity**: the number of object manifolds that can be linearly separated by a downstream readout, which depends on the manifolds' dimensionality and radius.

Chung, Lee, and Sompolinsky [21] derived a theory of perceptual manifold classification, showing that the capacity of a linear classifier to separate object manifolds depends on their geometry -- specifically, their dimensionality and extent. This theory was applied to deep neural networks by Cohen et al. [22], who showed that successive layers progressively reduce manifold dimensionality and radius, "untangling" representations to increase classification capacity. Froudarakis et al. [23] applied this framework to the mouse visual hierarchy, finding that object manifolds become more compact and separable as one ascends the cortical hierarchy.

Wakhloo, Slatton, and Chung [24] extended the population geometry framework to tasks with shared latent structure, analytically determining which geometric properties of neural activity govern generalisation across contexts. Chou et al. [25] developed a framework linking "untangling efficiency" to neural population geometry, connecting the visualisation of neural trajectories to quantitative measures of computational performance.

### Orthogonal geometry and representational structure

A recurring finding is that neural representations of different task variables are often arranged in approximately orthogonal subspaces. Wang et al. [26] found orthogonal neural geometry of orientation, spatial frequency, and ocular dominance in macaque V1. This orthogonality enables independent readout of each variable without interference, a computational advantage formalised by the population geometry framework.

### Topological data analysis

While geometry captures the shape of manifolds, **topology** captures their qualitative structural features -- the number and type of "holes." Persistent homology, the primary tool of topological data analysis (TDA), identifies topological features that persist across spatial scales, providing robust signatures of manifold structure [27,28].

Gardner et al. [29] applied persistent cohomology to grid cell recordings in the medial entorhinal cortex of freely moving rats and discovered that the population activity of grid cells lies on a toroidal manifold -- a torus in neural state space. This was a landmark finding because it provided direct evidence for the continuous attractor model of grid cells and demonstrated that the topology of the neural manifold matches the mathematical structure predicted by theory.

Kang, Xu, and Morozov [28] systematically evaluated persistent cohomology for discovering the topology of spatial representations, showing that it reliably recovers the ring topology of head direction cells, the torus of grid cells, and the sphere of conjunctive cells, but requires sufficient data and careful parameter choices.

Yoon et al. [30] extended topological methods to track manifold structure across populations, developing tools for comparing the topology of neural manifolds in different brain regions or between recorded and simulated populations. Beshkov and Tiesinga [31] showed that geodesic-based distance metrics can reveal nonlinear topological features in visual cortex data that standard persistent homology might miss.

Bardin, Spreemann, and Hess [32] applied persistent homology to artificial neural network dynamics, demonstrating that topological methods can characterise the global structure of network dynamics in ways that complement traditional dynamical systems analysis.

---

## 6. Motor Cortex Manifolds and Dynamics {#6-motor}

### The dynamical systems revolution in motor neuroscience

The motor cortex has been the primary testing ground for the neural manifold framework. Churchland et al. [10] recorded from populations of neurons in monkey motor and premotor cortex during reaching and discovered that the dominant pattern of population activity during movement is a rotation in neural state space. These rotational dynamics were not expected from any model in which neurons simply encode movement parameters; rather, they emerge naturally from the dynamics of a recurrent network.

Shenoy, Sahani, and Churchland [3] synthesised this into a comprehensive dynamical systems view of motor cortex: neural activity during motor preparation sets the initial condition for a dynamical system, and the subsequent trajectory through state space generates the time-varying muscle commands. This framework was validated by Kao et al. [33], who showed that dynamical models could predict single-trial neural activity and improve brain-machine interface decoding.

### Preserved manifold structure across tasks and time

Gallego et al. [34] demonstrated that the neural manifold in motor cortex is preserved across different motor behaviours. While each task requires different patterns of muscle and single-neuron activity, the same low-dimensional "neural modes" (the principal axes of the manifold) are shared across tasks. The manifold is partitioned into task-specific subregions, but its overall structure is common -- analogous to different melodies played on the same instrument.

Gallego et al. [35] further showed that cortical population dynamics are stable over weeks to months, even as individual neurons change their firing rates. The low-dimensional manifold and the dynamics on it are preserved, providing a stable neural correlate for consistent behaviour despite representational drift. Abdulla et al. [36] confirmed and extended this, finding that manifold stability holds even at minimal dimensionality, and proposed a framework for extracting labelled latent variables that maintain a fixed relationship to behaviour.

### Human motor cortex and the grasp network

Natraj et al. [37] used electrocorticography to study the human "grasp network" spanning motor, premotor, and somatosensory cortex. They found a common multi-area manifold that represents both finger individuation and grasping movements, with different movement types occupying compartmentalised regions of the shared manifold.

### Songbird vocal motor cortex

Tostado-Marcos et al. [38] extended the population dynamics framework to songbirds, recording from vocal motor regions (HVC and RA) during singing. They found that both regions exhibit low-dimensional population dynamics, with RA showing rotational structure similar to primate motor cortex. This cross-species conservation of dynamical motifs supports the generality of the manifold framework.

### Premotor cortex and rhythmic timing

Dotov et al. [39] investigated neural manifolds in the macaque medial premotor cortex during rhythmic tapping synchronised to a metronome. They found low-dimensional manifolds capturing the transition from attending to the rhythm to actively synchronising, demonstrating that manifold dynamics can capture the temporal structure of sensorimotor coordination.

### Bayesian computation in motor timing

Sohn et al. [40] showed that neural population dynamics in motor cortex implement Bayesian computation during a time-interval reproduction task. Prior statistics warp the geometry of the neural manifold, biasing the neural trajectory towards intervals consistent with the prior distribution. This provided evidence that manifold-level dynamics implement probabilistic inference.

---

## 7. Sensory Manifolds {#7-sensory}

### Visual cortex

Sensory neural manifolds encode the features of stimuli. In the visual system, the key question is how the geometry of neural representations changes across the cortical hierarchy. Froudarakis et al. [23] measured object manifold geometry across the mouse cortical visual hierarchy and found progressive untangling: manifolds become more compact and linearly separable in higher areas, consistent with the theoretical framework of Chung and colleagues [20,21].

Wang et al. [26] characterised the neural geometry of orientation, spatial frequency, and ocular dominance in macaque V1 at the population level, finding orthogonal coding axes for these features. This orthogonal arrangement maximises the information that can be independently extracted about each feature.

### Olfactory system

The olfactory system provides a striking example of manifold structure. Friedrich and colleagues [41] studied how odour representations in zebrafish undergo experience-dependent restructuring during learning, using manifold geometry analysis. They found that learning reshapes the geometry of stimulus manifolds in the olfactory memory network, optimising the manifold capacity for discriminating learned odours.

### Auditory cortex

Runfola et al. [42] used intracranial recordings to study neural dynamics during speech and music listening. Using a "Manifold Density Flow" method, they characterised the complexity of brain dynamics on the neural manifold and found that speech and music evoke higher complexity dynamics than the resting state, with region-specific patterns reflecting specialised processing.

### C. elegans whole-brain imaging

Liang et al. [43] used whole-brain calcium imaging in C. elegans to study how aversive olfactory learning reorganises neural dynamics. They found that learning induces a global reorganisation of the neural manifold, context-gated by the animal's internal state. This demonstrates that manifold-level changes can capture learning at the whole-brain scale even in a small nervous system.

---

## 8. Cognitive Manifolds: Working Memory, Decision-Making, and Context {#8-cognitive}

### Prefrontal cortex and working memory

The prefrontal cortex (PFC) is a key site for studying cognitive manifolds because it encodes stimuli, task rules, and decisions simultaneously. Mante et al. [44] showed that PFC population activity in monkeys performing a context-dependent decision task is well described by low-dimensional dynamics in which context, sensory evidence, and choice are represented along approximately orthogonal axes. An input-driven selection mechanism gates which sensory evidence drives the decision trajectory.

Pu et al. [45] asked whether the manifold dynamics observed during cognitive tasks reflect task demands or intrinsic cortical dynamics. They found that rotations of stimulus representations occur in the low-dimensional activity space of prefrontal neurons in naive monkeys passively viewing stimuli -- without any task demands. This suggests that some manifold transformations are intrinsic to cortical circuitry rather than being specifically recruited for task computation.

### Mixed selectivity and abstract representations

Bernardi et al. [46] showed that prefrontal neurons exhibit high-dimensional, abstract representations that enable generalisation across tasks. The geometry of these representations -- specifically, their dimensionality and the arrangement of coding subspaces -- determines the brain's ability to flexibly apply learned rules to new situations. This high-dimensional geometry is distinct from the low-dimensional task-specific manifolds and may reflect a complementary coding strategy.

### Context-dependent computation

Zhang, Liu, and Chen [47] used trained RNNs to explore how context rules are encoded, maintained, and applied in a decision-making task. They found that the RNN learns a geometric structure in which context information creates separate manifolds for each context, enabling the same sensory input to drive different decisions depending on the active manifold. This provides a geometric account of flexible cognition.

---

## 9. Attractor Dynamics and Topological Structure {#9-attractors}

### Continuous attractors

Many cognitive and navigational functions require maintaining persistent states -- a remembered position, a head direction, an evidence accumulation signal. Continuous attractor networks provide a theoretical framework in which a continuum of stable states (the attractor manifold) enables this persistent activity [48].

The head direction system is the canonical example: neurons in the head direction circuit maintain a stable "bump" of activity whose position on a ring corresponds to the animal's heading. Chaudhuri et al. [48] developed a theory for how continuous attractor dynamics emerge from recurrent connectivity, showing that the geometry of the attractor manifold is determined by the structure of the weight matrix.

### Toroidal manifold of grid cells

Gardner et al. [29] provided the most dramatic demonstration of manifold topology in the brain. Using persistent cohomology applied to Neuropixels recordings of grid cells in rat medial entorhinal cortex, they showed that the population activity lies on a torus -- a manifold with the topology of a doughnut. This toroidal structure is precisely what is predicted by continuous attractor models of grid cells, in which the phase of the grid pattern is represented by a two-dimensional periodic variable.

This finding was significant for several reasons: it demonstrated that topological analysis can reveal structure in neural data that is invisible to linear methods; it confirmed a specific prediction of computational theory; and it showed that the brain implements geometric structures at the population level that have direct functional meaning.

### Trained manifold attractors

Darshan and Rivkind [49] developed a theory for manifold attractors in trained neural networks, showing that training can produce continuous attractor manifolds even in networks with heterogeneous, asymmetric connectivity. This reconciles the theoretical framework of continuous attractors (which traditionally requires symmetric connectivity) with the biological reality of diverse, irregular synaptic connections.

### Universal computations through manifold dynamics

Gort [50] provided a theoretical analysis showing that neural manifold dynamics can implement "universal computations" -- that the topology and geometry of the manifold, combined with the flow structure on it, determines the computational repertoire of a neural population. This suggests that the manifold is not merely a low-dimensional summary but a substrate for flexible computation.

---

## 10. Learning and Plasticity on the Neural Manifold {#10-plasticity}

### Within-manifold and outside-manifold learning

Sadtler et al. [51] established a foundational paradigm for studying learning on the neural manifold using a brain-machine interface (BMI). They showed that subjects could rapidly learn new neural-to-cursor mappings that lay within the existing neural manifold (i.e., required only reweighting existing patterns of co-activation) but struggled to learn mappings that required moving outside the manifold (i.e., generating new patterns of co-activation not seen in spontaneous activity). This provided direct evidence that the manifold constrains learning.

Feulner and Clopath [52] modelled manifold plasticity during goal-driven learning, showing that synaptic plasticity rules can reshape the neural manifold when within-manifold adaptation is insufficient. Their model predicts that outside-manifold learning requires longer timescales and different plasticity mechanisms than within-manifold learning.

### BCI learning and manifold deformation

Athalye et al. [53] studied de novo neuroprosthetic learning and found that skill acquisition involves the progressive consolidation of neural population dynamics, with the manifold becoming more structured and lower-dimensional as performance improves. Iwama, Zhang, and Ushiba [54] showed that BCI learning in humans deforms the manifold of population activity patterns, with the manifold expanding to include new activity patterns needed for the novel task.

### Manifold stability despite representational drift

A key finding is that the neural manifold is stable even as individual neurons drift in their tuning [35,36]. This suggests that the manifold reflects circuit-level constraints (connectivity, excitation-inhibition balance) that are more stable than the firing properties of individual neurons. From a learning perspective, this means that plasticity at the level of individual synapses can occur without disrupting the manifold-level computations, as long as the changes are confined to rotations within the manifold.

### Manifold plasticity in C. elegans and zebrafish

Liang et al. [43] showed that aversive learning in C. elegans produces a global reorganisation of the neural manifold, demonstrating that even in small nervous systems, learning operates at the manifold level. Friedrich et al. [41] found that olfactory learning in zebrafish reshapes stimulus manifold geometry to optimise discrimination, providing a developmental and learning perspective on manifold structure.

---

## 11. Computational Models: Low-Rank RNNs and Trained Networks {#11-computational}

### The low-rank RNN framework

A major theoretical advance has been the development of low-rank recurrent neural networks (RNNs) as analytically tractable models of neural population dynamics [55,56]. In these models, the connectivity matrix is the sum of a small number of rank-one components, which directly constrains the population activity to a low-dimensional manifold. Mastrogiuseppe and Ostojic [55] showed that this low-rank structure enables an exact analytical mapping from connectivity to dynamics: the rank of the connectivity determines the dimensionality of the manifold, and the structure of the rank-one components determines the geometry of the dynamics on it.

Beiran et al. [56] extended this framework to networks with multiple statistically defined populations, showing how the interaction between population structure and low-rank connectivity shapes the manifold dynamics. Schuessler et al. [57] studied the interplay between structured (low-rank) and random connectivity components, showing that random connectivity can enrich the dynamics on the manifold without destroying its low-dimensional structure.

### From connectivity to manifold geometry

Cimesa, Ciric, and Ostojic [58] extended the low-rank framework to spiking networks, showing that the geometry of population activity in spiking networks with low-rank structure can be analytically predicted. Herbert and Ostojic [59] studied the impact of sparse connectivity in low-rank RNNs, showing that sparsity modifies the manifold dynamics in ways that depend on the relationship between the low-rank structure and the sparsity pattern.

Pezon, Schmutz, and Gerstner [60] made a major contribution by linking neural manifolds to circuit structure in spiking recurrent networks. They connected three levels of description -- circuit structure (the weight matrix), single-neuron functional properties (tuning curves), and low-dimensional population dynamics (the manifold) -- providing a bridge between the manifold perspective and the circuit perspective.

### Relationship to latent dynamical systems models

Valente, Ostojic, and Pillow [61] probed the relationship between latent linear dynamical system (LDS) models and low-rank RNNs, showing that these two approaches to modelling low-dimensional dynamics are closely related but not equivalent. Low-rank RNNs can produce nonlinear dynamics that LDS models cannot capture, but when the dynamics are approximately linear, the two frameworks converge.

### Trained RNNs as models of computation

Beyond analytically tractable low-rank models, RNNs trained on cognitive tasks have become important tools for generating hypotheses about neural computation. Vyas et al. [5] reviewed "computation through neural population dynamics," arguing that trained RNNs provide a framework for understanding how neural populations implement computations through their manifold dynamics. The dynamical motifs discovered in trained RNNs -- rotations, line attractors, saddle points -- have been found in neural data, validating the approach.

---

## 12. Manifold Alignment, Brain-Machine Interfaces, and Cross-Individual Dynamics {#12-alignment-bmi}

### Preserved dynamics across individuals

A striking finding is that the manifold dynamics are preserved not only across time within an individual but across individuals of the same species performing similar behaviour. Safaie et al. [62] recorded neural populations from motor cortex of multiple monkeys and mice performing similar motor tasks and found that the latent dynamics are remarkably similar across individuals, despite differences in the specific neurons recorded. This suggests that the manifold dynamics reflect species-level constraints on neural circuit organisation, shaped by evolution and development.

### Manifold alignment for stable BCIs

Brain-machine interfaces (BMIs) face the challenge of neural instability: as neurons are lost or gained across recording sessions, the mapping from neural activity to cursor control degrades. The manifold perspective offers a solution: if the underlying manifold is stable, then aligning new recordings to the manifold should restore decoding accuracy.

Karpowicz et al. [63] demonstrated this approach, showing that aligning latent dynamics across sessions stabilises iBCI performance without requiring supervised recalibration. Their method, SABLE (Stabilization Alignment By Latent Embeddings), uses LFADS to extract latent dynamics and then aligns them across sessions, enabling continuous iBCI use over extended periods in people with paralysis.

Ganjali et al. [64] developed unsupervised manifold alignment methods for stable motor decoding, using dimensionality reduction and correlation-based alignment to transfer decoders across sessions. Ma et al. [65] used adversarial networks to adapt decoders to neural drift, framing the problem as domain adaptation on the manifold.

### Long-term neuroprosthetic control

Natraj et al. [66] demonstrated that the neural manifold for simple imagined movements is remarkably stable over days in human ECoG-BCI users, enabling long-term neuroprosthetic control. By sampling the representational plasticity of the manifold, they achieved stable BCI performance without frequent recalibration.

### EEG-based manifold analysis for stroke rehabilitation

Liu et al. [67] introduced methods for identifying low-dimensional manifold structure in EEG recordings from stroke patients during motor imagery, showing that manifold structure can reveal neural reorganisation and predict rehabilitation outcomes. This extends the manifold framework from invasive recordings to non-invasive clinical applications.

---

## 13. Unifying Manifolds and Circuits {#13-unifying}

### The gap between manifolds and circuits

A central open question is how the low-dimensional manifold dynamics observed in neural recordings relate to the specific circuit elements (cell types, synaptic connections, neuromodulatory inputs) that produce them. Langdon, Genkin, and Engel [68] provided an important review arguing that the manifold perspective and the circuit perspective are complementary and should be unified. The manifold perspective identifies *what* computations the population performs; the circuit perspective explains *how* those computations are implemented.

### Linking connectivity to manifold structure

The low-rank RNN framework [55,56,58,60] provides one path towards this unification: if the connectivity matrix determines the manifold, then measuring the connectivity should predict the manifold structure, and vice versa. Pezon et al. [60] demonstrated this link in spiking networks, showing that the eigenvectors of the connectivity matrix define the manifold's axes and the eigenvalues determine the dynamics on them.

Dura-Bernal et al. [69] developed a detailed biophysical model of mouse primary motor cortex with over 10,000 neurons and 30 million synapses, constrained by experimental data on cell types, connectivity, and morphology. The model reproduces cell-type-specific dynamics during behaviour, providing a bridge between detailed circuit models and population-level manifold dynamics.

### Embodied sensorimotor control

Almani et al. [70] reviewed computational models of sensorimotor control that integrate population-level manifold dynamics with the biomechanics of the body and the anatomical loops connecting cortex, subcortical regions, and spinal cord. This "embodied" perspective highlights that neural manifolds must be understood not in isolation but as part of a closed-loop system interacting with the environment.

---

## 14. Discussion: Criticisms, Limitations, and Future Directions {#14-discussion}

### Criticisms and limitations

The neural manifold framework, despite its successes, faces several important criticisms.

**Descriptive vs. mechanistic.** Manifold analysis is primarily descriptive: it reveals the geometric structure of population activity but does not, by itself, explain the mechanisms that produce that structure. The link to circuit mechanisms remains an active area of research [60,68], and the risk of "manifold washing" -- where any dataset is reduced to a pretty low-dimensional plot without genuine insight -- is real.

**Linearity assumption.** Most widely used methods (PCA, GPFA, dPCA) assume linear manifolds. De and Chaudhuri [12] showed that common population codes produce extremely nonlinear manifolds, suggesting that linear methods may miss important structure. Fortunato et al. [13] provided empirical evidence that nonlinear methods reveal behaviourally relevant structure missed by PCA. The field is moving towards nonlinear methods [14,15,16,19], but these are more complex and harder to interpret.

**Dimensionality estimation.** The intrinsic dimensionality of the neural manifold is not straightforward to estimate [7]. Different methods can yield different answers, and the "true" dimensionality depends on the definition used. Altan et al. [7] showed that dimensionality estimates depend on noise, binning, and analysis parameters, suggesting that reported dimensionality values should be interpreted with caution.

**High-dimensional structure.** While manifold methods focus on the dominant low-dimensional structure, high-dimensional "residual" activity may carry important information. Bernardi et al. [46] showed that high-dimensional abstract representations in PFC enable generalisation. The relationship between low-dimensional manifold dynamics and high-dimensional coding remains to be fully elucidated [8].

**Observational confound.** The manifold is defined by the population of neurons that happen to be recorded. Different recording configurations (different neurons, different brain areas) will yield different manifolds. It is unclear to what extent the observed manifold reflects the brain's computation vs. the sampling bias of the recording.

### Future directions

Several exciting directions are emerging:

1. **Circuit-manifold links.** Combining cell-type-specific recordings (e.g., Neuropixels with optogenetic tagging) with manifold analysis will enable researchers to map how specific cell types contribute to manifold structure [60,68,69].

2. **Multi-area manifolds.** As multi-region recording becomes routine, understanding how manifolds in different brain areas are coordinated -- through shared dimensions, communication subspaces, or topological alignment -- will be critical [37,62,70].

3. **Development.** How do neural manifolds emerge during development? What is the interplay between genetically specified connectivity, activity-dependent plasticity, and experience in shaping manifold structure? This remains largely unexplored.

4. **Clinical applications.** Neural manifold analysis is beginning to be applied to clinical data, including stroke rehabilitation [67], epilepsy detection [71], and neurodegenerative disease. Manifold-based biomarkers could provide new diagnostic and prognostic tools.

5. **Nonlinear and topological methods.** The development of principled nonlinear methods (LFADS, CEBRA, MARBLE) and topological methods (persistent homology) will enable the characterisation of manifold structures that linear methods cannot access. Scaling these methods to the thousands of neurons now routinely recorded is an active technical challenge.

6. **Manifold control.** Fehrman and Meliza [72] introduced model predictive control on the neural manifold, using closed-loop stimulation to drive neural population activity along desired manifold trajectories. This approach could transform the manifold framework from observational to interventional, enabling direct tests of causal hypotheses.

7. **Theoretical foundations.** A complete theory linking connectivity, dynamics, geometry, and computation remains elusive. The low-rank RNN framework [55,56] provides a start, but extending it to biologically realistic spiking networks with heterogeneous cell types and complex connectivity is an ongoing challenge.

---

## 15. References {#15-references}

1. Kalaska, J.F. Emerging ideas and tools to study the emergent properties of the cortical neural circuits for voluntary motor control in non-human primates. *F1000Research* **8**, 749 (2019). https://doi.org/10.12688/f1000research.17161.1

2. Cunningham, J.P. & Yu, B.M. Dimensionality reduction for large-scale neural recordings. *Nat. Neurosci.* **17**, 1500--1509 (2014). https://doi.org/10.1038/nn.3776

3. Shenoy, K.V., Sahani, M. & Churchland, M.M. Cortical control of arm movements: a dynamical systems perspective. *Annu. Rev. Neurosci.* **36**, 337--359 (2013). https://doi.org/10.1146/annurev-neuro-062111-150509

4. Mitchell-Heggs, R., Prado, S., Gava, G.P., Go, M.A. & Schultz, S.R. Neural manifold analysis of brain circuit dynamics in health and disease. *J. Comput. Neurosci.* **51**, 1--21 (2023). https://doi.org/10.1007/s10827-022-00839-3

5. Vyas, S., Golub, M.D., Sussillo, D. & Shenoy, K.V. Computation through neural population dynamics. *Annu. Rev. Neurosci.* **43**, 249--275 (2020). https://doi.org/10.1146/annurev-neuro-092619-094115

6. Shenoy, K.V. & Kao, J.C. Measurement, manipulation and modeling of brain-wide neural population dynamics. *Nat. Commun.* **12**, 633 (2021). https://doi.org/10.1038/s41467-020-20371-1

7. Altan, E., Solla, S.A., Miller, L.E. & Perreault, E.J. Estimating the dimensionality of the manifold underlying multi-electrode neural recordings. *PLoS Comput. Biol.* **17**, e1008591 (2021). https://doi.org/10.1371/journal.pcbi.1008591

8. Schmutz, V. et al. High-dimensional neuronal activity from low-dimensional latent dynamics: a solvable model. *bioRxiv* 2025.06.03.657632 (2025). https://doi.org/10.1101/2025.06.03.657632

9. Yu, B.M. et al. Gaussian-process factor analysis for low-dimensional single-trial analysis of neural population activity. *J. Neurophysiol.* **102**, 614--635 (2009). https://doi.org/10.1152/jn.90941.2008

10. Churchland, M.M. et al. Neural population dynamics during reaching. *Nature* **487**, 51--56 (2012). https://doi.org/10.1038/nature11129

11. Kobak, D. et al. Demixed principal component analysis of neural population data. *eLife* **5**, e10989 (2016). https://doi.org/10.7554/eLife.10989

12. De, A. & Chaudhuri, R. Common population codes produce extremely nonlinear neural manifolds. *Proc. Natl Acad. Sci. USA* **120**, e2305853120 (2023). https://doi.org/10.1073/pnas.2305853120

13. Fortunato, C. et al. Nonlinear manifolds underlie neural population activity during behaviour. *bioRxiv* 2023.07.18.549575 (2024). https://doi.org/10.1101/2023.07.18.549575

14. Pandarinath, C. et al. Inferring single-trial neural population dynamics using sequential auto-encoders. *Nat. Methods* **15**, 805--815 (2018). https://doi.org/10.1038/s41592-018-0109-9

15. Schneider, S., Lee, J.H. & Mathis, M.W. Learnable latent embeddings for joint behavioural and neural analysis. *Nature* **617**, 360--368 (2023). https://doi.org/10.1038/s41586-023-06031-6

16. Gosztolai, A. et al. MARBLE: interpretable representations of neural population dynamics using geometric deep learning. *Nat. Methods* **22**, 291--300 (2025). https://doi.org/10.1038/s41592-024-02582-2

17. Kingma, D.P. & Welling, M. Auto-encoding variational Bayes. *Proc. 2nd Int. Conf. Learn. Represent.* (2014). https://doi.org/10.48550/arXiv.1312.6114

18. Luo, D.D., Giri, B., Diba, K. & Kemere, C. Extended Poisson Gaussian-process latent variable model for unsupervised neural decoding. *Neural Comput.* **36**, 1449--1475 (2024). https://doi.org/10.1162/neco_a_01685

19. Abbaspourazad, H., Erturk, E., Pesaran, B. & Shanechi, M.M. Dynamical flexible inference of nonlinear latent factors and structures in neural population activity. *Nat. Biomed. Eng.* **8**, 85--104 (2024). https://doi.org/10.1038/s41551-023-01106-1

20. Chung, S. & Abbott, L.F. Neural population geometry: an approach for understanding biological and artificial neural networks. *Curr. Opin. Neurobiol.* **70**, 137--144 (2021). https://doi.org/10.1016/j.conb.2021.10.010

21. Chung, S., Lee, D.D. & Sompolinsky, H. Classification and geometry of general perceptual manifolds. *Phys. Rev. X* **8**, 031003 (2018). https://doi.org/10.1103/PhysRevX.8.031003

22. Cohen, U., Chung, S., Lee, D.D. & Sompolinsky, H. Separability and geometry of object manifolds in deep neural networks. *Nat. Commun.* **11**, 746 (2020). https://doi.org/10.1038/s41467-020-14578-5

23. Froudarakis, E. et al. Object manifold geometry across the mouse cortical visual hierarchy. *bioRxiv* 2020.08.20.258798 (2020). https://doi.org/10.1101/2020.08.20.258798

24. Wakhloo, A.J., Slatton, W. & Chung, S. Neural population geometry and optimal coding of tasks with shared latent structure. *Nat. Neurosci.* **29**, 639--649 (2026). https://doi.org/10.1038/s41593-025-02183-y

25. Chou, C.-N. et al. Geometry linked to untangling efficiency reveals structure and computation in neural populations. *bioRxiv* 2024.02.26.582157 (2025). https://doi.org/10.1101/2024.02.26.582157

26. Wang, X., Zhang, S.-H., Tang, S.-M. & Yu, C. Orthogonal neural geometry of orientation, spatial frequency, and ocular dominance in macaque V1. *Prog. Neurobiol.* **241**, 102874 (2026). https://doi.org/10.1016/j.pneurobio.2025.102874

27. Bardin, J.-B., Spreemann, G. & Hess, K. Topological exploration of artificial neuronal network dynamics. *Netw. Neurosci.* **3**, 725--743 (2019). https://doi.org/10.1162/netn_a_00080

28. Kang, L., Xu, B. & Morozov, D. Evaluating state space discovery by persistent cohomology in the spatial representation system. *Front. Comput. Neurosci.* **15**, 616748 (2021). https://doi.org/10.3389/fncom.2021.616748

29. Gardner, R.J. et al. Toroidal topology of population activity in grid cells. *Nature* **602**, 123--128 (2022). https://doi.org/10.1038/s41586-021-04268-7

30. Yoon, I.H.R. et al. Tracking the topology of neural manifolds across populations. *Proc. Natl Acad. Sci. USA* **121**, e2407997121 (2024). https://doi.org/10.1073/pnas.2407997121

31. Beshkov, K. & Tiesinga, P. Geodesic-based distance reveals nonlinear topological features in neural activity from mouse visual cortex. *Biol. Cybern.* **116**, 53--68 (2022). https://doi.org/10.1007/s00422-021-00906-5

32. Kao, J.C. et al. Single-trial dynamics of motor cortex and their applications to brain-machine interfaces. *Nat. Commun.* **6**, 7759 (2015). https://doi.org/10.1038/ncomms8759

34. Gallego, J.A. et al. Cortical population activity within a preserved neural manifold underlies multiple motor behaviors. *Nat. Commun.* **9**, 4233 (2018). https://doi.org/10.1038/s41467-018-06560-z

35. Gallego, J.A., Perich, M.G., Chowdhury, R.H., Solla, S.A. & Miller, L.E. Long-term stability of cortical population dynamics underlying consistent behavior. *Nat. Neurosci.* **23**, 260--270 (2020). https://doi.org/10.1038/s41593-019-0555-4

36. Abdulla, M.U. et al. Stability of neural manifolds at minimal dimensionality despite motor representational drift. *bioRxiv* 2026.01.30.702162 (2026). https://doi.org/10.64898/2026.01.30.702162

37. Natraj, N., Silversmith, D.B., Chang, E.F. & Ganguly, K. Compartmentalized dynamics within a common multi-area mesoscale manifold represent a repertoire of human hand movements. *Neuron* **110**, 154--174 (2022). https://doi.org/10.1016/j.neuron.2021.10.002

38. Tostado-Marcos, P. et al. Neural population dynamics in songbird RA and HVC during learned motor-vocal behavior. *ArXiv* (2024). https://pubmed.ncbi.nlm.nih.gov/39040642/

39. Dotov, D., Betancourt, A., Gamez, J. & Merchant, H. Manifold properties in the macaque medial premotor cortex during switching from attending to tapping to a metronome. *bioRxiv* 2025.10.07.681062 (2025). https://doi.org/10.1101/2025.10.07.681062

40. Sohn, H., Narain, D., Meirhaeghe, N. & Jazayeri, M. Bayesian computation through cortical latent dynamics. *Neuron* **104**, 785--801 (2019). https://doi.org/10.1016/j.neuron.2019.06.012

41. Friedrich, R.W. et al. Representational learning by optimization of neural manifolds in an olfactory memory network. *Res. Sq.* (2025). https://doi.org/10.21203/rs.3.rs-6155477/v1

42. Runfola, C. et al. Complexity in speech and music listening via neural manifold flows. *Netw. Neurosci.* **9**, 148--170 (2025). https://doi.org/10.1162/netn_a_00422

43. Liang, J. et al. Aversive learning induces context-gated global reorganization of neural dynamics in *Caenorhabditis elegans*. *bioRxiv* 2025.10.31.685731 (2025). https://doi.org/10.1101/2025.10.31.685731

44. Mante, V., Sussillo, D., Shenoy, K.V. & Newsome, W.T. Context-dependent computation by recurrent dynamics in prefrontal cortex. *Nature* **503**, 78--84 (2013). https://doi.org/10.1038/nature12742

45. Pu, S., Dang, W., Qi, X.-L. & Constantinidis, C. Prefrontal neuronal dynamics in the absence of task execution. *Nat. Commun.* **15**, 6476 (2024). https://doi.org/10.1038/s41467-024-50717-y

46. Bernardi, S. et al. The geometry of abstraction in the hippocampus and prefrontal cortex. *Cell* **183**, 954--967 (2020). https://doi.org/10.1016/j.cell.2020.09.031

47. Zhang, X., Liu, S. & Chen, Z.S. A geometric framework for understanding dynamic information integration in context-dependent computation. *iScience* **24**, 102919 (2021). https://doi.org/10.1016/j.isci.2021.102919

48. Chaudhuri, R., Gercek, B., Bhalla, U.S., Bhatt, D.H. & Bhatt, D.H. The intrinsic attractor manifold and population dynamics of a canonical cognitive circuit across waking and sleep. *Nat. Neurosci.* **22**, 1512--1520 (2019). https://doi.org/10.1038/s41593-019-0460-x

49. Darshan, R. & Rivkind, A. Learning to represent continuous variables in heterogeneous neural networks. *Cell Rep.* **39**, 110612 (2022). https://doi.org/10.1016/j.celrep.2022.110612

50. Gort, J. Emergence of universal computations through neural manifold dynamics. *Neural Comput.* **36**, 227--270 (2024). https://doi.org/10.1162/neco_a_01631

51. Sadtler, P.T. et al. Neural constraints on learning. *Nature* **512**, 423--426 (2014). https://doi.org/10.1038/nature13665

52. Feulner, B. & Clopath, C. Neural manifold under plasticity in a goal driven learning behaviour. *PLoS Comput. Biol.* **17**, e1008621 (2021). https://doi.org/10.1371/journal.pcbi.1008621

53. Athalye, V.R., Ganguly, K., Costa, R.M. & Carmena, J.M. Emergence of coordinated neural dynamics underlies neuroprosthetic learning and skillful control. *Neuron* **93**, 955--970 (2017). https://doi.org/10.1016/j.neuron.2017.01.016

54. Iwama, S., Zhang, Y. & Ushiba, J. De novo brain-computer interfacing deforms manifold of populational neural activity patterns in human cerebral cortex. *eNeuro* **9**, ENEURO.0145-22.2022 (2022). https://doi.org/10.1523/ENEURO.0145-22.2022

55. Mastrogiuseppe, F. & Ostojic, S. Linking connectivity, dynamics, and computations in low-rank recurrent neural networks. *Neuron* **99**, 609--623 (2018). https://doi.org/10.1016/j.neuron.2018.07.003

56. Beiran, M., Dubreuil, A., Valente, A., Mastrogiuseppe, F. & Ostojic, S. Shaping dynamics with multiple populations in low-rank recurrent networks. *Neural Comput.* **33**, 1--40 (2021). https://doi.org/10.1162/neco_a_01381

57. Schuessler, F., Dubreuil, A., Mastrogiuseppe, F., Ostojic, S. & Barak, O. Dynamics of random recurrent networks with correlated low-rank structure. *Phys. Rev. Res.* **2**, 013111 (2020). https://doi.org/10.1103/physrevresearch.2.013111

58. Cimesa, L., Ciric, L. & Ostojic, S. Geometry of population activity in spiking networks with low-rank structure. *PLoS Comput. Biol.* **19**, e1011315 (2023). https://doi.org/10.1371/journal.pcbi.1011315

59. Herbert, E. & Ostojic, S. The impact of sparsity in low-rank recurrent neural networks. *PLoS Comput. Biol.* **18**, e1010426 (2022). https://doi.org/10.1371/journal.pcbi.1010426

60. Pezon, L., Schmutz, V. & Gerstner, W. Linking neural manifolds to circuit structure in recurrent networks. *Neuron* (2026). https://doi.org/10.1016/j.neuron.2025.12.047

61. Valente, A., Ostojic, S. & Pillow, J.W. Probing the relationship between latent linear dynamical systems and low-rank recurrent neural network models. *Neural Comput.* **34**, 1871--1892 (2022). https://doi.org/10.1162/neco_a_01522

62. Safaie, M. et al. Preserved neural dynamics across animals performing similar behaviour. *Nature* **623**, 765--771 (2023). https://doi.org/10.1038/s41586-023-06714-0

63. Karpowicz, B.M. et al. Stabilizing brain-computer interfaces through alignment of latent dynamics. *Nat. Commun.* **16**, 4835 (2025). https://doi.org/10.1038/s41467-025-59652-y

64. Ganjali, M., Mehridehnavi, A., Rakhshani, S. & Khorasani, A. Unsupervised neural manifold alignment for stable decoding of movement from cortical signals. *Int. J. Neural Syst.* **34**, 2450006 (2024). https://doi.org/10.1142/S0129065724500060

65. Ma, X. et al. Using adversarial networks to extend brain computer interface decoding accuracy over time. *eLife* **12**, e84296 (2023). https://doi.org/10.7554/eLife.84296

66. Natraj, N. et al. Sampling representational plasticity of simple imagined movements across days enables long-term neuroprosthetic control. *Cell* **188**, 1245--1263 (2025). https://doi.org/10.1016/j.cell.2025.02.001

67. Liu, T. et al. Uncovering low-dimensional manifolds of neural dynamics for motor-imagery based stroke rehabilitation: an EEG-based brain-computer interface study. *IEEE Trans. Neural Syst. Rehabil. Eng.* **33**, 2436--2446 (2025). https://doi.org/10.1109/TNSRE.2025.3600824

68. Langdon, C., Genkin, M. & Engel, T.A. A unifying perspective on neural manifolds and circuits for cognition. *Nat. Rev. Neurosci.* **24**, 363--377 (2023). https://doi.org/10.1038/s41583-023-00693-x

69. Dura-Bernal, S. et al. Multiscale model of primary motor cortex circuits predicts in vivo cell-type-specific, behavioral state-dependent dynamics. *Cell Rep.* **42**, 112574 (2023). https://doi.org/10.1016/j.celrep.2023.112574

70. Almani, M.N. et al. Embodied sensorimotor control: computational modeling of the neural control of movement. *Annu. Rev. Biomed. Eng.* **28** (2026). https://doi.org/10.1146/annurev-bioeng-102723-020454

71. Yang, X. et al. Epileptic detection in single and multi-lead EEG signals using persistent homology based on bi-directional weighted visibility graphs. *Chaos* **33**, 063139 (2023). https://doi.org/10.1063/5.0140579

72. Fehrman, C. & Meliza, C.D. Model predictive control on the neural manifold. *Neural Comput.* **37** (2025). https://doi.org/10.1162/neco.a.37

73. Gallego-Carracedo, C., Perich, M.G., Chowdhury, R.H., Miller, L.E. & Gallego, J.A. Local field potentials reflect cortical population dynamics in a region-specific and frequency-dependent manner. *eLife* **11**, e73155 (2022). https://doi.org/10.7554/eLife.73155

74. Trautmann, E.M. et al. Accurate estimation of neural population dynamics without spike sorting. *Neuron* **103**, 292--308 (2019). https://doi.org/10.1016/j.neuron.2019.05.003

75. Vyas, S. et al. Neural population dynamics underlying motor learning transfer. *Neuron* **97**, 1177--1186 (2018). https://doi.org/10.1016/j.neuron.2018.01.040

76. Pandarinath, C. et al. Neural population dynamics in human motor cortex during movements in people with ALS. *eLife* **4**, e07436 (2015). https://doi.org/10.7554/eLife.07436

77. Mignacco, F., Chou, C.-N. & Chung, S. Nonlinear classification of neural manifolds with contextual information. *Phys. Rev. E* **110**, 054404 (2024). https://doi.org/10.48550/arXiv.2405.06851

78. Morrison, M., Fieseler, C. & Kutz, J.N. Nonlinear control in the nematode *C. elegans*. *Front. Comput. Neurosci.* **14**, 616639 (2020). https://doi.org/10.3389/fncom.2020.616639

79. Herz, A.V.M., Mathis, A. & Stemmler, M. Periodic population codes: from a single circular variable to higher dimensions, multiple nested scales, and conceptual spaces. *Curr. Opin. Neurobiol.* **46**, 99--108 (2017). https://doi.org/10.1016/j.conb.2017.07.005

80. Vermani, A. et al. Meta-dynamical state space models for integrative neural data analysis. *ArXiv* (2025). https://pubmed.ncbi.nlm.nih.gov/40297236/

81. Gallego, J.A. et al. Neural manifolds for the control of movement. *Neuron* **94**, 978--984 (2017). https://doi.org/10.1016/j.neuron.2017.05.025

82. Sussillo, D. & Abbott, L.F. Generating coherent patterns of activity from chaotic neural networks. *Neuron* **63**, 544--557 (2009). https://doi.org/10.1016/j.neuron.2009.07.018

83. Sussillo, D. Neural circuits as computational dynamical systems. *Curr. Opin. Neurobiol.* **25**, 156--163 (2014). https://doi.org/10.1016/j.conb.2014.01.008

84. Jazayeri, M. & Ostojic, S. Interpreting neural computations by examining intrinsic and embedding dimensionality of neural activity. *Curr. Opin. Neurobiol.* **70**, 113--120 (2021). https://doi.org/10.1016/j.conb.2021.08.002

85. Stringer, C. et al. Spontaneous behaviors drive multidimensional, brainwide activity. *Science* **364**, eaav7893 (2019). https://doi.org/10.1126/science.aav7893

86. Stringer, C., Pachitariu, M., Steinmetz, N., Carandini, M. & Harris, K.D. High-dimensional geometry of population responses in visual cortex. *Nature* **571**, 361--365 (2019). https://doi.org/10.1038/s41586-019-1346-5

87. Saxena, S. & Cunningham, J.P. Towards the neural population doctrine. *Curr. Opin. Neurobiol.* **55**, 103--111 (2019). https://doi.org/10.1016/j.conb.2019.02.002

88. Rajan, K., Harvey, C.D. & Tank, D.W. Recurrent network models of sequence generation and memory. *Neuron* **90**, 128--142 (2016). https://doi.org/10.1016/j.neuron.2016.02.009

89. Li, H.-H., Ma, W.J. & Curtis, C.E. Drift-like dynamics and information flow across the cortical hierarchy during working memory. *bioRxiv* 2025.08.07.669201 (2025). https://doi.org/10.1101/2025.08.07.669201

91. Ciferri, M., Ferrante, M. & Toschi, N. Reconstructing music perception from brain activity using a prior guided diffusion model. *Sci. Rep.* **15**, 12345 (2025). https://doi.org/10.1038/s41598-025-26095-w

92. Friston, K.J. Transients, metastability, and neuronal dynamics. *NeuroImage* **5**, 164--171 (1997). https://doi.org/10.1006/nimg.1997.0259

93. Kuoch, M. et al. Probing biological and artificial neural networks with task-dependent neural manifolds. *CPAL* (2023). https://doi.org/10.48550/arXiv.2312.14285

94. Li, D., Chung, S. & Sompolinsky, H. Dynamic Manifold Hopfield Networks for context-dependent associative memory. *ArXiv* (2025). https://www.semanticscholar.org/paper/7ca1bd83a66d524413034ba08f63cd2da1385119

