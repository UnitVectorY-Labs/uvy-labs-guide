# AGENTS.md

## What this repo is

Pure documentation site. No application code. Jekyll + [just-the-docs](https://just-the-docs.com/) theme, deployed to `guide.unitvectorylabs.com` via GitHub Pages.

## No local build

There are no build, test, lint, or codegen commands. GitHub Pages builds Jekyll automatically on push. Do not invent a build step.

## Adding/editing documentation

Content lives under `docs/` in five Jekyll collections:

| Directory | URL prefix |
|---|---|
| `docs/_bestpractices/` | `/bestpractices/*` |
| `docs/_javadevelopment/` | `/javadevelopment/*` |
| `docs/_tofudevelopment/` | `/tofudevelopment/*` |
| `docs/_uvyutilities/` | `/uvyutilities/*` |
| `docs/_projects/` | `/projects/*` |

Each file needs Jekyll front matter. Look at an existing file for the pattern (title, nav_order, parent, etc.).

## Internal links

Use Jekyll's `link` tag, not raw relative paths:

```liquid
{{ site.baseurl }}{% link _bestpractices/licenses.md %}
```

Raw relative paths will break if files move; `link` tags cause a build failure immediately, which is better.

## Version-bumping the Jekyll theme

Managed by [`repver`](https://github.com/UnitVectorY-Labs/repver). The `.repver` config at the repo root defines one command, `justthedocsversion`, which updates the theme version in `docs/_config.yml`, creates a branch, commits, pushes, and opens a PR via `gh`. Run it as:

```sh
repver justthedocsversion --version <new-version>
```

Do not manually edit the version string in `_config.yml` for a version bump — use `repver`.

## CI conventions

- All workflows run on `arc-runner-set` (self-hosted ARC runner), **not** `ubuntu-latest`.
- Every `uses:` reference must be pinned to a **full SHA hash** (not a version tag like `v4`). The `zizmor.yml` workflow scans for violations. Dependabot keeps SHA pins current.
- Use `pull_request_target` (not `pull_request`) for workflows that need permissions on external/Dependabot PRs (see `add-to-project.yml`).

## Mermaid diagrams

Mermaid v11.12.3 is enabled with a dark theme (`docs/_includes/mermaid_config.js`). Use standard fenced code blocks with `mermaid` as the language identifier.

## Organization-wide metadata (GitHub Custom Properties)

All repos must set these four custom properties: `project-status`, `programming-language`, `project-type`, `distribution`. The `project-status` value must match the README badge text exactly — automated tooling reads both.
