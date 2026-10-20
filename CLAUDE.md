# Repository Instructions

## Scope

These instructions apply to the entire `dip-skill` repository.

## About This Skill

`dip-skill` is a dual-purpose skill that works with both **Claude Code** and **Codex**. The skill content lives in `skills/dip-skill/SKILL.md` and uses a shared format (YAML frontmatter + Markdown body) understood by both AI systems.

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

Then run these commands from the repo root to validate and install the skill locally for Claude Code:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./skills/dip-skill
rm -rf ~/.claude/skills/dip-skill
cp -R ./skills/dip-skill ~/.claude/skills/dip-skill
```

This installs the updated skill into Claude Code's local skill directory so the current revision is active immediately. Run this after every change to this repository.

> **Note:** To also sync for Codex in the same session, see `AGENTS.md` for the Codex sync command.

> **Development-only:** This sync step is a local-development convenience for testing the current revision as an unpacked skill copy. It is not part of the skill's runtime behavior — `skills/dip-skill/SKILL.md` must never instruct the running skill to reinstall, update, or copy itself. End users who install `dip-skill` via the Claude Code plugin marketplace (see `README.md`) do not need to run this and get updates through the normal plugin update mechanism instead.

## Mandatory Commit Policy

In this repository, commit every change as soon as it's made — do not batch multiple unrelated changes into one commit, and do not wait for the user to ask for a commit.

- After completing each discrete change (e.g., editing `SKILL.md`, bumping `VERSION`, updating `CHANGELOG.md`, updating `README.md`), stage and commit it before moving on to the next unrelated change.
- A single logical task (e.g., "add instruction X" which touches `SKILL.md` + `VERSION` + `CHANGELOG.md` together) may be committed as one commit, since those files change together under the versioning rule above.
- Write concise commit messages describing what changed and why.
- This overrides the general default of only committing when explicitly asked — in this repository, committing after each change is the explicit, standing instruction.
