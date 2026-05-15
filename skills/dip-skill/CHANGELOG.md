# Changelog

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
