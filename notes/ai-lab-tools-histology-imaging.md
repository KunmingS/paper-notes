---
title: "AI tools eating wet-lab histology and imaging workflows"
authors: —
year: 2026
source: drafts/neuroscience/ai-lab-tools-histology-imaging.md
source_url: ~
tags: [methods, ai-tools, histology, cell-segmentation, neuroscience]
created: 2026-04-08
---

# AI tools eating wet-lab histology and imaging workflows

## TL;DR
Drop-in AI tools are displacing the manual bench workflows that have consumed grad-student time for decades: **DeepSlice** auto-registers brain slices to a reference atlas at >1000x human speed; **CellPose** and **StarDist** segment cells well enough that hand-counting in ImageJ is no longer the only option. Many labs haven't switched yet — the gap between available tooling and actual practice is still wide.

## Key tools
- **DeepSlice** — automatic histological brain-section registration to a reference atlas. Quoted as >1000x faster than manual alignment.
- **CellPose** — generalist deep-learning cell segmentation; handles diverse morphologies without retraining.
- **StarDist** — star-convex polygon detection, popular for nuclei/cell body segmentation.
- **ImageJ** — the legacy default for manual counting/annotation; still in heavy use in many labs despite AI alternatives.

## Why it matters
Pipeline-level acceleration (1000x) on the "boring" parts of histology changes what experiments are even worth running — brain-wide quantification studies that used to be prohibitively tedious become routine. The slow adoption curve suggests an opportunity: labs that integrate these tools gain a genuine throughput advantage over those that don't.

## Related
- [[science-ai-agents-saas-landscape]] — the commercial SaaS layer above these open-source tools
- [[wiki/neuroai-and-embodiment]] — adjacent: AI reshaping experimental neuroscience, not just modeling it
