# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Intel Gaudi-specific fork of the [AgentOps Observability with Red Hat AI](https://github.com/rhpds/agentops-in-prod-showroom) Showroom lab. This version targets Intel Gaudi 3 AI accelerators running `qwen3-14b` via vLLM (the upstream uses `gpt-oss-120b`). Module 5 (Agent & LLM Evaluations) has been removed from navigation but the source file (`07-module-05-evals.adoc`) is preserved for potential future use.

Rendered site: https://rhpds.github.io/agentops-in-prod-showroom (upstream — this fork deploys via the same GH Pages workflow)

## Build & Preview

```bash
# Local preview with live reload (Podman)
podman run --rm --name antora -v $PWD:/antora -p 8080:8080 -i -t ghcr.io/juliaaano/antora-viewer

# SELinux systems — append :z
podman run --rm --name antora -v $PWD:/antora:z -p 8080:8080 -i -t ghcr.io/juliaaano/antora-viewer

# Manual Antora build (no server)
npx @antora/cli@3.1 --fetch site.yml
# Output goes to ./www/
```

No test suite or linter — validation is visual via the Antora preview.

## Architecture

This is an [Antora](https://antora.org) site using the [RHDP Showroom theme](https://github.com/rhpds/rhdp_showroom_theme).

- `content/antora.yml` — component descriptor: title, nav pointer, and AsciiDoc attributes (version placeholders like `{user}`, `{password}`, `{user_project}` are substituted by Showroom at runtime)
- `content/modules/ROOT/nav.adoc` — left-sidebar navigation tree
- `content/modules/ROOT/pages/` — AsciiDoc lab content (numbered `01-` through `09-`)
- `content/modules/ROOT/assets/images/` — screenshots referenced by pages
- `content/supplemental-ui/` — theme overrides (CSS, JS, Handlebars partials)
- `site.yml` — Antora playbook for local/CI builds
- `.github/workflows/gh-pages.yml` — deploys to GitHub Pages on push to `main`
- `examples/` — Showroom template examples (demo/workshop), not part of the live lab

## Content Conventions (Showroom AsciiDoc)

- Source blocks intended for student copy-paste: use `[source,lang,role="execute"]`
- Image lightbox popout: use `link=self` (not `window=blank`)
- No trailing period after credential/URL examples
- No blank line after `====` admonition delimiter (breaks attribute substitution)
- Pre-render Mermaid diagrams as SVGs for split-panel readability
- Antora attributes like `{user}`, `{password}`, `{user_project}` are defined in `content/antora.yml` and replaced at runtime by the Showroom deployer

## Module Structure

| File | Title | Status |
|------|-------|--------|
| `01-overview.adoc` | Workshop Overview | Active |
| `02-details.adoc` | Workshop Details | Active |
| `intel-hardware.adoc` | Intel Hardware | Active |
| `03-module-01-agentic-app.adoc` | Module 1: The Agentic App | Active |
| `04-module-02-observability-pillars.adoc` | Module 2: Observability Pillars | Active |
| `05-module-03-metrics-kpis.adoc` | Module 3: Metrics & Logs | Active |
| `06-module-04-tracing-mlflow.adoc` | Module 4: Tracing & MLflow | Active |
| `07-module-05-evals.adoc` | Module 5: Evals | **Removed from nav** — kept as source |
| `08-module-06-dev-to-production.adoc` | Module 5: Dev to Production | Active (renumbered) |
| `09-conclusion.adoc` | Conclusion | Active |

## Intel Gaudi Differences from Upstream

- Model: `qwen3-14b` (not `gpt-oss-120b`)
- Hardware: Intel Gaudi 3 accelerators
- Added `intel-hardware.adoc` page
- Module 5 (Evals) removed from navigation
- Module 6 (Dev to Production) renumbered as Module 5 in nav
