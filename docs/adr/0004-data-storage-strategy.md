# 0004 — Data storage strategy

**Status:** Accepted (supersedes earlier "Deferred" status from 2026-05-06)
**Date:** 2026-05-08

## Context

Geospatial datasets can be large. EJScreen alone ships as a multi-GB block-group file. The original scaffold deferred this decision and gitignored `data/`, with each teammate downloading from documented source URLs.

In practice, the team has converged on a different approach: commit raw and processed datasets directly into the repo so every teammate has identical, immediately-usable data on clone. The teammate distribution we've observed includes a range of git/Python comfort levels, and the friction of "download these N datasets to these N paths before anything works" is real. For a 7-week academic timeline, removing that friction outweighs the costs.

## Decision

**Commit datasets to the repo.** `data/` is no longer gitignored. Raw, interim, and processed data files are tracked alongside code. Model artifacts and notebook outputs are also tracked alongside the notebooks that produce them — see consequences for caveats.

The earlier alternative options (DVC, Git LFS, GitHub Releases as snapshot tarballs) are off the table for this project's lifetime.

## Consequences

- **Onboarding is one step.** `git clone && uv sync` produces a fully reproducible environment with all data in place — no per-teammate downloads, no version drift.
- **Repo size grows over time.** This is the main cost. With current files (~5 MB total in the merged work) we are well below GitHub's 100 MB-per-file hard limit and far below the soft repo-size warning threshold (~1 GB). If a single dataset approaches 100 MB, we revisit.
- **Binary artifacts have known issues.** `*.pkl` files are sklearn-version-fragile and don't diff. Model artifacts will need to be regenerated when dependencies change. The team accepts this trade-off for now; if it becomes painful, switch to "regenerate from notebook" instead.
- **License responsibility.** Including third-party datasets in our repo means the dataset's license now binds the repo. `data/README.md` should record source + license for each tracked dataset; verify each is redistributable before adding new ones.
- **PII / sensitive content.** None of our current datasets are sensitive (all are public environmental/infrastructure data), but check before adding any new dataset.
