# 0004 — Data storage strategy

**Status:** Deferred
**Date:** 2026-05-06

## Context

Geospatial datasets can be large. EJScreen alone ships as a multi-GB block-group file. Once we add raster sensitivity layers, the volume grows quickly. The team needs to share datasets reproducibly, but it's premature to lock in a system before we know:

- How large the data actually is in practice.
- Whether teammates need pinned canonical snapshots, or are fine re-downloading from sources.
- Whether we'll have access to a shared cloud bucket (S3 / GCS) for any backend.

## Decision

**Deferred.** For now: `data/` is gitignored except for `.gitkeep` markers, and `data/README.md` documents source URLs so any teammate can rebuild their local copy.

Options to revisit:

- **Status quo (gitignore + README pointers).** Cheapest. Works as long as sources stay live, downloads are tractable, and we don't need byte-identical reproducibility.
- **DVC (Data Version Control).** Versions data alongside git. Needs a remote backend (S3, GCS, Azure Blob, or DVC's own free tier). Highest reproducibility, most setup overhead.
- **Git LFS.** Built into GitHub. Counts against repo storage quota; works for moderate-size files. Can be awkward to undo.
- **GitHub Releases as snapshot tarballs.** Manual but durable. We could publish a "data-snapshot-vN.tar.gz" release any time we want to pin a state.

Trigger to revisit: (a) a teammate hits a reproducibility need (e.g., "the OSTI atlas got updated and our results don't match anymore"); or (b) someone times themselves rebuilding from scratch and it's painful.

## Consequences

- Today: zero infrastructure cost, fast onboarding once data sources are documented.
- Risk: source URLs change, teammates accidentally use slightly different download dates, or a dataset is taken down.
- Mitigation while deferred: when a teammate downloads a dataset, note the access date in a comment in the relevant notebook or processing script, and consider taking a checksum.
