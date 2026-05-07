# 0006 — Data center dataset selection

**Status:** Open
**Date:** 2026-05-06

## Context

The original concept doc names three U.S.-relevant data center datasets:

- **OSTI IM3 Open Source Data Center Atlas** (Mongird et al. 2025) — openly published, U.S. coverage.
- **Aterio.io — US Data Center Locations and Power Demand** (Databricks Marketplace) — listing-page indicates power demand metadata; license/terms need verification.
- **map.datacente.rs** — global; potentially useful as a sanity check or for later global expansion (out of initial scope per ADR 0003).

Each has different coverage, definitions, and metadata richness. We need to commit to a primary source — or to a deduplication / fusion strategy if we combine them.

The temporal analysis (pre/post-AI-expansion) is gated on having reliable **build/commission dates** with adequate coverage. If only one source has those at scale, it likely becomes our primary.

## Decision

**Open.** Working questions to answer in Week 5 EDA:

1. License and terms compatibility — can we use each in an academic project, redistribute derived results, etc.?
2. What fields does each carry — location precision, owner, build date, commission date, capacity (MW), facility type, status (operational vs planned)?
3. Date coverage — for each dataset, what fraction of records have a usable date?
4. Overlap — by spatial proximity, how many entities appear in more than one source?
5. Disagreements — when sources overlap, do they agree on attributes? Which is more recent?

Likely outcomes:

- Pick OSTI IM3 as the primary source for license simplicity; layer in Aterio metadata where it adds value (power demand, recent additions).
- Or, fuse via spatial deduplication and treat the union as the canonical set.

## Consequences (when decided)

- Determines the size of N for our analysis.
- Determines whether the temporal pre/post-AI analysis is feasible at all (ADR-pending) or has to be reframed.
- Affects feature engineering: we can only use power-demand features if they exist in the chosen source.
