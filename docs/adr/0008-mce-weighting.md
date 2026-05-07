# 0008 — MCE weighting scheme

**Status:** Open
**Date:** 2026-05-06

## Context

The Multi-Criteria Evaluation (MCE) collapses many normalized indicator layers into a single risk score per location. The weights we assign to each indicator largely determine which locations come out as "high-risk" — and therefore drive the project's central conclusions.

EJScreen alone has 13 environmental burden indicators and several community vulnerability indicators; we may layer in USGS seismic and water-stress indicators on top. Equal weights treat lead paint and PM2.5 as equally important; AHP weights require pairwise judgments; literature-derived weights require us to find and defend a specific paper.

## Decision

**Open.** Candidates:

1. **Equal weights across normalized indicators.**
   - *Pro:* simplest, no ad-hoc judgment.
   - *Con:* arguably treats incomparable indicators as equal; some EJScreen burdens are clearly more health-impactful than others.

2. **Equal weights within categories (environmental, community, sensitivity), with category weights set by the team.**
   - *Pro:* makes the team's value judgments explicit at the category level only.
   - *Con:* still smuggles equal-within-category assumptions in.

3. **AHP (Analytic Hierarchy Process).**
   - *Pro:* canonical in MCE literature; produces a defensible weight vector from pairwise comparisons.
   - *Con:* requires the team to do the comparisons; introduces our own values.

4. **Literature-derived weights from EJ scholarship.**
   - *Pro:* externalizes the value judgment.
   - *Con:* requires identifying and defending a specific source; few studies use the exact indicator set we'll have.

## Mandatory regardless of choice

- **Sensitivity analysis.** Run the full pipeline with at least two weighting schemes (e.g., equal + AHP). Report whether the high-risk classification is stable across them. If results flip materially, that itself is a finding.

## Consequences (when decided)

- Frames how the team explains "high-risk" in the final report — as a value-laden definition the team owns explicitly, not as an objective measurement.
- Sensitivity analysis becomes a non-negotiable section of the report.
