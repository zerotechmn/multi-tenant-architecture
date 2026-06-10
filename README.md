# Multi-Tenant Architecture

Architecture documentation for Zerotech's multi-tenant platform initiative.

## Live site

After GitHub Pages is enabled, the docs are published at:

**https://zerotechmn.github.io/multi-tenant-architecture/**

## Edit the docs

Source files:

- [`docs/index.md`](docs/index.md) — main architecture doc
- [`docs/where-we-are-today.md`](docs/where-we-are-today.md) — current-state baseline

## Preview locally

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Open http://127.0.0.1:8000

## Deploy

Pushes to `main` trigger the [GitHub Actions workflow](.github/workflows/pages.yml).

**One-time setup** in the GitHub repo:

1. Go to **Settings → Pages**
2. Set **Source** to **GitHub Actions**
