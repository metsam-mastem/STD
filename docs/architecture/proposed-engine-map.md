# STD — Proposed Modular Engine Architecture

- Document: STD-ARC-001
- Version: 0.1.0
- Status: Proposed; not an approved implementation decision.

## 1. Architecture rule

The STD core owns job contracts, asset manifests, scheduling, validation and provenance. It does not implement every renderer. Each renderer or media processor is an adapter behind a stable interface.

No engine may be imported directly into the core domain package.

## 2. Logical layers

    Dashboard / CLI / Telegram / GitHub Actions / Desktop
                         |
                  Control Plane API
                         |
       Project + Asset Registry + Job Scheduler
                         |
            Versioned Core Contracts
                         |
       +-----------------+------------------+
       |                 |                  |
  2D Motion Adapter  3D Scene Adapter   Image Adapter
  Motion Canvas      Blender            SVG / Raster
       |                 |                  |
       +-----------------+------------------+
                         |
             Render / Media Processing
            FFmpeg · OpenImageIO · OCIO
                         |
              Editorial / Compositing
             OTIO · Natron · Gaffer
                         |
             Artifacts + QC + Provenance
                         |
                 Local / Export / Sync

## 3. Proposed repository layout

    STD/
    ├── README.md
    ├── apps/
    │   ├── dashboard/
    │   ├── desktop/
    │   └── telegram-bot/
    ├── core/
    │   ├── domain/
    │   ├── contracts/
    │   ├── scheduler/
    │   ├── validation/
    │   └── provenance/
    ├── adapters/
    │   ├── motion-canvas/
    │   ├── blender/
    │   ├── manim/
    │   ├── ffmpeg/
    │   ├── opentimelineio/
    │   ├── openimageio/
    │   ├── opencolorio/
    │   ├── natron/
    │   ├── gaffer/
    │   └── external/
    │       ├── magnific/
    │       └── remotion/
    ├── workers/
    │   ├── local/
    │   ├── github-actions/
    │   └── self-hosted/
    ├── workflows/
    │   ├── still-image/
    │   ├── motion-graphics/
    │   ├── animation-2d/
    │   ├── animation-3d/
    │   ├── compositing/
    │   ├── editorial/
    │   └── cinematic-sequence/
    ├── assets/
    │   ├── project-manifests/
    │   ├── fonts/
    │   ├── textures/
    │   ├── models/
    │   ├── audio/
    │   └── references/
    ├── tests/
    │   ├── unit/
    │   ├── contract/
    │   ├── golden-frames/
    │   ├── integration/
    │   └── fixtures/
    ├── packaging/
    │   ├── cli/
    │   ├── desktop/
    │   ├── browser-extension/
    │   └── github-actions/
    └── docs/

This is a proposed tree, not yet a created source-code structure. Only documentation directories exist in the initial research commit.

## 4. Versioned contracts

### Engine manifest
- engine_id, engine_version, adapter_version
- supported capabilities
- input/output formats
- required binaries and dependencies
- OS/CPU/GPU requirements
- offline classification
- license identifiers
- health-check and version-probe commands

### Render job
- job_id, project_id, contract_version
- engine_id and engine_version
- input asset IDs and content hashes
- scene/timeline specification
- frame range, FPS/timebase, resolution, color configuration
- output profile and destination
- resource limits and timeout
- deterministic seed where supported
- retry/cancellation policy

### Artifact manifest
- artifact_id, job_id, path/URI, media type
- checksum, byte size, dimensions, duration, frame rate
- color space, bit depth, audio sample rate/channels
- source assets and dependency hashes
- engine/build version and render settings
- created_at and validation result

### Render result
- status: PASS / FAIL / NOT RUN / BLOCKED
- outputs and logs
- warnings and errors
- QC measurements
- resource usage and elapsed time
- provenance links

## 5. Engine adapter interface

Each adapter should expose:
1. probe() — detect binary/version/capabilities.
2. validate(job) — validate inputs without rendering.
3. estimate(job) — estimate frames, memory and duration when possible.
4. prepare(job) — create isolated work directory and resolved inputs.
5. render(job) — run the engine with controlled arguments.
6. collect(job) — discover output artifacts and metadata.
7. validate_output(artifacts) — verify readability, dimensions, duration and expected frames.
8. cancel(job) — terminate safely and clean temporary state.
9. cleanup(job) — remove only owned temporary files.

Adapter failure must not corrupt core job state or another engine's workspace.

## 6. Data and file policy

- Git stores source code, schemas, tests, small reference assets and documentation.
- Large media files belong in local project storage or a dedicated object store; Git LFS may be used for selected versioned binaries.
- Render cache is disposable and separate from canonical project assets.
- Project manifests and timeline descriptions should be text-based and diffable.
- Every render output must be traceable to its inputs and exact settings.
- Paths should be relative to a project root where practical.

## 7. Local-first and device tiers

- Phone: control surface, job submission, preview, asset review and lightweight 2D tasks; do not assume sustained heavy 3D rendering.
- Low-memory laptop: CLI, vector motion, low-resolution previews, small Manim scenes, media inspection and orchestration.
- Workstation/render node: Blender high-quality rendering, simulation, compositing and parallel rendering.
- Optional remote worker: burst rendering only when the user explicitly enables a trusted host.

The control plane and worker should communicate through a documented local API so the dashboard can be on a different device from the renderer.

## 8. Security boundaries

- Treat project files, scripts, plugins, fonts, models and uploaded media as untrusted.
- Do not execute arbitrary project scripts in the dashboard process.
- Use isolated worker processes, timeouts, CPU/memory/disk quotas and explicit network policy.
- Avoid passing secrets to render jobs.
- Record plugin provenance, version and license.
- Require explicit approval for external uploads, paid services and public publishing.

## 9. Proposed MVP vertical slice

1. Create a project manifest.
2. Submit a deterministic 5–10 second Motion Canvas animation job.
3. Validate and render locally.
4. Inspect the generated frame sequence.
5. Encode MP4 with FFmpeg.
6. Create an artifact manifest with hashes and metadata.
7. Run automated output checks.
8. Display job status and downloadable output in the dashboard.

A second slice can add Blender headless rendering after the contract is stable.

## 10. Architecture decision gates

Do not freeze architecture until:
- the first target output is selected;
- target hardware is measured;
- candidate licenses are reviewed;
- one Motion Canvas render and one Blender render have been tested;
- the core contract can represent both without engine-specific fields leaking into the domain model.