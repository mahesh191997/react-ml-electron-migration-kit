# Migration plan

Status: **Template — inspect this repository before filling it in.**

## Baseline inventory

| Topic | Actual finding | Evidence (file / command) |
| --- | --- | --- |
| React framework, scripts and build output | TBD | TBD |
| Inference runtime and entrypoint | TBD | TBD |
| Model files, formats, licenses and sizes | TBD | TBD |
| Input decoding, preprocessing and output schema | TBD | TBD |
| Existing UI workflow and error handling | TBD | TBD |
| Sample images and baseline output/evaluation | TBD | TBD |
| Windows and hardware requirements | TBD | TBD |

## Architecture decision

- Electron main/window lifecycle: TBD
- Preload API and typed IPC contract: TBD
- Inference worker/process and resource lifetime: TBD
- Image transport (path vs bytes; lifetime and size limits): TBD
- Development vs packaged paths for assets and model: TBD
- Offline/install strategy and supported Windows architecture: TBD
- Packaging tool and scripts: TBD

Explain the alternatives considered **from the actual repository** and why the selected design fits. If inference is already in browser, verify whether it can stay there safely and performantly before adding a new service. If Python is required, establish a reliable local executable/environment provision and avoid requiring end users to configure Python manually unless explicitly accepted.

## Milestones

- [ ] M0: Baseline capture: clean or documented git status, working web app, sample inputs, expected outputs.
- [ ] M1: Electron launches the existing React UI in development and from compiled assets; safe window and preload bridge.
- [ ] M2: Inference works through chosen desktop path; progress, cancellation/timeout, failures and worker shutdown handled.
- [ ] M3: Production packaging includes or locates every required runtime/model/asset; documented Windows installer/portable artifact.
- [ ] M4: Automated checks and manual representative image comparison complete; Windows launch and offline smoke test complete (or explicitly blocked by platform).

## Acceptance criteria

- [ ] From a fresh checkout, documented commands install dependencies and launch desktop development build.
- [ ] Documented commands create the intended local Windows package; packaged app starts independently of dev server.
- [ ] Same representative images yield equivalent outputs to baseline within stated numerical or visual tolerance; evaluation report notes exact metric and threshold.
- [ ] Invalid/corrupt input produces a user-visible error; repeated jobs do not leak worker processes; quit closes worker.
- [ ] Security checks confirm no renderer Node integration, broad IPC passthrough, remote private-image upload, or arbitrary external navigation.
- [ ] Readme/build docs state system requirements, how models are supplied, package size, and known limitations.

## Risks / decisions requiring owner input

Record only genuine blockers and concrete evidence. If a choice depends on unavailable proprietary model files or expected output, complete independent work and specify the exact missing artifact. Never invent performance/equivalence numbers.
