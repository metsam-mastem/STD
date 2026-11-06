# STD — Phase 1 Handoff

- Handoff ID: STD-HO-001
- Version: 0.1.0
- Date: 2026-11-06
- Current phase: Research and coding knowledge
- Next phase: Engine proof-of-capability and conversion pipeline design
- Repository: https://github.com/metsam-mastem/STD

## 1. Actually completed
- [x] Confirmed STD repository metadata and empty initial state.
- [x] Surveyed official documentation and selected upstream repositories.
- [x] Inspected selected repository README files and license declarations.
- [x] Built programming, mathematics, graphics, animation, cinema and production-engineering skill map.
- [x] Compared candidate rendering and media-processing engines.
- [x] Inspected Magnific official docs and connected Move/Spaces/3D Scene tool contracts.
- [x] Inspected AppDeploy frontend-only React/Vite deployment preflight. No app was deployed.
- [x] Wrote research report, proposed architecture, skill matrix, integration map and source register.

## 2. Not complete
- [ ] No local engine installation has been tested.
- [ ] No code-driven image or video was rendered.
- [ ] No performance benchmark was run.
- [ ] No engine adapter or dashboard has been implemented.
- [ ] No Telegram bot or GitHub Actions workflow has been created.
- [ ] No AppDeploy dashboard has been deployed.
- [ ] No paid Magnific generation has been run.
- [ ] No full source-code, security or license audit has been completed.
- [ ] No architecture decision has been approved.

## 3. Recommended next work packages

### WP-01 — Coding and rendering foundations
Build a deterministic Python/TypeScript proof:
- generate one SVG and one PNG;
- animate a geometric subject with timeline and easing;
- render a frame sequence;
- encode MP4 with FFmpeg;
- inspect dimensions, frame rate, duration and audio state;
- create a manifest and checksum.

### WP-02 — Motion Canvas adapter
- install in an isolated workspace;
- create a minimal vector scene;
- render preview and final output;
- test deterministic rerender and frame-count correctness;
- record CPU/RAM/time and output size.

### WP-03 — Blender headless adapter
- create a minimal scene through bpy;
- render a still and short frame sequence;
- test headless CLI execution;
- capture render settings and dependencies;
- measure memory and render time.

### WP-04 — Core contracts
- EngineManifest
- RenderJob
- ArtifactManifest
- RenderResult
- versioning and schema migration tests

### WP-05 — Render control plane
- local queue and worker process;
- progress, logs, cancellation and retries;
- bounded CPU/RAM/disk/time;
- job and artifact provenance.

### WP-06 — Delivery clients
Only after the local API is stable: CLI, React/Vite dashboard, Telegram bot, GitHub Actions, optional self-hosted runner, optional AppDeploy dashboard and Magnific adapter.

## 4. Acceptance criteria for the first vertical slice

1. One command validates a render job without launching the renderer.
2. One command renders a deterministic 5–10 second animation locally.
3. Expected frame count equals the timebase calculation.
4. Output video can be probed and decoded by FFmpeg.
5. Output metadata includes dimensions, FPS/timebase, duration and checksum.
6. A repeated render with identical inputs/settings produces equivalent output within declared deterministic limits.
7. A failed job records an error and does not report success.
8. The job can be cancelled without corrupting project assets.
9. The dashboard can display status and link to the resulting artifact.
10. No LLM or paid API is required for this path.

## 5. Decision required before implementation

Choose the first acceptance target:
- A — 2D motion graphic: quickest and lowest-resource proof of the code-to-video pipeline.
- B — 3D cinematic shot: validates Blender and 3D scene rendering early, with higher resource cost.
- C — storyboard/animatic: validates shot sequencing and editorial contracts, but does not prove final-quality rendering.

Recommendation: A first, then B, then C as the bridge to multi-shot cinema. This keeps the first milestone measurable and affordable without excluding the cinematic roadmap.

## 6. Handoff integrity

This document records research and planned work. It does not claim code execution, successful rendering, deployment or validation. Update this handoff append-only when new work is actually performed; preserve prior status and evidence.