# React ML → Electron migration kit

Extract the **contents** of this ZIP at the root of your existing React repository. This is a set of Claude Code instructions and agents; it does not contain your application or complete the migration by itself.

## Before extracting

1. Commit or back up your current work. If you already have `CLAUDE.md`, `.claude/settings.json`, or similarly named migration files, **merge them manually**; do not overwrite your project guidance. On Windows, inspect the archive before extracting: `tar -tf .\react-ml-electron-autonomous.zip`.
2. Open a terminal at the repository root (the directory containing `package.json`). Extract the ZIP there, without a new enclosing directory. Windows PowerShell: `tar -xf .\react-ml-electron-autonomous.zip -C .` (only after checking for filename collisions).
3. Check `git status` and review `.claude/settings.json`. Your existing build scripts, Python environment, model location and GLM provider are unknown; the agents must discover them.
4. Have the app's current inference working and keep a small, **non-sensitive** set of sample images plus expected outputs available locally. The agents should document where these are; do not commit model weights or patient data. Ensure Node/npm, a working build toolchain, and your local GLM 5.2 coding setup are already available. GLM 5.2 is the coding assistant here; your existing inference model can be different.

## Run

Install or update Claude Code according to its official instructions. From the repository root, start an interactive session to establish the baseline and review the plan:

```powershell
claude
```

Paste the text of `OVERNIGHT_PROMPT.md` (or tell Claude to read that file). Review `MIGRATION_PLAN.md`, especially acceptance criteria and any unresolved decisions. For an unattended run in PowerShell after you are satisfied with the scope:

```powershell
$promptText = Get-Content .\OVERNIGHT_PROMPT.md -Raw
claude -p $promptText --permission-mode auto --permission-prompts none
```

Requires a Claude Code version supporting `--permission-prompts none` (v2.1.259+), plus auto mode availability in your environment. If your GLM-backed Claude Code setup does not support auto mode, use a supported unattended mode with explicitly approved, narrow tool rules; do not assume this repository setting switches it on. Run the command in a terminal/session that stays alive, and leave the computer awake with enough disk space. CLI flags, organization rules, and provider capabilities may override project settings. The agent should log progress in `MIGRATION_PROGRESS.md`; one unattended invocation is not a guarantee it will finish overnight. Resume by repeating the same command after checking progress and git diff.

## What the kit asks the agents to do

1. Map the existing React app, inference path, assets, runtime, and build pipeline.
2. Decide the smallest safe Electron architecture and implement it incrementally.
3. Keep inference off the renderer, expose a narrow typed preload API, preserve the browser UX, and package a Windows desktop build.
4. Compare desktop inference with the existing app on representative images, run checks, document build/run instructions, and leave a concise handoff.

The orchestrator can invoke the project agents `repo-auditor`, `electron-integrator`, `inference-integrator`, `packaging-engineer`, and `qa-reviewer`. Their presence does not automatically launch a session. There is no repository-specific install command until the audit inspects your actual project.

## Safety and boundaries

- Treat input images, model paths, and inference output as local data unless the current app explicitly requires a service. Never upload private images or weights.
- No automatic `git push`, release publishing, installer signing, telemetry setup, credential changes, or destructive git operations.
- Do not disable Electron security controls or expose Node.js directly to renderer code. Keep original web code runnable during migration when feasible.
- If the repo has its own `CLAUDE.md`/settings, merge instructions carefully. For an existing `.claude/agents` directory, retain existing agents and resolve duplicate names.

## Files

`CLAUDE.md` orchestrates work; `MIGRATION_PLAN.md` is the plan template; `MIGRATION_PROGRESS.md` is the running log; `OVERNIGHT_PROMPT.md` starts or resumes the work; `.claude/settings.json` supplies project permissions; `.claude/agents/*.md` define specialist subagents.
