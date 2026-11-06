# STD — Code-First Graphics, Animation and Cinema Skill Matrix

- Document: STD-SKILL-001
- Version: 0.1.0
- Status: Learning roadmap; not a claim of completed mastery.

## Priority key
- P0: foundational; learn before building the engine.
- P1: needed for first production-quality outputs.
- P2: advanced production capability.
- P3: specialist or optional engine capability.

## 1. Programming

| Priority | Skill | Required knowledge | Practice output |
|---|---|---|---|
| P0 | Python | functions, classes, modules, typing, generators, file IO, subprocess, testing | deterministic image generator |
| P0 | TypeScript | types, modules, async, strict mode, build tools | Motion Canvas scene |
| P0 | CLI engineering | arguments, config, logs, exit codes | render command |
| P0 | Git | branches, commits, tags, LFS, reproducible source | versioned project |
| P1 | C/C++ | memory, RAII, SIMD, threads, native libraries | performance experiment |
| P1 | Rust | ownership, errors, concurrency, FFI | safe media worker utility |
| P1 | Data contracts | JSON Schema, versioning, validation, migrations | render-job schema |
| P2 | GPU programming | compute, buffers, pipelines, synchronization | shader experiment |

## 2. Mathematics and motion

| Priority | Skill | Required knowledge | Practice output |
|---|---|---|---|
| P0 | Linear algebra | vectors, matrices, dot/cross products, transforms | animated transforms |
| P0 | Trigonometry | angles, rotations, periodic functions | procedural orbit and wave |
| P0 | Curves | Bézier, splines, arc length | path-following animation |
| P0 | Interpolation | linear, Hermite, cubic, easing, spring | timing library |
| P1 | 3D geometry | coordinate spaces, normals, topology, UVs | procedural mesh |
| P1 | Quaternions | orientation, slerp, rotation composition | smooth camera/rig motion |
| P1 | Numerical methods | integration, stability, sampling | particle simulation |
| P2 | Kinematics | forward/inverse kinematics, constraints | character rig |
| P2 | Physics | rigid body, cloth, fluids, collisions | simulation shot |

## 3. Computer graphics and image science

- Raster and vector representations.
- SVG path grammar, Bézier curves, clipping, masks and gradients.
- Canvas 2D, SVG DOM, WebGL and WebGPU.
- Rasterization, tessellation, anti-aliasing and sampling.
- Texture mapping, UVs, mipmaps and filtering.
- Shader languages: GLSL and WGSL.
- Lighting, BRDF, PBR, shadows, reflections and global illumination.
- Ray tracing/path tracing, denoising and sampling noise.
- Alpha compositing, premultiplication, mattes and keying.
- Linear-light compositing, sRGB, HDR, ICC and OCIO.
- Image formats, metadata, bit depth, compression and color profiles.

## 4. Animation craft

- Frame rates, rational timebases and frame-accurate timing.
- Keyframes, channels, animation curves and interpolation.
- Staggering, sequencing, loops and state machines.
- Kinetic typography, logo animation, lower thirds and infographics.
- Sprite sheets, frame-by-frame, cut-out and vector tweening.
- Skeletons, bones, skinning, blend shapes and retargeting.
- Camera paths, motion blur, depth of field and focus pulls.
- Procedural motion, particles, instancing and simulation.
- Continuity, anticipation, staging, weight, follow-through and settle.

## 5. 3D and VFX

- Modeling, topology, normals, UVs and material authoring.
- Rigging, skinning, facial systems and animation retargeting.
- Camera, lens, exposure, lighting and render passes.
- PBR, path tracing, global illumination and denoising.
- Geometry Nodes and procedural scene generation.
- Rigid body, cloth, fluid, hair and particle simulation.
- Motion tracking, camera tracking, rotoscoping and keying.
- Node compositing, masks, alpha, mattes and OpenFX.
- USD scene composition, instancing and time-sampled data.
- EXR passes, multilayer images and render metadata.

## 6. Cinema, editorial and sound

