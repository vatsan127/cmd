# Command Reference

A personal DevOps/engineering cheat sheet — the commands and setup steps I reach
for often, in one place. Written as a documentation site (MkDocs Material) and
published to GitHub Pages.

📖 **Read it live:** <https://vatsan127.github.io/cmd/> — source under [`docs/`](docs/).

## Project structure

```
cmd/
├── README.md          # This file
├── CLAUDE.md          # Guidance for Claude Code
├── mkdocs.yml         # Site config (theme, nav, extensions)
├── docs/              # All notes (single source of truth)
│   ├── index.md           # Landing page
│   ├── setup/             # One-time install/config guides
│   │   ├── server.md          # Java 21, Maven, Git, Docker, PostgreSQL 17
│   │   └── kafka.md           # Confluent Kafka 7.7 (KRaft) setup
│   ├── commands/          # Day-to-day command references
│   │   ├── linux.md
│   │   ├── git.md
│   │   ├── docker.md
│   │   ├── kubernetes.md
│   │   └── kafka.md
│   └── stylesheets/extra.css  # Full-width layout override
├── postgres/          # PostgreSQL reference + sample DB dump (not yet in the site)
├── .venv/             # Python virtualenv (gitignored)
└── site/              # mkdocs build output (gitignored)
```

## Setup

Create the virtualenv and install MkDocs Material (one-time):

```bash
py -m venv .venv
.venv/Scripts/python.exe -m pip install --upgrade pip mkdocs-material
```

## Run

```bash
# Live dev server with hot reload → http://127.0.0.1:8000/cmd/
.venv/Scripts/python.exe -m mkdocs serve

# Static build to site/
.venv/Scripts/python.exe -m mkdocs build
```

## Deploy

Pushing to `master` triggers `.github/workflows/deploy-docs.yml`, which builds the
site and publishes it to GitHub Pages. One-time repo setting: **Settings → Pages →
Source = "GitHub Actions"**.
