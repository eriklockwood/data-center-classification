# Data

Datasets are tracked directly in this repo so every teammate has identical, immediately-usable data on clone. See [ADR 0004](../docs/adr/0004-data-storage-strategy.md) for the rationale and limits (most importantly: don't add files larger than ~50 MB without discussing).

## Subdirectories

- `raw/` — source files exactly as downloaded. **Do not edit in place.**
- `interim/` — partially processed intermediates (e.g. cleaned, joined, reprojected).
- `processed/` — analysis-ready datasets that feed models or notebooks directly.

## Sources

| Dataset | Use | Source |
|---------|-----|--------|
| OSTI IM3 Open Source Data Center Atlas (Mongird et al. 2025) | U.S. data center locations | https://www.osti.gov/biblio/2550666 |
| Aterio.io — US Data Center Locations and Power Demand | U.S. locations + power demand | https://marketplace.databricks.com/details/79b0642c-9b22-4922-a94e-480d8aa41e51/aterioio_US-Data-Center-Locations-and-Power-Demand |
| map.datacente.rs | Global infrastructure (out of initial scope; reserved for later) | https://map.datacente.rs/ |
| EPA EJScreen v2.3 | Environmental burdens + community vulnerability indicators | https://www.epa.gov/ejscreen |
| EJScreen technical documentation v2.3 | Indicator definitions | https://www.epa.gov/system/files/documents/2024-07/ejscreen-tech-doc-version-2-3.pdf |
| FracTracker U.S. Data Centers Tracker | Cross-reference / validation | https://www.fractracker.org/2026/04/open-u-s-data-centers-tracker/ |
| USGS seismic zones | Environmental sensitivity layer (MCE input) | TBD — pin a specific dataset |
| Water-stressed basins | Environmental sensitivity layer (MCE input) | TBD — candidate sources include WRI Aqueduct |

The "Industry feature set" sources (industrial electricity prices, tax incentive presence, electricity-market deregulation, state/county moratoria, cluster density) are still under investigation. Track findings in ADR 0006 or open a new ADR when sources are picked.

## Conventions

- Filenames in `interim/` and `processed/` should encode source + date: `osti-im3_2025-06-06_us-data-centers.parquet`.
- Prefer Parquet over CSV for tabular intermediates and GeoParquet over Shapefile/GeoJSON for spatial intermediates (smaller, faster, types preserved).
- Don't add files larger than ~50 MB without discussing — GitHub warns at 50 MB and rejects pushes over 100 MB.
