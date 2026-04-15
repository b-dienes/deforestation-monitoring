# Monitoring Amazonas Deforestation

## Overview
This project implements a geospatial pipeline to analyze deforestation in the Amazonas region using Sentinel-2 satellite imagery accessed via the UP42 API and STAC services.

The pipeline demonstrates:
- Authentication with UP42 API
- Catalog search and filtering of satellite imagery (based on AOI, time range, and cloud coverage)
- STAC metadata exploration
- Download and processing of spectral bands (Red and NIR)
- NDVI computation for vegetation monitoring
- Temporal analysis and change detection

---

## Methodology

### 1. Data Access
Sentinel-2 imagery is queried through the UP42 catalog using:
- Area of Interest (AOI)
- Time range (consistent seasonal comparison across years): July was selected as the basis of comparison, since it in the beginning of the dry season, combining good cloud conditions and limited wildland fire impact 
- Cloud coverage filtering

### 2. STAC API
The STAC API is used to access standardized geospatial metadata, including:
- Collections (datasets)
- Items (scenes)
- Assets (spectral bands)

### 3. NDVI Computation
Vegetation health is estimated using NDVI:

NDVI = (NIR - Red) / (NIR + Red)

### 4. Change Detection
NDVI differences between time steps are used to identify potential vegetation loss areas.

---

## Outputs

### Mean NDVI Trend Over Time
![Mean NDVI trend over time](mean_ndvi_over_time.png)

---

### NDVI Raster Maps (First vs. Last Observation)
![NDVI first vs last observation](ndvi_first_last_year.png)

---

### NDVI Change Detection (Difference Map)
![NDVI difference map](delta_ndvi_first_last_year.png)

---

### Areas of Lowest NDVI (Potential Deforestation)
![Lowest NDVI difference map](lowest_delta_ndvi_first_last_year.png)

---

## Limitations
- No atmospheric correction was used beyond cloud filtering
- Spatial consistency was assumed across scenes
- NDVI is not necessarily a direct deforestation classifier

---

## Environment Variables
The following environment variables are required:

- UP42_USERNAME
- UP42_PASSWORD
- UP42_WORKSPACE_ID

These are loaded via a `.env` file.

---

## Requirements
- jupyterlab
- ipykernel
- requests
- rasterio
- numpy
- matplotlib
- python-dotenv
