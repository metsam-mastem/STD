# Code-First Media Production — Feasibility Research

- Project: STD — Studio & Technical Direction
- Report: STD-RPT-001
- Version: 0.1.0
- Date: 2026-11-06
- Phase: 1 — Coding knowledge, source ecosystem and feasibility
- Status: Research baseline; architecture proposed, not approved
- Scope exclusion: LLMs and generative models are not part of the core-engine selection.

## 1. Executive finding

Code-driven creation of still images, vector graphics, motion graphics, 2D animation, 3D animation, compositing, visual effects and encoded video is technically feasible with mature open-source components.

A feature-length cinematic pipeline is feasible as a systems-integration problem, not as one renderer. It requires coordinated asset creation, scene description, animation, lighting, rendering, compositing, editorial, sound, color management, encoding, QC, asset tracking and render orchestration.

Recommended strategy: a modular production workbench with a deterministic core, independent engine adapters, a media-processing/interchange layer, a local render queue and optional delivery clients.

## 2. Repository inspection

Evidence: metsam-mastem/STD is public, default branch main, reported repository size zero. The GitHub contents endpoint returned 404 with the message that the repository is empty.

Implication: no existing code, directory layout, license file, CI configuration or architecture was available to preserve.

Action: initialize research documentation only. No production code, generated media, external service or paid job was created.

## 3. Feasibility by output class

| Output | Code-first feasibility | Main requirements |
|---|---|---|
| Raster still image | High | pixels, color spaces, sampling, filters, typography, image IO |
| SVG/vector still | High | paths, Bézier curves, transforms, clipping, gradients, text layout |
| Motion graphics | High | timeline, timebase, keyframes, easing, typography, layers |
| 2D animation | High | sprites, skeletal rigs, interpolation, frame timing, compositing |
| 3D animation | High | mesh topology, transforms, rigs, skinning, camera, lighting |
| Procedural VFX | High, specialist complexity | particles, fluids, rigid bodies, fields, shaders, simulation caches |
| Compositing | High | alpha, premultiplication, masks, keying, tracking, color management |
| Editorial video | High | timeline model, source media, trims, transitions, audio synchronization |
| Cinematic sequence | Feasible | continuity, shot design, assets, scene management, render and editorial pipeline |
| Feature-length film | Feasible as a production system | distributed rendering, storage, asset/version control, sound, QC, color and delivery |

A one-frame render does not prove a cinematic pipeline. A valid production workflow also needs continuity, shot-level approvals, deterministic revisions, asset provenance and final-master verification.

## 4. Recommended engine candidates

### Core production engines

| Engine | Responsibility | Fit | Initial position |
|---|---|---|---|
| Blender + Python API | 3D, rigging, animation, simulation, rendering, compositing, tracking, video editing | Primary 3D/cinematic engine | Primary candidate |
| Motion Canvas | Programmatic TypeScript vector animation and preview editor | Motion graphics, explainers, titles | Primary 2D code-animation candidate |
| Manim Community | Programmatic mathematical/vector animation in Python | Technical and geometric animation | Specialized adapter |
| Three.js | Browser 3D rendering with WebGL/WebGPU | Interactive 3D preview and browser experiences | Dashboard/preview adapter |
| Synfig | Vector/bitmap 2D animation, bones, tweening and effects | Traditional 2D animation | Optional adapter |
| Gaffer | Node-based look development, lighting and scene automation; Python/OSL scripting | Advanced VFX/lighting pipeline | Advanced adapter |
| Natron | Node-based compositing and OpenFX | Compositing/VFX | Optional adapter |
| Godot | Real-time 2D/3D engine and animation system | Interactive and real-time scenes | Optional; not primary offline film renderer |

### Infrastructure and interchange

| Component | Responsibility |
|---|---|
| FFmpeg | Media probing, filtering, image-sequence assembly, audio/video encoding and muxing |
| OpenTimelineIO | Editorial timeline interchange: clips, tracks, transitions, markers and metadata; references media rather than embedding it |
| OpenImageIO | Format-agnostic image IO and image processing for VFX |
| OpenEXR | High-dynamic-range image and render-pass storage |
| OpenColorIO | Color-space transforms and consistent color management |
| OpenUSD | Scalable, time-sampled scene description and interchange |
| Flamenco | Self-hosted render-job management, especially for Blender |
| Rive Runtime | Reusable vector animation playback and state-machine runtime |
| GSAP | Browser motion sequencing; verify license and intended use before embedding |
| Remotion | React-based programmatic video; source-available under a special license, not OSI open source. Optional pending license review |

