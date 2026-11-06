# STD — Studio & Technical Direction

**Status:** Research baseline · 0.1.0 · 2026-11-06

A modular, code-first media workbench for still images, motion graphics, 2D/3D animation, VFX, editorial timelines and cinematic rendering.

## Principles
- The core works without an LLM, generative model, paid API or cloud service.
- Engines are replaceable adapters, not hard-coded dependencies.
- Local-first operation; network services are optional.
- Every output has a reproducible job specification, asset manifest and render metadata.
- Large binary media does not belong in ordinary Git history.
- No engine is validated until reproducible test renders and acceptance checks pass.

## Research status
- [x] Initial source and ecosystem survey
- [x] Code-first skill map
- [x] Proposed modular architecture
- [x] Delivery-surface comparison
- [ ] Architecture decision approved
- [ ] MVP engine benchmarked
- [ ] Core contracts and tests implemented
- [ ] First local render pipeline validated

## Documents
- Research report: docs/research/2026-11-06-code-first-media-research.md
- Engine architecture: docs/architecture/proposed-engine-map.md
- Skill matrix: docs/learning/skill-matrix.md
- Integration surfaces: docs/integrations/delivery-surfaces.md
- Source register: docs/research/sources.md
- Phase 1 handoff: docs/handoff/phase-1-handoff.md

## Boundary
The repository was empty at inspection time. This initial commit establishes research documentation only. No production renderer, generated media, dashboard or paid integration has been added.