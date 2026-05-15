# dip-skill

`dip-skill` is a Codex skill that helps configure local development environments with [`dip`](https://github.com/bibendi/dip).

## What this skill can do

- Detect the current project tech stack from repository files.
- Apply stack-specific setup recipes for `dip`-based development.
- Bootstrap or update `dip` configuration files (`dip.yml`, compose files, Dockerfiles) with minimal, safe changes.
- Provide ready-to-run `dip` commands for setup, shell access, tests, and linting.
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
- `Use dip-skill to setup dip for this Django app.`
- `Use dip-skill to detect stack and prepare dip commands for development.`