Do not confuse a renderer with a codec, a timeline interchange format with a media container, or a scene-description format with a 3D application.

## 5. Coding and mathematics knowledge required

### Programming foundations
- Python: modules, packages, typing, dataclasses, iterators, generators, context managers, file IO, subprocess, multiprocessing, profiling and testing.
- TypeScript/JavaScript: strict typing, async control, browser rendering, Web APIs, workers, bundling and package management.
- C/C++: memory layout, pointers, RAII, SIMD, threading, native libraries and GPU-facing code.
- Rust: ownership, lifetimes, error handling, concurrency and safe native tooling.
- CLI design, configuration, structured logging, serialization, schema validation and reproducible builds.

### Mathematics and geometry
- Scalars, vectors, matrices, coordinate systems and basis changes.
- 2D/3D affine transforms, homogeneous coordinates and matrix composition.
- Quaternions, Euler angles, rotation order and interpolation.
- Trigonometry, analytic geometry, linear algebra and numerical methods.
- Bézier curves, Catmull–Rom splines, arc length and path following.
- Interpolation, easing functions, spring systems and time remapping.
- Camera projection, field of view, perspective, orthographic projection and depth.
- Mesh topology, normals, tangents, UVs, barycentric coordinates and spatial acceleration structures.
- Kinematics, inverse kinematics, constraints, collision detection and rigid-body dynamics.

### Computer graphics
- Rasterization, vector paths, tessellation and anti-aliasing.
- CPU/GPU rendering and graphics pipelines.
- WebGL, WebGPU, OpenGL/Vulkan concepts, GLSL and WGSL shaders.
- Textures, mipmaps, sampling, filtering and texture coordinates.
- Lighting, BRDF, PBR materials, shadows, reflections and global illumination.
- Ray tracing/path tracing and denoising.
- Alpha compositing, premultiplied alpha, masks, mattes and color transforms.
- Linear light, sRGB, HDR, bit depth, chroma subsampling and color management.

### Animation
- Frame rate, frame index, rational timebase and sub-frame timing.
- Keyframes, curves, interpolation, easing, animation graphs and state machines.
- Pose systems, rigs, bones, skinning and deformation.
- Motion paths, camera animation, constraints and procedural motion.
- Particle systems, instancing, cloth, fluid, hair and rigid-body simulation.
- Motion blur, frame sampling, retiming and temporal continuity.
- 2D cut-out, frame-by-frame, vector tweening and sprite animation.

### Cinema and production craft
- Screenplay structure, beats, scenes, sequences and shot lists.
- Storyboards, animatics, blocking and previs.
- Shot size, camera angle, lens, focal length, depth of field and exposure.
- Screen direction, eyelines, continuity, staging and camera motivation.
- Editing rhythm, coverage, transitions and editorial decision lists.
- Dialogue, Foley, ambience, music, sample rates, loudness and audio mixing.
- Color grading, look development, mastering, captions and delivery specifications.

### Production engineering
- Deterministic render jobs and reproducible environments.
- Asset identity, manifests, hashes, versioning and dependency pinning.
- Render queues, retries, cancellation, idempotency and crash recovery.
- CPU/GPU profiling, memory budgets, caching and parallel rendering.
- Frame-level tests, golden-image tests, visual diffs and QC reports.
- Security boundaries for untrusted project files, scripts, plugins and uploaded media.
- License inventory for code, fonts, textures, models, audio, plugins and codecs.

## 6. Output and interchange rules

- Vector graphics: SVG or documented vector scene graph.
- Raster images: PNG for lossless 8-bit deliverables; TIFF/EXR for higher bit-depth and VFX.
- 3D assets: glTF/GLB for runtime exchange; USD for larger scene interchange; retain native project files.
- Editorial: OTIO plus external media references.
- Audio: WAV/PCM master with explicit sample rate and channel layout.
- Video: image sequences or mezzanine masters during production; H.264/H.265/AV1 or other delivery codecs only at final delivery.

