# Autonomous migration run

You are in the root of my existing React image-inference repository. Migrate it into a Windows Electron desktop app according to `CLAUDE.md`. Read `README.md`, `MIGRATION_PLAN.md`, `MIGRATION_PROGRESS.md`, the repository files, and current git state first.

Proceed through the milestones independently. Use the project agents for focused audit, Electron, inference, packaging, and QA work where they help. Keep one owner for shared dependency files and integrate results. Update the plan with observed architecture, and append progress after each milestone. Make real code changes and run the relevant tests/builds. If a failure appears, debug it, fix it, and rerun the smallest meaningful check. Resume from completed work rather than starting over.

Use the local GLM 5.2 coding provider **only if this Claude Code environment already has it configured**; do not change credentials/provider configuration. The inference model used by the app may differ. Never upload private input images, model weights or patient data. Do not push to GitHub, publish releases, sign installers, overwrite unrelated changes, or use destructive git commands. If a required choice or proprietary input is unavailable, document the blocker precisely and complete independent milestones.

At the end, report actual changes, exact commands and outputs, the Windows package path if produced, inference comparison evidence, and any platform-dependent checks still pending. A passing build alone is not enough to claim the app works.
