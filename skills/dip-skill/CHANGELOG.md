# Changelog

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
