# STD — Integration and Delivery Surfaces

- Document: STD-INT-001
- Version: 0.1.0
- Status: Research proposal

## 1. One engine core, many clients

The rendering engine must not be duplicated in each delivery surface. Each surface submits a versioned job to the same control plane or worker API.

## 2. Delivery comparison

| Surface | Role | Strength | Constraint | Recommendation |
|---|---|---|---|---|
| Local CLI | Core execution interface | Offline, scriptable, testable | Requires terminal | Build first |
| Local desktop app | Project and render management | Full file access, preview and logs | Packaging and OS support | Build after CLI |
| Browser dashboard | Control plane and project UI | Cross-device interface | Browser should not own heavy render | Build as client |
| Browser extension | Capture references and submit jobs | Convenient web workflow | Limited filesystem and execution rights | Optional |
| Telegram bot | Submit jobs, track status, send previews/results | Easy remote control | Bot API file limits; bot is not compute | Optional client |
| GitHub Actions | CI, test, short render and packaging | Versioned automation | Hosted resource/time limits | Use for CI and bounded tasks |
| Self-hosted GitHub runner | Render on user's own machine | Local GPU/CPU and private assets | Machine must remain online | Useful optional worker |
| AppDeploy | Host dashboard/control plane | Shareable hosted UI | Not a replacement for local render hardware | Optional front end |
| Magnific Move | External code-driven motion service | Fast motion-graphic creation | Hosted service and account/credit constraints | Optional adapter |
| Magnific Spaces | Visual node workflow | Reusable visual orchestration | Hosted workspace and account access | Optional adapter |

## 3. Local CLI

Proposed commands:
- std doctor — report engine availability and versions.
- std project create — create a project manifest and asset folders.
- std engine list — show installed adapters.
- std job validate job.json — validate a job without rendering.
- std render job.json — execute locally.
- std job status ID — inspect progress.
- std artifact inspect PATH — read media metadata.
- std package PROJECT — collect source, manifests and output references.

## 4. Telegram bot

Telegram should be a thin control-plane client:
- /new create a project/job request;
- /render submit a validated job;
- /status inspect a job;
- /cancel request cancellation;
- /preview return a low-resolution preview;
- /result return artifact links or send small files.

Never run arbitrary user-provided code inside the bot process. Submit jobs to a local worker with allowlisted engine IDs and bounded resources.

Official Bot API documents ordinary bot uploads up to 50 MB and file downloads up to 20 MB. Running Telegram's local Bot API server increases upload capability to 2000 MB. Large masters should normally be returned as controlled download links or through a local Bot API server.

## 5. GitHub Actions

Use GitHub Actions for:
- lint, unit and contract tests;
- schema validation;
- engine-version checks;
- small deterministic reference renders;
- frame-count and media metadata checks;
- packaging and release artifacts;
- scheduled maintenance and documentation checks.

Do not assume a hosted runner is a cinema render farm. Long 3D renders, large caches and GPU workloads should use a self-hosted runner or dedicated worker. Store source and manifests in Git; store large generated media as workflow artifacts or external assets with explicit retention.

## 6. AppDeploy

Recommended role:
- host a React/Vite dashboard;
- display projects, engines, jobs, logs and artifacts;
- submit jobs to an explicitly configured worker endpoint;
- keep render binaries and project files on the worker, not inside the dashboard runtime.

A frontend-only AppDeploy app is suitable for a dashboard prototype. It does not by itself provide Blender, FFmpeg or GPU rendering on the user's local computer. A secure worker connection and network boundary must be designed separately.

No AppDeploy app has been deployed in this research phase.

## 7. Magnific adapter

Keep Magnific as an optional external adapter:
- Move create → code-authored motion graphics.
- Move status → version status and preview.
- Move render → MP4 export.
- Spaces list/run → reusable node workflows.
- Other image/video/audio operations must remain separately typed.

Before any paid or credit-consuming job:
- inspect account balance;
- inspect live model/tool catalog;
- estimate cost;
- ask for approval above the agreed budget threshold;
- never duplicate a pending paid job;
- preserve result IDs, provenance and output metadata.

The connected account reported zero credits, so no Magnific generation was run.

## 8. Integration security

- API tokens remain in secret storage and never enter Git or render logs.
- The bot and dashboard authenticate to the worker.
- Use job-level permissions and allowlisted adapters.
- Restrict filesystem access to approved project roots.
- Limit CPU, RAM, GPU, disk, execution time and network access.
- Validate uploaded files and inspect media metadata before processing.
- Public download links must be scoped and revocable.