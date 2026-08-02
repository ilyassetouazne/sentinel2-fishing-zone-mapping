# Sentinel-2 Fishing Zone Mapping

Unsupervised detection of high-productivity marine zones off the Agadir coast (Morocco) using Sentinel-2 multispectral imagery.

## Overview

This project explores whether spectral signatures alone — without ground-truth fishing data — can reveal spatial structure in the ocean that correlates with biological productivity (a proxy for fish presence).

**Pipeline:**
1. **Data acquisition** — Sentinel-2 L2A imagery (Google Earth Engine), cloud-filtered, median composite (2023), 50k sampled points over the Agadir coastal zone.
2. **Feature engineering** — 13 spectral bands, water/vegetation indices (NDWI, MNDWI, NDVI, NDBI, BSI), band ratios, log transforms, GLCM texture.
3. **Exploratory analysis** — band-wise histograms and correlation heatmaps to select informative features and drop redundant/irrelevant ones (e.g. NDVI, BSI for the marine subset).
4. **Sea / Beach / Land classification** — rule-based split using NDWI thresholds.
5. **Dimensionality reduction** — PCA (linear) and UMAP (non-linear) to reveal structure not captured by PCA alone.
6. **Clustering** — DBSCAN on the UMAP embedding to detect natural sub-zones within the sea class.
7. **Productivity ranking** — clusters ranked using a chlorophyll-a proxy (B3/B2 ratio) to flag zones of higher biological activity.

## Key result

DBSCAN on the UMAP embedding surfaces ~58 distinct marine sub-clusters against a dominant homogeneous "open ocean" background. The highest-ranked clusters by chlorophyll proxy show spectral signatures consistent with nutrient-rich coastal water — plausible candidate zones for fishing activity.

## Notes and limitations

- The B3/B2 chlorophyll proxy is a simplified indicator, not a validated oceanographic index (e.g. OC3/OC4).
- No ground-truth validation (AIS vessel data, reported catches) is used — results are a spectral hypothesis, not a confirmed fishing map.
- Single-year (2023) data; no seasonal analysis, despite fishing activity being highly seasonal.
- Bathymetry and current data, often stronger drivers of fish presence than surface color alone, are not included.

## Stack

`Google Earth Engine` · `Python` · `pandas` · `scikit-learn` · `UMAP` · `seaborn` / `matplotlib`

## Author

Ilyasse Touazne — Data Science Engineering, INSEA
