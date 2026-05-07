# 0002 — GIS stack

**Status:** Accepted (top-level) / Open (sub-decisions)
**Date:** 2026-05-06

## Context

The project's central methodology is GIS-based: spatial joins between data center points and EJScreen polygon data, Multi-Criteria Evaluation overlays, zonal statistics, and Global Moran's I for spatial autocorrelation. The original concept doc described this in ArcGIS terms (ArcGIS Pro tools and ESRI workflows).

No teammate has an ArcGIS Pro license. Beyond cost, ArcGIS would also weaken the reproducibility deliverable in Week 9 — a grader without ArcGIS could not re-run the analysis.

## Decision

**Top-level:** the project uses an open-source pure-Python GIS stack. ArcGIS is not a dependency.

**Open sub-decisions** (revisit as the relevant analysis comes online):

- **Vector core:** geopandas + shapely + pyproj. *Already added to pyproject.toml.* Open: pin geopandas to 1.x major or stay flexible? geopandas 1.0 was a meaningful API shift.
- **Raster:** rasterio is the obvious choice if/when we need to handle raster layers (e.g., gridded environmental sensitivity products). Defer adding it until a teammate hits a raster task — reduces install footprint until then.
- **Spatial statistics (Moran's I, etc.):** PySAL ecosystem — likely `libpysal` + `esda` for autocorrelation, possibly `pointpats` for point-pattern checks. Add when Moran's I work begins.
- **Zonal statistics:** `rasterstats` is the conventional choice for raster-on-vector zonal stats. Add with rasterio.
- **MCE / weighted overlay:** likely roll our own with numpy/geopandas rather than adopting a heavyweight package — MCE is conceptually a weighted sum across normalized layers, which is a few lines of numpy.

## Consequences

- The whole pipeline can be run on a clean Linux machine in CI with `uv sync` plus a free Python install.
- We give up ArcGIS's GUI debugging affordances; visual sanity checks happen via Jupyter + matplotlib + folium instead.
- Some ArcGIS-native concepts (e.g., "Spatial Autocorrelation (Global Moran's I)" tool) translate cleanly to PySAL but the parameters and outputs are presented differently — anyone porting from an ArcGIS tutorial will need to translate.
- We will need to handle CRS choices ourselves (no ArcGIS auto-projection). Plan to standardize on a single equal-area projection (EPSG:5070, NAD83 / Conus Albers) for analysis layers; reproject visualization layers to Web Mercator only at display time.
