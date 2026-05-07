# 0005 — Spatial unit of analysis

**Status:** Open
**Date:** 2026-05-06

## Context

Data centers in our datasets are point locations. Most of our environmental and community indicators (EJScreen) are reported at the **block group** level. We need a defensible rule for attributing area-based indicators to a point — and the choice will materially shape the feature distributions and the final risk score.

The environmental justice literature offers no single canonical rule. Different studies use different buffers and units depending on the pollutant of interest, exposure pathway, and data resolution.

## Decision

**Open.** Options on the table:

1. **Containing block group.** Take the indicator value of the block group the data center sits inside. Simple, deterministic, no buffer parameter to defend.
   - *Pro:* matches EJScreen's native unit; no aggregation logic needed.
   - *Con:* a data center on the edge of a block group may have very different exposure than the block group's centroid suggests; ignores cross-boundary effects.

2. **Fixed-radius buffer (e.g. 1 km, 3 km, 5 km).** Aggregate indicators across all block groups intersecting the buffer, weighted by area of intersection.
   - *Pro:* captures spatial spillover; common in EJ literature.
   - *Con:* radius is a parameter that needs justification; values aggregate further when buffers cross many block groups.

3. **Multi-radius weighted aggregate.** Combine values at 1 km, 3 km, 5 km with declining weights.
   - *Pro:* resilient to single-radius arbitrariness.
   - *Con:* more parameters; harder to communicate.

## Considerations

- Whatever we pick, we should run a **sensitivity analysis** with at least one alternate rule and report whether results are stable across choices.
- Block-group geometry can be irregular; a small block group near a data center may not represent the local exposure if the center sits on the boundary.
- For data center *power* impacts (e.g., grid stress), the exposure radius is much larger than for local PM2.5 exposure. We may need different radii for different feature classes — flag in the eventual decision.

## Consequences (when decided)

- Locks in the spatial join logic in `src/data_center_classification/`.
- All downstream feature distributions, risk scores, and model accuracies are conditional on this choice — make sure the report calls this out.
