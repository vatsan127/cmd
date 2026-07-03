# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project Overview

Personal DevOps/engineering cheat sheet — a collection of Markdown reference files
(commands and setup guides) rendered as a documentation site with **MkDocs Material**
and published to GitHub Pages. Not a software application.

Site: <https://vatsan127.github.io/cmd/>

## Project structure

```
cmd/
├── README.md                 ← repo intro (structure + setup + run)
├── CLAUDE.md                 ← this file
├── mkdocs.yml                ← site config: theme, nav, Markdown extensions
├── .gitignore                ← excludes .venv/, site/, .env
├── docs/                     ← single source of truth for all notes
│   ├── index.md              ← landing page
│   ├── setup/                ← one-time install/config guides
│   │   ├── server.md         ← Java 21, Maven, Git, Docker, PostgreSQL 17
│   │   └── kafka.md          ← Confluent Kafka 7.7 (KRaft) setup
│   ├── commands/             ← day-to-day command references
│   │   ├── linux.md
│   │   ├── git.md
│   │   ├── docker.md
│   │   ├── kubernetes.md
│   │   └── kafka.md
│   └── stylesheets/extra.css ← full-width layout override
├── postgres/                 ← PostgreSQL reference + sample DB dump (NOT yet migrated to docs/)
├── .github/workflows/        ← deploy-docs.yml: auto-build + publish to GitHub Pages
├── .venv/                    ← gitignored; MkDocs Material lives here
└── site/                     ← gitignored; mkdocs build output
```

Content is organised **Setup first, then Commands**. The `postgres/` folder is
intentionally left at the repo root for now and is not part of the site build.

## Commands

Assume the venv at `.venv/`:

```bash
# Live dev server, hot reload → http://127.0.0.1:8000/cmd/
.venv/Scripts/python.exe -m mkdocs serve

# Static build to site/
.venv/Scripts/python.exe -m mkdocs build

# Strict build (fail on warnings — run before publishing)
.venv/Scripts/python.exe -m mkdocs build --strict
```

Recreate the venv if `.venv/` is lost:

```bash
py -m venv .venv
.venv/Scripts/python.exe -m pip install --upgrade pip mkdocs-material
```

## Deployment

The site auto-deploys to GitHub Pages via `.github/workflows/deploy-docs.yml`.
Every push to `master` triggers a GitHub Actions run that installs
`mkdocs-material`, runs `mkdocs build --strict`, and publishes the result to
<https://vatsan127.github.io/cmd/>. No manual step and no `gh-pages` branch — the
built site is uploaded straight to Pages as an artifact. The workflow can also be
run by hand from the repo's Actions tab (`workflow_dispatch`).

One-time setup (done once in the GitHub repo UI): Settings → Pages → Build and
deployment → Source = "GitHub Actions".

## Notes file conventions

All notes live under `docs/` as `.md` files.

- **Title:** each page starts with a single `# Title` heading.
- **Sections:** `## Heading`, `### Sub-heading`. Sections separated by `---`.
- **Command entries:** a one-line plain-English description above each fenced block.
- **Code fences:** always tag the language — `sh`/`bash` for shell, `sql` for SQL,
  `ini` for config/unit files. No bare fences (they lose syntax highlighting).
- **Placeholders:** `<angle_brackets>` for values the reader replaces.
- **Nav:** register new pages in `mkdocs.yml` under `Setup` or `Commands`.

## Keep this file current

When you make a structural change to the repo, **register it in this file in the
same change** — treat `CLAUDE.md` as part of the deliverable. Structural changes
include: adding/removing/renaming/moving files or folders (update the structure
tree); changing the docs conventions; changing the MkDocs setup, venv recipe, or
commands.

## Things to avoid

- Don't commit secrets. API keys / passwords belong in `.env` (gitignored).
- Don't create empty placeholder folders before they are actually needed.
- Don't commit the `.venv/` or `site/` directories (both gitignored).
