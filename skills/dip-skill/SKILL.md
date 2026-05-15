# dip-skill

Use this skill to configure or update a project's local development environment with `dip` (`https://github.com/bibendi/dip`).

## Core behavior

1. Detect the current tech stack.
2. Select and execute the matching recipe.
3. Keep changes minimal and aligned with existing project conventions.

## Stack detection rules

Inspect repository files in this order:

1. **Ruby on Rails**
   - `Gemfile` includes `gem "rails"` (or equivalent)
   - `config/application.rb` exists
2. **Node.js**
   - `package.json` exists
3. **Django**
   - `manage.py` exists, or
   - `pyproject.toml` / `requirements*.txt` contains `django`
4. **Python (non-Django)**
   - `pyproject.toml`, `requirements.txt`, or `setup.py` exists
5. **Unknown**
   - None of the above patterns match

If multiple stacks match, prioritize framework-specific recipes (`Rails`, `Django`) over generic ones.

## Mandatory Rails handoff

If the project is Ruby on Rails, do **not** continue with this skill recipes.  
Respond with:

- A clear recommendation to use `tramway-skill` instead:  
  `https://github.com/Purple-Magic/tramway-skill/`
- A short reason: it is purpose-built for Rails and provides better Rails-specific workflows.

## Recipe execution policy

- Prefer updating existing `dip.yml` / compose files over replacing them.
- Reuse existing service names and ports when possible.
- Avoid destructive edits.
- After changes, provide exact `dip` commands for provisioning and daily workflow.

## Recipe: Node.js

Apply when `package.json` is present and Rails/Django are not detected.

Target files (create if missing):

- `docker-compose.yml` (or merge into existing compose file)
- `Dockerfile.dev`
- `dip.yml`

Recommended defaults:

- Service name: `app`
- Working dir: `/app`
- Bind mount project directory
- `node_modules` Docker volume
- Container command for dev server if script exists, otherwise idle command

`dip.yml` command set should include:

- `provision`: install dependencies (`npm ci` or package-manager equivalent)
- `shell`: open shell in app service
- `npm`: pass-through package manager command
- `test`: run project tests
- `lint`: run project linter if configured

## Recipe: Django

Apply when Django is detected and Rails is not detected.

Target files (create if missing):

- `docker-compose.yml` with:
  - `web` service for Django app
  - `db` service (PostgreSQL) when project requires database
- `Dockerfile.dev`
- `dip.yml`

Recommended defaults:

- `web` command: `python manage.py runserver 0.0.0.0:8000`
- Code mounted into container
- Persistent volume for database data

`dip.yml` command set should include:

- `provision`: install Python dependencies and run migrations
- `shell`: shell in `web`
- `manage`: pass-through to `python manage.py`
- `test`: run Django tests (`python manage.py test`)

## Recipe: Generic Python (non-Django)

Configure `dip` for dependency install, shell, and tests using project's package manager and test tooling.

## Unknown stack behavior

If no known stack is detected:

- Explain what was checked.
- Ask the user which stack to target.
- Offer to scaffold a minimal generic `dip` setup once stack is confirmed.

## Output format to user

Always include:

1. Detected stack and evidence.
2. Files created/updated.
3. Exact commands to run next (for example: `dip provision`, `dip up`, `dip test`).
4. Any assumptions requiring user confirmation.
