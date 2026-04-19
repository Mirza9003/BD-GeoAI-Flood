# BD-GeoAI-Flood

A national-scale GeoAI framework for flood susceptibility mapping and urban flood risk assessment in Bangladesh using machine learning, explainable AI, and spatial spatial-statistical analysis.

## Overview

This repository accompanies the study **“Geospatial Artificial Intelligence-based Flood Susceptibility Mapping and Urban Flood Risk Assessment: A Machine Learning Framework to Reduce Flood Risk.”** The project develops a reproducible national-scale workflow to map flood susceptibility across Bangladesh and to derive a pixel-level urban flood risk proxy by integrating modeled hazard with building exposure and population concentration. :contentReference[oaicite:0]{index=0}

The framework was designed to move beyond susceptibility-only mapping by identifying where elevated flood hazard coincides with dense built environments and concentrated population. The analysis covers all 64 districts of Bangladesh at 30 m spatial resolution. :contentReference[oaicite:1]{index=1}

## Study Objectives

The study addresses four major gaps in the Bangladesh flood assessment literature: limited national-scale machine learning applications, underuse of optimization and explainability methods, weak integration of hazard with urban exposure, and insufficient assessment of district-scale spatial clustering. To address these issues, the framework:

1. compares four machine learning models for flood susceptibility mapping,
2. applies explainable AI to interpret model behavior,
3. derives a pixel-level urban flood risk proxy by integrating hazard, building exposure, and population concentration, and
4. evaluates district-level spatial clustering using Global Moran’s I, LISA, and Getis-Ord Gi*. :contentReference[oaicite:2]{index=2}

## Study Area

The study covers the full national territory of **Bangladesh**, representing one of the world’s largest and most hydrologically complex deltaic environments. The analysis includes all **8 divisions** and **64 districts** over approximately **147,570 km²**. Major hydro-geomorphic settings include the Brahmaputra-Jamuna river system, northeastern haor wetlands, and the tidally influenced southern coastal belt. :contentReference[oaicite:3]{index=3}

## Methodological Framework

The workflow consists of five main stages:

- data acquisition, harmonization, and preprocessing,
- flood conditioning factor selection and multicollinearity screening,
- comparative machine learning-based flood susceptibility modelling,
- district-level spatial clustering analysis, and
- derivation of a pixel-based Urban Flood Risk Proxy (UFRP). :contentReference[oaicite:4]{index=4}

All datasets were harmonized to a common 30 m national grid before modelling and raster integration. :contentReference[oaicite:5]{index=5}

## Data Sources

The analysis integrates publicly available multisource geospatial datasets, including:

- **FABDEM** for terrain and hydrologic derivatives,
- **CHIRPS v2.0** for rainfall,
- **HydroSHEDS** for river proximity and drainage density,
- **Landsat-8 OLI** for NDVI, MNDWI, and NDBI,
- **ESA WorldCover 2021** for land use/land cover,
- **OpenStreetMap / HDX** for road distance,
- **WRI Aqueduct v2** for flood inventory generation,
- **TEMPO 2023 Q4** for building density, building height, and building volume proxy, and
- **WorldPop 2020** for gridded population concentration. :contentReference[oaicite:6]{index=6}

## Flood Inventory and Predictors

A binary flood inventory was derived from the **WRI Aqueduct historical river-flood inundation depth map** using a **0.1 m threshold**. From this inventory, **20,000 stratified sample points** were extracted, comprising **10,000 flood points** and **10,000 non-flood points**. :contentReference[oaicite:7]{index=7}

Eighteen candidate flood conditioning factors were initially considered. After variance inflation factor screening, **16 predictors** were retained for model development. :contentReference[oaicite:8]{index=8}

## Machine Learning Models

Four machine learning models were trained and evaluated:

- **XGBoost with Bayesian Optimization (XGB-BO)**
- **LightGBM**
- **Stacking Ensemble**
- **Artificial Neural Network (ANN)**

Model development used a **stratified 70:30 train-test split** and **10-fold cross-validation**. XGBoost hyperparameters were optimized using **Optuna** with a Tree-structured Parzen Estimator. :contentReference[oaicite:9]{index=9}

## Model Performance

Among the tested models, **XGB-BO** achieved the best overall performance and was selected as the reference model for downstream analyses. Reported performance metrics were:

- **AUROC:** 0.873
- **Accuracy:** 78.4%
- **Sensitivity:** 0.806
- **Specificity:** 0.763
- **F1-score:** 0.788 :contentReference[oaicite:10]{index=10}

SHAP analysis identified **elevation**, **rainfall**, and **distance to coast** as the most influential predictors of flood susceptibility. :contentReference[oaicite:11]{index=11}

## Urban Flood Risk Proxy

The second stage transforms flood susceptibility into a **pixel-based Urban Flood Risk Proxy (UFRP)** by integrating:

- normalized flood hazard,
- normalized built-environment exposure, and
- normalized population concentration.

The final proxy is computed using a **geometric mean formulation**, ensuring that high proxy values emerge only where all three components co-occur. :contentReference[oaicite:12]{index=12}

## Main Findings

### Flood Susceptibility

The national flood susceptibility map revealed strong spatial heterogeneity, with High and Very High susceptibility concentrated in the northeastern haor basin, north-central floodplain corridor, southwestern deltaic zone, and lower Meghna estuary. The combined **High + Very High** classes covered approximately **30% of the national territory**. **Sunamganj** was identified as the most flood-susceptible district, with **90%** of its area falling in High or Very High classes. :contentReference[oaicite:13]{index=13}

### Urban Flood Risk

At the national scale, the urban flood risk proxy was calculated for **130,880,943 valid pixels**. The distribution was strongly right-skewed, with **Very High urban flood risk accounting for 4.77%** of valid pixels and combined **High + Very High classes accounting for 11.62%**. **Narayanganj** ranked as the highest urban flood risk district with a score of **0.434**. :contentReference[oaicite:14]{index=14}

### Spatial Clustering

Flood susceptibility showed significant positive spatial autocorrelation with **Global Moran’s I = 0.4192**. Urban flood risk exhibited even stronger clustering, with **Global Moran’s I = 0.5011**. LISA analysis identified a compact central-eastern High-High urban flood risk corridor including **Dhaka, Narayanganj, Munshiganj, Narsingdi, Brahmanbaria, Cumilla, Chandpur, Feni, Noakhali, and Faridpur**. :contentReference[oaicite:15]{index=15} :contentReference[oaicite:16]{index=16}

## Repository Contents

```text
BD-GeoAI-Flood/
├── README.md
├── LICENSE
├── BD_Fig2_Methodology.png
├── BD_Fig.6_GeoAI_ML_ModelsAll.png
├── BD_Fig.8_LISA_Hotspot_MoransI.png
└── BD_Fig.9_NationalPixelBasedUrbanFloodRisk.png
