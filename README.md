# data-center-classification

A Python research project that classifies U.S. data center sites by social and environmental risk, and assesses whether siting outcomes have shifted with the post-AI-expansion build-out.

## Team resources

- **Shared Google Drive folder:** https://drive.google.com/drive/u/2/folders/1UyQb-bjZbXkOb3IvpeAtjM8R708Km6kk — concept docs, deliverables, references, anything not appropriate for the repo.

## What this project does

We construct two parallel scoring frameworks and compare them against where data centers have actually been built:

1. **Risk score** — a GIS-based Multi-Criteria Evaluation (MCE) combining EPA EJScreen environmental burdens, EJScreen community vulnerability indicators, and environmental sensitivity layers (USGS seismic zones, water-stressed basins).
2. **Industry-friendliness index** — industrial electricity prices, tax incentives, deregulation status, state/county moratoria, and existing data center cluster density.

Real siting decisions are then evaluated against both, and we look at how this relationship has shifted over time as AI infrastructure demand has grown.

The framework is meant to be a transparent, reproducible accountability benchmark — not a model of corporate decision-making.

## Scope

- **Geography:** U.S.-only for now. Architecture should not foreclose later expansion to global data (see [ADR 0003](docs/adr/0003-geographic-scope.md)).
- **Tooling:** pure-Python open-source GIS stack (no ArcGIS dependency).

## Getting started

This project uses [uv](https://docs.astral.sh/uv/) for environment and dependency management.

```sh
# 1. Install uv (one-time, per machine)
curl -LsSf https://astral.sh/uv/install.sh | sh

# 2. Clone and sync
git clone <repo-url>
cd data-center-classification
uv sync

# 3. Run Jupyter
uv run jupyter lab
```

Verify the install:

```sh
uv run python -c "import data_center_classification; print(data_center_classification.__version__)"
```

## Repository layout

```
data/         # gitignored; download instructions in data/README.md
docs/adr/     # architecture decision records
notebooks/    # exploratory notebooks (NN-author-topic.ipynb)
src/          # importable package (data_center_classification)
tests/        # pytest tests
```

## Design decisions

Open and accepted decisions are tracked as ADRs in [`docs/adr/`](docs/adr/). Most early-project decisions are intentionally left open — see the index for status.

## Project schedule

Seven-week academic timeline (Weeks 4–10):

| Week | Focus | Deliverable |
|------|-------|-------------|
| 4 | Research concept and feasibility | Research Proposal (Zoë) |
| 5 | Lit review, scope narrow, demographic enrichment, data cleanup, model scaffolding | — |
| 6 | Initial training, first-pass validation, preliminary results | Project Plan & Preliminary Results (Erik) |
| 7 | Model refinement, group sanity check, second-pass eval | — |
| 8 | Final analysis, retrospective, draft report | Project Report draft |
| 9 | Feedback incorporation, slide deck, reproducibility materials | — |
| 10 | Final dry-run | Presentation of Findings (group) |

## Data sources

See [`data/README.md`](data/README.md) for the full list. Primary sources include OSTI's IM3 Open Source Data Center Atlas, Aterio.io's data via the Databricks Marketplace, EPA EJScreen v2.3, and USGS environmental sensitivity layers.
