# Architecture Decision Records (ADRs)

We use lightweight ADRs (Michael Nygard format) to record significant decisions on this project. Each ADR captures **why** a decision was made — the constraints and trade-offs at the time — so future contributors can revisit decisions with full context.

## Format

Every ADR has four sections:

- **Status** — `Proposed` / `Accepted` / `Open` / `Deferred` / `Superseded by NNNN` / `Deprecated`.
- **Context** — what's going on, what problem we're solving, what constraints apply.
- **Decision** — the decision itself, or (for `Open` ADRs) the options on the table.
- **Consequences** — what becomes easier, harder, or different because of the decision.

## How to add a new ADR

```sh
cp docs/adr/template.md docs/adr/NNNN-short-slug.md
```

Where `NNNN` is the next zero-padded number after the highest existing ADR. Edit the new file, then update the index below in the same commit.

## Index

| # | Title | Status |
|---|-------|--------|
| [0001](0001-python-environment.md) | Python environment manager | Accepted |
| [0002](0002-gis-stack.md) | GIS stack | Accepted (top-level); Open (sub-decisions) |
| [0003](0003-geographic-scope.md) | Geographic scope | Accepted |
| [0004](0004-data-storage-strategy.md) | Data storage strategy | Deferred |
| [0005](0005-spatial-unit-of-analysis.md) | Spatial unit of analysis | Open |
| [0006](0006-data-center-dataset.md) | Data center dataset selection | Open |
| [0007](0007-classification-target.md) | Classification target and label strategy | Open |
| [0008](0008-mce-weighting.md) | MCE weighting scheme | Open |
