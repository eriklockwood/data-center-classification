# 0007 — Classification target and label strategy

**Status:** Open
**Date:** 2026-05-06

## Context

The concept doc describes "training classification models to predict the presence of data centers and to distinguish between low-impact and high-impact locations." There is a real methodological tension here that the team needs to resolve before model training begins:

If we **build "high-risk" labels from EJScreen indicators via MCE**, and then **train a classifier on EJScreen indicators to predict the label**, the classifier will achieve near-perfect accuracy by re-learning the MCE rule. The result is mechanically circular and doesn't tell us anything about siting decisions.

We need a target formulation where the label is genuinely separable from the features used to predict it.

## Decision

**Open.** Three candidate framings:

### A. Presence classifier + separate MCE risk score (compared post-hoc)

- **Target:** binary "is there a data center here?" at chosen spatial unit.
- **Features:** EJScreen + industry-friendliness features.
- **MCE risk score:** computed independently per location.
- **Analysis:** look at whether the presence classifier's predictions correlate with the MCE risk score, and whether the *gap* (high MCE risk × high industry-friendliness) is where data centers preferentially appear.

This avoids label leakage and matches the doc's "siting fits within the model" framing.

### B. High-risk-among-existing-data-centers as the target

- **Target:** for *existing* data centers only, classify as "high-impact" vs "low-impact" based on MCE risk.
- **Features:** industry-friendliness, build date, capacity, ownership — but **not** the EJScreen features used to compute the label.
- **Analysis:** what makes some data centers land in higher-risk areas than others?

Avoids leakage by rigorously excluding label-feeder features; smaller N (only data center sites).

### C. Both (A and B in parallel)

- Run both. Each answers a different sub-question; results are complementary.

## Open considerations

- Need to decide what "absent" means for framing A. Random U.S. locations? Block-group population centroids? Industrially-zoned parcels with no data center?
- The choice of negatives matters enormously for framing A; document the rationale.
- Framing B requires the underlying data center records to have enough non-EJScreen features to be predictively meaningful.

## Consequences (when decided)

- Defines the core training pipeline in `src/data_center_classification/`.
- Determines what counts as a positive result for the project's central question.
- Affects how we interpret feature importance — A and B answer different questions.
