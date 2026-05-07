# 0003 — Geographic scope

**Status:** Accepted
**Date:** 2026-05-06

## Context

The strongest data sources we have access to (EJScreen, OSTI IM3 atlas, Aterio Databricks Marketplace, USGS) are U.S.-only. The global map.datacente.rs dataset exists, but the social/environmental indicator coverage outside the U.S. is uneven, and mapping a comparable "EJScreen-equivalent" globally is a research project in its own right.

The team's bandwidth over Weeks 4–10 is limited. A clear scope keeps the analysis tractable and lets us cut deeper on a smaller area rather than producing a thinner global summary.

## Decision

The project's analysis scope is the **United States**. All MCE inputs, classification targets, and results are U.S.-only.

However, the codebase should not foreclose later expansion to global data. Specifically:

- Data ingestion modules should not hard-code U.S.-only assumptions where a more general implementation costs nothing extra.
- CRS handling should not assume CONUS-only (EPSG:5070 is fine for U.S. analysis, but utility code that handles arbitrary regions should accept a CRS argument).
- Joins should not assume FIPS-only spatial keys; geometry-based joins are preferred when feasible.
- Documentation should call out U.S.-specific data sources rather than burying the assumption in code.

## Consequences

- We get to use EJScreen's rich indicator set as the backbone of the social/environmental risk model.
- Comparisons with map.datacente.rs are out of initial scope, though we may use it as a sanity check for U.S. coverage.
- If a future iteration of the project expands to global, the data layer will need substantial new work; the modeling layer should mostly survive intact.