The production master should not be a heavily compressed social-media file. Preserve source frames, audio stems, edit data and render metadata.

## 7. Integration surfaces

The same core should be callable through local CLI, desktop app, local HTTP service, browser dashboard, optional browser extension, Telegram bot, GitHub Actions, self-hosted GitHub runner and optional AppDeploy-hosted dashboard.

Telegram is a control plane, not a renderer. The official Bot API documents ordinary uploads up to 50 MB; its local Bot API server supports uploads up to 2000 MB.

GitHub-hosted runners are suitable for tests, packaging and bounded render tasks. Heavy or long renders should use a self-hosted runner or separate render worker, with artifact retention and runner quotas considered.

## 8. Magnific findings — separate from the code-first core

### Magnific Move
The connected Magnific catalog exposes video_move_create, video_move_get and video_move_render. Its stated use is code-authored motion graphics: kinetic typography, logo reveals, explainers, infographics, lower thirds and social ads. It is distinct from generative video footage.

Flow:
1. provide brief/copy/style/pacing and optional imported references;
2. start a Move project;
3. inspect the version using its project ID;
4. render the ready version to MP4 with selected FPS, scale and motion-blur option.

allowGeneration defaults to false; this keeps the workflow to references, code, free fonts and free sound effects. Narration/music or paid generated visual assets require a different permission choice.

### Other Magnific surfaces
- Spaces: node-based visual workflows and reusable connected pipelines.
- 3D Scenes: compose a virtual scene, arrange objects/characters, frame a camera and capture.
- Video Generator: model-generated video footage; outside the core-engine scope.
- Video finishing: cutting, concatenation, grading, retiming, background removal, upscaling and editor-ready delivery.
- Previs/storyboard: shot lists, consistent frames and timed animatics.
- Sound and voice: voice, dialogue, music, SFX and mixing.

### Account and source limitation
At inspection, the connected account reported Free/Basic and zero available credits. No paid generation was run. The official Magnific documentation is public, but no public source repository for the hosted Magnific platform was established. The connected tool interface and documented contracts are the evidence used for Move integration.

## 9. Licensing and provenance gates

- Blender: GPL-3.0 for Blender as a whole; audit add-ons and dependencies separately.
- Motion Canvas: MIT.
- Manim Community: MIT.
- Synfig: GPL-3.0.
- Godot: MIT.
- OpenImageIO: Apache-2.0.
- OpenEXR: BSD-3-Clause.
- Natron: GPL-2.0 according to its repository README.
- Flamenco: GPL-3.0-or-later.
- Remotion: special proprietary/source-available license; not OSI open source.
- Other candidates (GSAP, Rive editor, plugins, fonts, assets and codecs): verify exact current terms before bundling or commercial distribution.

A project's license does not automatically cover assets, fonts, models, plugins, patents or codecs used by that project.

## 10. Preliminary architecture recommendation

Use a provider-neutral core with first-class adapters:
- Motion Canvas for code-first 2D motion graphics.
- Blender for 3D, animation, rendering and the first cinematic pipeline.
- FFmpeg for media processing and final assembly.
- OpenTimelineIO for editorial interchange.
- OpenColorIO/OpenEXR/OpenImageIO for professional image pipeline support.
- Flamenco as optional distributed-render adapter.
- Manim as specialized Python animation adapter.

Keep Synfig, Gaffer, Natron, Godot, Three.js, Rive, GSAP and Remotion optional until a measurable requirement justifies them.

## 11. Open questions
1. Which first deliverable defines MVP acceptance: a 10-second 2D motion graphic, a 10-second 3D shot, or a multi-shot animatic?
2. Which machine is the first execution target and what are its CPU, RAM, GPU and free storage?
3. Must the first release run entirely offline after installation?
4. Is the dashboard primarily a local control panel or a hosted remote interface?
5. Which export formats and target frame rates are mandatory for the first release?

## 12. Status discipline
- EVIDENCE: repository metadata, official project documentation, source README files and connected Magnific tool contracts inspected.
- INFERENCE: modular engine architecture and recommended primary stack.
- PLANNED: implementation, benchmarking, deployment and end-to-end render validation.
- NOT RUN: no renderer benchmark, local installation test, generated media or deployed dashboard.