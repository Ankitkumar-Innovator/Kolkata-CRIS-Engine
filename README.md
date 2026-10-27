# CRIS: Climate Resilience Intelligence System for Kolkata

[![IEEE Paper](https://img.shields.io/badge/IEEE-Paper_Draft-blue.svg)](#)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-green.svg)](https://www.python.org/)
[![Google Earth Engine](https://img.shields.io/badge/GEE-Python_API-00704A.svg)](https://earthengine.google.com/)

An integrated geospatial data fusion pipeline designed to quantify joint **Urban Heat Island (UHI)** and **Urban Flood Vulnerabilities** across Kolkata, India, using multi-sensor satellite telemetry (Landsat-8 & Sentinel-2). 

This project forms the underlying framework for our IEEE conference research paper:  
**"CRIS: A Multi-Modal Climate Resilience Intelligence System for Joint Urban Heat Island and Flood Risk Analysis"**  
*Department of Computer Science and Engineering, Techno India University, Kolkata.*

---

## Scientific Overview

Traditional municipal climate monitoring treats thermal stress and hydrological hazards as isolated events. The **CRIS** framework unifies them into a single 30-meter resolution spatial grid using first-principles remote sensing math and matrix operations:

1. **Land Surface Temperature (LST °C):** Thermal Infrared (TIR) Band 10 from Landsat-8 is converted from raw Digital Numbers (DN) to Spectral Radiance, and inverted via Planck's Law to derive true ground temperature in Celsius.
2. **Modified Normalized Difference Water Index (MNDWI):** Sentinel-2 Green (B3) and SWIR (B11) bands isolate permanent and seasonal surface water channels to evaluate drainage/flood exposure.
3. **Matrix Alignment & Fusion:** Bilinear spatial resampling matches Sentinel-2 (10m) to Landsat-8 (30m) matrix dimensions, enabling min-max normalization and weighted linear combination into a unified **Climate Risk Index (CRI)** array.

---

## Repository Structure

```text
Kolkata-CRIS-Engine/
├── scripts/
│   ├── 01_gee_data_extraction.ipynb       # Google Earth Engine data pipeline
│   ├── 02_grid_resampling_alignment.ipynb # Rasterio spatial affine transformation
│   └── 03_cri_matrix_fusion.py            # First-principles LST, MNDWI & CRI fusion
├── README.md
└── requirements.txt
```

---

## Installation & Setup

### 1. Prerequisites
Make sure you have Python 3.9+ installed along with the following geospatial libraries:

```bash
pip install earthengine-api rasterio numpy matplotlib
```

### 2. Google Earth Engine Authentication
To run the extraction pipeline, you need an active GEE account tied to a cloud project:

```python
import ee
ee.Authenticate()
ee.Initialize(project='your-cloud-project-id')
```

---

## Execution Pipeline

### Step 1: Satellite Telemetry Extraction
Run `scripts/01_gee_data_extraction.ipynb` in Google Colab to filter cloud-masked summer composites for Landsat-8 (Thermal) and dry winter composites for Sentinel-2 (MNDWI) over Kolkata (`[88.20, 22.45, 88.45, 22.65]`). Export outputs directly to Google Drive.

### Step 2: Grid Alignment & Spatial Warping
Run `scripts/02_grid_resampling_alignment.ipynb` locally or in Colab to resample Sentinel-2 imagery to match Landsat-8’s $30\text{m}$ grid extent using Bilinear Interpolation.

### Step 3: Matrix Fusion & CRI Map Generation
Execute the main calculation script to compute physical temperature matrices, MNDWI ratios, and export `Kolkata_Climate_Risk_Index_30m.tif`.

---

## Sample Output & Verification

The output spatial matrices identify high-density commercial/industrial cores exhibiting surface heat islands exceeding $45^\circ\text{C}$, intersecting low-lying drainage vectors along the East Kolkata Wetlands.

---

## Research Team

* **Ankit Kumar Shaw** (Lead Architecture & Data Pipeline)
* **Ramisha Fathma** (Hydrology & Literature Review)
* **Suhana Chakrabarti** (UHI Dynamics & Data Analysis)

*Techno India University, Kolkata, India.*
