# Repository instructions: React ML → Electron

You are migrating **this existing repository** into a Windows desktop application. First inspect the repository. Never assume the framework (Vite/CRA/Next), language, inference backend, model format, or packaging tool until confirmed in code. Follow existing project instructions and merge this file with any pre-existing `CLAUDE.md` guidance.

## Orchestration

1. Read `README.md`, `MIGRATION_PLAN.md`, `MIGRATION_PROGRESS.md`, `package.json`, and applicable project guidance. Check `git status` before editing; preserve user changes. Use `repo-auditor` to inventory actual files and identify the inference boundary, build commands, assets, dependency versions, and representative test path.
2. Fill `MIGRATION_PLAN.md` with observed facts, architecture decisions, risks, small milestones, and runnable acceptance criteria before broad changes. If architecture is uncertain, validate a small vertical slice first. Update `MIGRATION_PROGRESS.md` after each milestone and when blocked.
3. Delegate focused tasks to `electron-integrator`, `inference-integrator`, `packaging-engineer`, and `qa-reviewer` when useful. State exact file ownership for concurrent tasks; avoid concurrent edits to `package.json`, lockfiles, or config. Integrate their work yourself.
4. Implement, verify, and fix failures. Continue from the progress log on resume. Record exact commands, results and any untested items. Do not claim completion without a working packaged app and image inference parity, or mark it blocked with reproducible evidence.

## Technical constraints

- Main process handles app windows, dialogs and lifecycle. Renderer remains the React UI. Preload exposes only narrow, typed IPC methods for the required operations. Enable `contextIsolation`, disable `nodeIntegration`, use sandbox where compatible, validate IPC inputs and file paths, and limit navigation/external URLs.
- Keep expensive ML work out of the renderer and main event loop. Choose an inference bridge based on the repository: local Python subprocess/service, Node native runtime, or in-renderer ONNX/WebAssembly only if already justified. Define a startup/ready/timeout/error/shutdown contract; avoid arbitrary shell interpolation.
- Preserve model resolution in both development and packaged paths. Treat large weights as external or packaged resources deliberately; document installer footprint, platform architecture, license, and update strategy. No network transfer of private data.
- Preserve image orientation, preprocessing, normalization, output format, thresholds and postprocessing (including masks/boxes) when comparing results. Surface errors in the UI and log diagnostics without logging private image contents.
- Prefer minimally invasive changes. Keep browser and desktop scripts distinct where possible. Do not guess API behavior; inspect real implementations. Avoid unrelated refactors.
- Do not push, publish, sign, delete user data, reset branches, modify credentials, or commit images/weights without explicit authorization. You may install dependencies and produce local build artifacts as needed; record what changed.

## Completion

Verify development launch, production build, packaged Windows launch where the environment permits, inference on representative inputs, repeated requests, invalid input, app close/restart and offline operation. If running on another OS, explicitly leave native Windows launch verification pending. Summarize changes, test evidence, build path, and remaining risks in `MIGRATION_PROGRESS.md`.