- Story structure, beats, screenplay and scene breakdown.
- Shot lists, storyboards, animatics and previs.
- Blocking, screen direction, eyelines and continuity.
- Lens vocabulary, framing, camera movement and motivated lighting.
- Coverage, editing rhythm, cuts, transitions and timeline structure.
- Dialogue editing, Foley, ambience, music and sound effects.
- PCM/WAV, sample rates, bit depth, channels and synchronization.
- Loudness, stems, mixing and final audio QC.
- Color grading, look matching, HDR/SDR and delivery masters.

## 7. Production engineering

- Reproducible jobs, dependency pinning and environment capture.
- Asset manifests, hashes, lineage and version control.
- Render queues, job dependencies, retries and cancellation.
- Cache design, parallelism, CPU/GPU profiling and memory limits.
- Frame-level tests, golden images, pixel diffs and perceptual review.
- Media metadata validation and corrupt-file detection.
- Crash recovery, idempotency, logs and observability.
- License, attribution, font, model, texture and codec audits.
- Safe handling of untrusted scripts and project files.

## 8. Learning sequence

1. P0 — Single frame: create one PNG and one SVG using code; prove dimensions, alpha, color and reproducibility.
2. P0 — Motion primitive: implement deterministic timeline, interpolation, easing and a 2D object moving through keyframes.
3. P0 — Motion Canvas: create a 5–10 second vector animation with preview and export.
4. P0 — FFmpeg: encode an image sequence, attach audio and inspect output.
5. P1 — Blender Python: create a scene, camera, light, object, animation and headless render.
6. P1 — 3D math: implement transforms, camera projection and procedural geometry.
7. P1 — Compositing: alpha, masks, EXR and color transforms.
8. P1 — Editorial: represent clips and tracks in OTIO and render a timeline.
9. P2 — Character animation: rigging, skinning, IK, motion curves and continuity.
10. P2 — VFX: particles, simulation, tracking and node compositing.
11. P2 — Render orchestration: local queue, worker isolation, retries and artifact manifests.
12. P3 — Cinematic pipeline: multi-shot continuity, asset tracking, distributed render and final mastering.

## 9. Relevant installed skill references

These are available instruction packages in the current ChatGPT environment. They are workflow aids, not substitutes for learning mathematics, APIs and source code.

### Motion and code translation
- figma-implement-motion — maps motion context to CSS keyframes or Motion.dev and framework code.
- figma-use-motion — keyframes, easing, timeline duration and animation styles in Figma.
- canvas2d-data-visualization — Canvas2D rendering and hybrid Canvas/SVG/HTML patterns.
- threejs-data-visualization — Three.js, raw WebGL and GPU-based rendering.
- d3-data-visualization — SVG/DOM data-driven graphics.

### Testing and accessibility
- testing-data-visualizations — screenshot/image-diff, visual regression and export tests.
- accessibility-and-inclusive-visualization — contrast, keyboard, reduced motion and readable graphics.
- test-driven-development — red/green/refactor implementation discipline.
- atlas-research — source registry, evidence, recipes and research traceability.

### Magnific workflow skills
- magnific-essentials — credit controls, job lifecycle, asset import, result delivery and provenance.
- previs-storyboard — shot list, storyboard and timed animatic.
- cinematic-shots — shot direction, continuity and sequence generation.
- consistent-characters — character/location identity references.
- video-finishing — editing, grade, upscale, retiming and delivery.
- sound-and-voice — dialogue, voice, music, SFX and mixing.
- localize-video — captions, dubbing and localization.
- video-ad and ad-campaign — campaign-specific production workflows.

## 10. Mastery evidence

A skill is not marked learned merely because documentation was read. Each skill needs:
- a runnable exercise;
- a source-controlled example;
- tests or measurable output checks;
- a list of limitations;
- a reproducible environment;
- a reference to official docs and exact library version.

Use statuses: NOT STARTED, STUDYING, PRACTICED, TESTED, VALIDATED.