# Repository Instructions

## Scope

These instructions apply to the entire `dip-skill` repository.

## End-of-Task Skill Sync

At the end of every task that changes this repository, update `skills/dip-skill/VERSION` before validation and sync.

Version rules:

- Use semantic versioning: `MAJOR.MINOR.PATCH`.
- Every repository-changing task must increase the version exactly once before validation and sync.
- If the skill has no version yet, create `skills/dip-skill/VERSION` with `0.1.0`.
- If the existing version is not full semantic versioning, normalize it first by treating missing components as `0`, then apply the required bump.
- Bump `PATCH` for wording, clarification, examples, and narrow bugfixes.
- Bump `MINOR` for new workflows, recipes, scripts, or materially expanded behavior.
- Bump `MAJOR` for breaking instruction changes or behavior reversals.
- Never leave `skills/dip-skill/VERSION` unchanged after modifying this repository.
- If the skill welcome/default prompt displays a version, keep it synchronized with `skills/dip-skill/VERSION`.
- Maintain `skills/dip-skill/CHANGELOG.md` for every version bump. Add a new entry for the new version and summarize what the user asked to change.
- When the user asks which version they are using, answer from `skills/dip-skill/VERSION` in the active skill copy.

Then run these commands from the repo root:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./skills/dip-skill
rm -rf ~/.codex/skills/dip-skill
cp -R ./skills/dip-skill ~/.codex/skills/dip-skill
```

This is a developer workflow requirement for local testing of the current skill revision in Codex.
