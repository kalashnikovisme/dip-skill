# Changelog

## 0.10.0

- Added a step to core behavior requiring the skill to report its own version (from `skills/dip-skill/VERSION`) and the installed `dip` version (`dip version`) at the start of work.

## 0.9.0

- Added a mandatory provisioning verification step: when a user asks to dipize or dockerize a project, the skill must actually run `dip provision` (and `dip up` when appropriate for the project) and iteratively diagnose and fix the configuration until the command succeeds, rather than stopping at generating files.

## 0.8.0

- Added Claude Code plugin marketplace support via `.claude-plugin/marketplace.json` at the repository root, pointing to `./skills/dip-skill`. No static `version` field is set in the marketplace entry so the plugin's update identity tracks the resolved Git commit SHA instead of duplicating the semantic version.
- Made Claude Code marketplace installation (`/plugin marketplace add` + `/plugin install`) the recommended installation method in `README.md`, with `claude plugin update` and marketplace auto-update documented for updating.
- Reclassified manual `cp -R` installation (for both Claude Code and Codex) as an explicit fallback in `README.md`, clearly noting it does not receive automatic updates.
- Documented in `CLAUDE.md` and `AGENTS.md` that the existing "end-of-task" `rm -rf` / `cp -R` sync steps are local-development conveniences only, and that `SKILL.md` must never instruct the running skill to reinstall or copy itself.
- No changes to skill recipe behavior.

## 0.7.0

- Added execution file detection: the skill now scans `bin/`, `scripts/`, and stack-specific locations for executable files and creates corresponding `dip` commands for each one found.
- Added a table of per-stack scan locations, rules for identifying executable files, naming conventions, and conflict-resolution guidance.
- Updated core behavior to list execution file detection as step 2.
- Updated the output format to report detected execution files and their mapped `dip` commands.

## 0.6.3

- Added mandatory source volume mounting rule: the project root must always be bind-mounted into every application container so developers can edit files locally without rebuilding the image.

## 0.6.2

- Added mandatory rule: never use `docker` or `docker compose` directly — all container operations must go through `dip` commands.

## 0.6.1

- Clarified `CLAUDE.md` sync instruction: emphasized it must run after every change and installs the skill into Claude Code's local skill directory.
- Updated `README.md` intro to state the skill works for both Codex and Claude Code with the same content.

## 0.6.0

- Made the skill dual-purpose: works with both Codex and Claude Code.
- Added `CLAUDE.md` with Claude Code-specific scope, versioning rules, and skill sync instructions.
- Updated `AGENTS.md` to describe the dual-system nature and cross-reference `CLAUDE.md`.

## 0.5.1

- Required helper scripts under `.dockerdev/scripts/` to use the project's main language with an executable shebang.

## 0.5.0

- Updated placement rules so `dip.yml` remains at the repository root while supporting development configuration files stay under `.dockerdev/`.
- Restored README command guidance to normal `dip` commands without `DIP_FILE`.
- Required README updates to describe Dip installation on common operating systems.

## 0.4.0

- Required newly created development configuration files and helper scripts to be placed under `.dockerdev/`.
- Standardized the generated Compose file path as `.dockerdev/compose.yml`.
- Updated command documentation guidance to use `DIP_FILE=.dockerdev/dip.yml` for generated configs.

## 0.3.0

- Added a mandatory critical-resource safety check so generated development workflows do not connect to production, staging, or other critical databases and services.

## 0.2.1

- Fixed `SKILL.md` metadata by adding required YAML frontmatter.
- Made README command documentation mandatory for projects changed by the skill.

## 0.2.0

- Added a Next.js + Supabase/PostgREST recipe focused on one-command `dip provision` onboarding.
- Documented Node 22, Next.js dev server, local Postgres/PostgREST, env-file, migration, and package-manager defaults.

## 0.1.0

- Initial release of `dip-skill`.
- Added stack detection flow and `dip` recipes for Node.js and Django projects.
- Added Ruby on Rails handoff to `tramway-skill`.
