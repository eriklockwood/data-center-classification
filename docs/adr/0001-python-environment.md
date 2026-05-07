# 0001 — Python environment manager

**Status:** Accepted
**Date:** 2026-05-06

## Context

This is a multi-person academic project running on a 7-week schedule. Onboarding friction matters — every minute a teammate spends fighting their environment is a minute not spent on the actual research. We also need a deterministic lockfile so that "works on my machine" disagreements between teammates can be resolved against a shared baseline.

Candidates considered:

- **uv** — a fast, single tool that handles Python install, virtualenv, dependency resolution, and lockfile generation. Driven by `pyproject.toml`. Becoming the default in modern Python tooling.
- **Poetry** — mature, also `pyproject.toml`-based, well-known on academic teams. Slower than uv; resolver historically has had edge cases.
- **pip + requirements.txt** — universally familiar, but no lockfile by default and weaker reproducibility.
- **conda / mamba** — common in geospatial because GDAL ships as a binary, side-stepping C-library headaches. Heavier install, slower, and config tends to drift.

## Decision

We use **uv** for Python install, environment management, and dependency resolution. The single source of truth for dependencies is `pyproject.toml`; the lockfile is `uv.lock` and is committed to the repo.

## Consequences

- One tool to install per teammate (`curl -LsSf https://astral.sh/uv/install.sh | sh`), then `uv sync` produces an identical environment for everyone.
- We avoid conda's binary distribution. If a pure-Python wheel for any geospatial dependency is unavailable on a teammate's platform, we revisit (likely fall back to system GDAL or switch that dep to conda just for that lib).
- Adding a new dependency: `uv add <pkg>`. Adding a dev tool: `uv add --dev <pkg>`. The lockfile is updated automatically.
- The `[project.scripts]` entry point feature is available if we want CLI commands later.
