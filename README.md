# BD-GeoAI-Flood

**Geospatial Artificial Intelligence-based Flood Susceptibility Mapping and Urban Flood Risk Assessment for Bangladesh**

A national-scale GeoAI framework for 30 m flood susceptibility mapping and pixel-level urban flood risk assessment in Bangladesh using machine learning, explainable AI, and spatial clustering analysis.

<p align="center">
  <img src="./BD_Fig2_Methodology.png" alt="Methodological framework" width="85%">
</p>

---

## Overview

This repository accompanies the study:

**Geospatial Artificial Intelligence-based Flood Susceptibility Mapping and Urban Flood Risk Assessment: A Machine Learning Framework to Reduce Flood Risk**

The project develops a reproducible national-scale framework to:

- map flood susceptibility across all 64 districts of Bangladesh,
- compare multiple machine learning models for predictive performance,
- interpret model behavior using explainable AI,
- integrate hazard, building exposure, and population concentration into a pixel-level urban flood risk proxy, and
- identify district-scale spatial clusters and hotspots of flood susceptibility and urban flood risk.

The analysis is conducted at **30 m spatial resolution** for the full territory of Bangladesh.

---

## Main Contributions

- National-scale **flood susceptibility mapping** for Bangladesh
- Comparative evaluation of **XGBoost-BO, LightGBM, Stacking Ensemble, and ANN**
- **SHAP-based explainable AI** for model interpretation
- Pixel-level **Urban Flood Risk Proxy (UFRP)** integrating hazard, built exposure, and population concentration
- District-level **Global Moran’s I, LISA, and Getis-Ord Gi\*** hotspot analysis
- Interactive visualization through a **Google Earth Engine web application**

---

## Study Area

The study covers the entire national territory of **Bangladesh**, including all **8 divisions** and **64 districts**. Bangladesh is a highly dynamic deltaic environment shaped by the Ganges, Brahmaputra, and Meghna river systems, northeastern haor wetlands, and a low-lying coastal belt exposed to tidal and storm-surge processes.

---

## Methodological Framework

The workflow consists of five main stages:

1. **Data acquisition, harmonization, and preprocessing**
2. **Flood conditioning factor screening and multicollinearity assessment**
3. **Comparative machine learning-based flood susceptibility modelling**
4. **Spatial statistical analysis of district-level susceptibility patterns**
5. **Urban flood risk proxy derivation and hotspot characterization**

---

## Data Sources

The framework integrates publicly available multisource geospatial datasets, including:

- **FABDEM** for terrain and hydrologic derivatives
- **CHIRPS v2.0** for rainfall
- **HydroSHEDS** for river proximity and drainage density
- **Landsat-8 OLI** for NDVI, MNDWI, and NDBI
- **ESA WorldCover 2021** for land use/land cover
- **OpenStreetMap / HDX** for road distance
- **WRI Aqueduct v2** for flood inventory generation
- **TEMPO 2023 Q4** for building density, building height, and building volume proxy
- **WorldPop 2020** for gridded population concentration

---

## Flood Inventory and Predictors

A binary flood inventory was generated from the WRI Aqueduct historical river-flood inundation depth dataset using a **0.1 m threshold**. A total of **20,000 stratified sample points** were extracted for supervised model development, including:

- **10,000 flood points**
- **10,000 non-flood points**

Eighteen candidate flood conditioning factors were initially compiled, and **16 predictors** were retained after multicollinearity screening.

---

## Machine Learning Models

The following models were evaluated:

- **XGBoost with Bayesian Optimization (XGB-BO)**
- **LightGBM**
- **Stacking Ensemble**
- **Artificial Neural Network (ANN)**

All models were trained using a **stratified 70:30 train-test split** and **10-fold cross-validation**.

### Best-performing model
**XGB-BO** was selected as the reference model for downstream susceptibility mapping and urban flood risk analysis.

**Performance metrics of XGB-BO:**
- **AUROC:** 0.873
- **Accuracy:** 78.4%
- **Sensitivity:** 0.806
- **Specificity:** 0.763
- **F1-score:** 0.788

SHAP analysis identified **elevation**, **rainfall**, and **distance to coast** as the most influential predictors.

---

## Key Results

### Flood Susceptibility
- High and Very High susceptibility zones are concentrated in the **northeastern haor basin**, **north-central floodplain corridor**, **southwestern deltaic plain**, and **lower Meghna estuary**.
- The combined **High + Very High** susceptibility classes cover approximately **30%** of Bangladesh.
- **Sunamganj** was identified as the most flood-susceptible district, with **90%** of its area falling within the High or Very High classes.

### Urban Flood Risk
- The Urban Flood Risk Proxy was derived for more than **130 million valid pixels**.
- **Very High** urban flood risk accounts for **4.77%** of valid pixels.
- Combined **High + Very High** urban flood risk accounts for **11.62%** of valid pixels.
- **Narayanganj** ranked as the highest urban flood risk district.

### Spatial Clustering
- Flood susceptibility exhibited significant positive spatial autocorrelation.
- Urban flood risk showed even stronger clustering than susceptibility.
- A compact **central-eastern urban flood risk hotspot corridor** was identified along the Dhaka-Meghna system.

---

## Repository Structure

```text
BD-GeoAI-Flood/
├── README.md
├── LICENSE
├── BD_Fig2_Methodology.png
├── BD_Fig.6_GeoAI_ML_ModelsAll.png
├── BD_Fig.8_LISA_Hotspot_MoransI.png
└── BD_Fig.9_NationalPixelBasedUrbanFloodRisk.png
