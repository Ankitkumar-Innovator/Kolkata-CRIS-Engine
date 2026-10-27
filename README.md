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

1. **Land Surface Temperature (LST °C):** Thermal Infrared (TIR) Band 10 from Landsat-8 is converted from raw Digital Numbers  to Spectral Radiance, and inverted via Planck's Law to derive true ground temperature in Celsius.
2. **Modified Normalized Difference Water Index (MNDWI):** Sentinel-2 Green (B3) and SWIR (B11) bands isolate permanent and seasonal surface water channels to evaluate drainage/flood exposure.
3. **Matrix Alignment & Fusion:** Bilinear spatial resampling matches Sentinel-2  to Landsat-8  matrix dimensions, enabling min-max normalization and weighted linear combination into a unified **Climate Risk Index (CRI)** array.

---

## Repository Structure

```text
Kolkata-CRIS-Engine/
├── scripts/
│   ├── 01_gee_data_extraction.ipynb      # Google Earth Engine data pipeline
│   ├── 02_grid_resampling_alignment.ipynb# Rasterio spatial affine transformation
│   └── 03_cri_matrix_fusion.py           # First-principles LST, MNDWI & CRI fusion
├── README.md
└── requirements.txt
