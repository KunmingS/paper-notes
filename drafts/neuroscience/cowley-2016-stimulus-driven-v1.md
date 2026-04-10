---
title: "Stimulus-Driven Population Activity Patterns in Macaque Primary Visual Cortex"
authors: "Benjamin R. Cowley, Matthew A. Smith, Adam Kohn, Byron M. Yu"
source_url: https://doi.org/10.1371/journal.pcbi.1005185
fetched: 2026-04-09
---

# Stimulus-Driven Population Activity Patterns in Macaque Primary Visual Cortex

## Abstract

This study applies principal component analysis (PCA) to trial-averaged neural responses in macaque primary visual cortex (V1) to address two fundamental questions about neural populations. First, the researchers investigate how neural complexity relates to stimulus complexity by measuring dimensionality through relative comparisons. Second, they assess whether responses to different stimuli occupy similar dimensions of the population activity space using a novel statistical method. Comparative analyses include a recently-proposed V1 receptive field model and a deep convolutional neural network. The findings demonstrate that "the dimensionality of the population response changes systematically with alterations in the properties and complexity of the visual stimulus."

## Author Summary

This work examines how large neural populations work together to enable sensory processing. While dimensionality reduction methods have been applied to neural population activity, their interpretability needed validation. The researchers recorded tens of neurons in macaque V1 while presenting different visual stimuli. Key findings show that population activity dimensionality grows with stimulus complexity, and responses to different stimuli occupy overlapping dimensions within the population firing rate space, mirroring the stimuli themselves. Comparison with a V1 receptive field model and deep network yielded interpretable results, supporting the broader application of dimensionality reduction in systems neuroscience.

## Introduction

Dimensionality reduction has been applied across multiple brain areas to study decision-making, motor control, olfaction, working memory, visual attention, audition, rule learning, and speech. However, application in brain areas where the stimulus-response relationship is poorly characterized can produce difficult-to-interpret results.

The authors note that "it is important to vary the inputs to a brain area and ask whether the outputs of dimensionality reduction change in a sensible way." This validation is most feasible in sensory cortices like V1, where stimulus-response properties are well-established.

The study addresses two key questions: (1) How does neural complexity scale with stimulus or task complexity? (2) How does a neural circuit flexibly encode the vast number of stimuli in the natural world?

The concept of dimensionality is illustrated through the population firing rate space, where each axis represents one neuron's firing rate. Dimensionality reduction identifies how many dimensions the neural population activity occupies and how these dimensions are oriented. The authors propose that "responses to different stimuli might occupy similar dimensions of the population activity space."

## Results

### Dimensionality of Population Responses to Gratings

The researchers varied stimulus complexity by presenting different numbers of consecutive grating orientations (1-12 orientations). Using PCA and a novel pattern aggregation method, they found that "the dimensionality for two orientations was 1.62 times the dimensionality for one orientation," significantly lower than random expectations (p < 10^-5). This indicates population responses share approximately half their basis patterns across consecutive orientations.

The dimensionality increased with angular offset between orientations up to 90°, then decreased, reaching minimum values at 180° offset (opposite drift directions). This result suggests "the population activity tends to use similar (but not identical) basis patterns for opposite drift directions."

Basis patterns were visualized, revealing that most neurons contribute to each pattern and that patterns capture both positive and negative signal correlations between neurons.

### Dimensionality of Population Responses to Different Classes of Visual Stimuli

Three movie stimuli were presented: gratings, natural scenes, and white noise. Stimulus complexity was assessed by applying PCA to pixel intensities, requiring 24, 64, and 459 dimensions respectively to explain 90% of variance.

Population response dimensionality followed stimulus complexity ordering: gratings < natural < noise. The researchers found that "the population responses to the gratings movie had the lowest dimensionality, followed by the natural movie, then the noise movie." This ordering was consistent across different neuron counts for both animals and was not simply explained by mean firing rate differences.

### Basis Patterns of Population Responses

Examining basis patterns across different stimulus types revealed mostly similar structures, though the highest-variance pattern for gratings and noise movies involved primarily two highly modulated neurons, while the natural movie's top pattern showed uniform signs (reflecting global luminance responses).

The pattern aggregation method quantitatively assessed pattern similarity across stimuli. Results indicated that "the dimensions occupied by the gratings movie overlap with those for the natural movie," with some overlap between all stimulus pairs, while "the dimensions occupied by the population response to the noise movie include most of the dimensions for the other two stimuli."

A Venn diagram summary showed basis patterns partially shared across stimuli, suggesting "a neural circuit is capable of expressing a limited repertoire of basis patterns, and that a subset of those basis patterns is employed for any given stimulus."

### Time-Resolved Dimensionality of Population Responses to Movie Stimuli

Using one-second windows, the researchers found consistent ordering (noise > natural/gratings) but noted that natural movie dimensionality was lower than gratings within short windows due to temporal correlations. When time points were shuffled, the natural movie exhibited higher dimensionality, confirming "the range of basis patterns expressed by the population responses to the natural movie within a short time window is limited by the temporal correlations in the natural movie itself."

Analyzing growing time windows from 1 to 30 seconds revealed that "the dimensionality corresponding to the natural movie grows more quickly and surpasses the dimensionality corresponding to the gratings movie for longer time windows." Pattern similarity matrices showed gratings movie patterns were more stable across time, while natural and noise movies recruited new patterns throughout presentation.

### Comparing to a V1 Receptive Field Model

A multi-component V1 receptive field model (Gabor filter, suppressive filter, normalization signal, exponential nonlinearity) was analyzed with similar methods. The model showed comparable trends to population activity for gratings responses, capturing direction selectivity effects. However, "the last component of the model showed substantially smaller dimensionalities than the other components," attributed to the exponential nonlinearity exaggerating distribution anisotropy.

For movie stimuli, the model's dimensionality ordering matched population responses, with the researchers noting that "the ordering of dimensionality for each component was consistent with the stimulus complexity ordering observed in the population responses."

## Discussion

The study demonstrates that dimensionality reduction applied to V1 yields interpretable, sensible results that track stimulus complexity. Population responses preserve the complexity ordering of visual stimuli, with dimensionality increasing systematically with stimulus complexity. The finding that "responses to different stimuli occupy similar dimensions of the population activity space" supports theories of flexible neural coding through multiplex representations.

Comparisons with the receptive field model and deep network provide further validation. The authors conclude that these findings "provide encouragement for the use of dimensionality reduction in other brain areas" where stimulus-response relationships are less well-characterized.
