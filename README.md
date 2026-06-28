# Port Adelaide — Coastal Inundation Assessment (Sea-Level Rise 2100)

Interactive web map assessing coastal inundation exposure for Port Adelaide / inner Gulf St Vincent, South Australia, under a +1.0 m sea-level-rise scenario (2100).

**[→ Open the interactive map](https://alberto98gallodot.github.io/PORTFOLIO/coastal-flooding/)**

## Overview

Low-lying coastal and reclaimed land within the City of Port Adelaide Enfield is among South Australia's most sea-level-rise-exposed areas. The Port River is a tidal estuary governed by sea level rather than catchment runoff, making the area's flood regime fundamentally coastal. This assessment maps the inundation extent, exposed buildings, and affected planning zones for the 2100 scenario.

## Methodology

Bathtub inundation model with hydraulic connectivity correction:

- **Source DEM:** 1 m LiDAR (AdelaideMetro2018, AHD datum)
- **Scenarios:** +0.3 m (2050) and +1.0 m (2100), per SA Coast Protection Board policy
- **Masking:** DEM thresholded via raster calculator (NoData-guarded)
- **Connectivity:** GRASS `r.clump` retains only cells hydraulically connected to the sea, removing isolated depressions a naïve bathtub model would falsely flag
- **Vectorisation:** connected extent polygonised (DN = 1)
- **Building exposure:** OSM footprints ∩ inundation extent
- **Aggregation:** hexagonal zonal statistics for mean elevation and exposed-building density
- **Planning exposure:** Planning & Design Code zones intersecting the 2100 extent
- **CRS:** GDA94 MGA Zone 54 (EPSG:28354)

## Key findings

- Connected inundation expands from **0.61 ha** (2050, +0.3 m, no buildings exposed) to **36.8 ha** (2100, +1.0 m), exposing **58 buildings**.
- Exposure concentrates at **Birkenhead and Eastern Parade** on naturally low reclaimed land, following the historic street grid; raised wharf infrastructure remains largely above threshold.
- Hydraulic connectivity is decisive: filtering disconnected depressions removes false positives a standard bathtub model would report, materially reducing overstated exposure.
- Affected Planning & Design Code zones are led by **Waterfront Neighbourhood** and **General Neighbourhood**.

## Limitations

Static (bathtub) model — does not simulate wave action, storm surge, tidal timing or stormwater infrastructure. Single threshold per scenario; no probabilistic range. LiDAR vertical accuracy (~0.1–0.3 m RMSE) propagates to the boundary; a NOAA-style buffer (1.96 × RMSE ≈ 0.29 m) frames the extent as indicative, not parcel-precise. OSM footprint coverage may be incomplete. Connectivity run at 5 m then resampled to 1 m. Subsidence and future coastal defences not modelled.

## Data sources

- Elvis / Geoscience Australia — 1 m LiDAR DEM
- SA Planning & Design Code (PlanSA) — zoning
- OpenStreetMap — building footprints
- SA Coast Protection Board — sea-level-rise benchmarks

## Tools

QGIS · GRASS GIS (`r.clump`) · qgis2web (Leaflet) · GitHub Pages

## References

- Poulter, B. & Halpin, P.N. (2008). Raster modelling of coastal flooding from sea-level rise. *Int. J. Geographical Information Science*, 22(2), 167–182.
- Williams, L. & Lück-Vogel, M. (2020). Comparative assessment of the bathtub method and hydrologically connected method for coastal inundation mapping. *Geocarto International*.
- Gesch, D.B. (2009/2018). Analysis of LiDAR elevation data for improved delineation of lands vulnerable to sea-level rise. *J. Coastal Research*.
- NOAA Coastal Services Center (2010). *Mapping Coastal Inundation Primer.*
- IPCC AR6 WG1 (2021). Ch. 9: Ocean, Cryosphere and Sea Level Change.

---

*Prepared by Alberto Gallo — GIS & Spatial Analysis · 2026*
