# dip-skill

`dip-skill` is a Codex skill that helps configure local development environments with [`dip`](https://github.com/bibendi/dip).

## What this skill can do

- Detect the current project tech stack from repository files.
- Apply stack-specific setup recipes for `dip`-based development.
- Bootstrap or update `dip` configuration files (`dip.yml`, compose files, Dockerfiles) with minimal, safe changes.
- Put newly created supporting development configuration files under `.dockerdev/` while keeping `dip.yml` at the repository root.
- Provide ready-to-run `dip` commands for setup, shell access, tests, and linting.
- Require a safety check that local development is not connected to production, staging, or other critical databases and resources.
- Require the target project's `README.md` to document Dip installation and the exact `dip` commands implemented by the skill.
- Configure Next.js projects with local Supabase/PostgREST-style services so a fresh checkout can run through `dip provision`.
- If the project is **Ruby on Rails**, it recommends using [`tramway-skill`](https://github.com/Purple-Magic/tramway-skill/) instead.

## Installation

Install using Codex `skill-installer` from:

`https://github.com/kalashnikovisme/dip-skill/tree/main/skills/dip-skill`

Example:

```bash
codex "Use the skill-installer skill to install https://github.com/kalashnikovisme/dip-skill/tree/main/skills/dip-skill"
```

Then restart Codex.

## Usage

Ask Codex to use this skill when you want to setup or update a `dip` environment in a project.

Example prompts:

- `Use dip-skill to configure this Node.js project with dip.`
- `Use dip-skill to dipize this Next.js + Supabase app so dip provision starts everything.`
- `Use dip-skill to setup dip for this Django app.`
- `Use dip-skill to detect stack and prepare dip commands for development.`

## Critical-resource safety check

Before the skill runs or documents mutable commands such as provisioning, migrations, seeds, resets, queue workers, or sync jobs, it must check that the development environment uses local containers, local emulators, or local-only placeholder credentials. It must stop and report the risky file, key, or command if it finds production, staging, shared, or unknown databases and external resources.

## Configuration location

When this skill creates new development configuration, it must keep `dip.yml` at the repository root and place supporting generated files under `.dockerdev/`, including `compose.yml`, `Dockerfile.dev`, local env templates, helper config files, and helper scripts. Commands for newly generated config use normal `dip` commands:

```bash
dip provision
```

## Implemented command documentation

When this skill creates or changes a project's `dip` workflow, it must also update that project's `README.md` with the commands it implemented. Depending on the detected stack and generated `dip.yml`, this can include:

- `dip provision` for first-time setup.
- `dip up` and `dip down` for starting and stopping services.
- `dip shell` for opening a container shell.
- Package-manager commands such as `dip npm`, `dip pnpm`, or `dip yarn`.
- Framework or database commands such as `dip next`, `dip manage`, or `dip psql`.
- Quality commands such as `dip test` and `dip lint` when they are configured.

## Dip installation documentation

When this skill creates or changes a project's `dip` workflow, it must also document how to install Dip on common operating systems:

- macOS: install with Homebrew.
- Linux: install with Homebrew on Linux or RubyGems.
- Windows: use WSL2, then follow Linux instructions inside WSL.
- Any OS with Ruby: install with `gem install dip`.
- Mention Dip releases as the source for precompiled binaries when package managers are not suitable.
