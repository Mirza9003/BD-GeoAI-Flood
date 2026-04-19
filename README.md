# BD-GeoAI-Flood

Geospatial Artificial Intelligence-based flood susceptibility mapping and urban flood risk assessment for Bangladesh using machine learning, explainable AI, and spatial hotspot analysis. This repository accompanies the study **“Geospatial Artificial Intelligence-based Flood Susceptibility Mapping and Urban Flood Risk Assessment: A Machine Learning Framework to Reduce Flood Risk.”** The framework maps flood susceptibility at 30 m resolution across all 64 districts of Bangladesh and then integrates hazard, building exposure, and population concentration to derive a pixel-level urban flood risk proxy. :contentReference[oaicite:0]{index=0}

## Overview

Flood risk in Bangladesh cannot be understood from hazard alone. This project develops a national-scale GeoAI workflow that combines flood susceptibility modelling with urban exposure layers to identify where modeled hazard overlaps with dense buildings and concentrated population. The study evaluates four machine learning models:

- XGBoost with Bayesian Optimization (XGB-BO)
- LightGBM
- Stacking Ensemble
- Artificial Neural Network (ANN)

Among them, **XGB-BO** achieved the best overall performance and was selected for downstream mapping and urban risk assessment. :contentReference[oaicite:1]{index=1}

## Key Contributions

- Developed a **national-scale 30 m flood susceptibility map** for Bangladesh.
- Compared **four machine learning models** under a stratified 70:30 train-test split with 10-fold cross-validation.
- Applied **SHAP-based explainable AI** to interpret model behavior and identify dominant flood controls.
- Integrated susceptibility, building exposure, and population concentration into a **pixel-level Urban Flood Risk Proxy (UFRP)**.
- Quantified **district-level spatial clustering** using Global Moran’s I, LISA, and Getis-Ord Gi*.
- Deployed the selected output through an **interactive Google Earth Engine web application** for accessibility and planning support. 

## Study Area

The analysis covers the full territory of **Bangladesh** (approximately **147,570 km²**), including all **8 divisions** and **64 districts**. The country’s hydro-geomorphic complexity includes the Brahmaputra-Jamuna system in the north, haor wetlands in the northeast, and the tidally influenced coastal belt in the south, making it a strong testbed for national flood modelling. :contentReference[oaicite:3]{index=3}

## Methodological Framework

The workflow consists of five major stages:

1. **Data acquisition, harmonization, and preprocessing**
2. **Flood conditioning factor selection** and multicollinearity screening using VIF
3. **Comparative machine learning-based flood susceptibility modelling**
4. **District-scale spatial statistical analysis** using Global Moran’s I, LISA, and Getis-Ord Gi*
5. **Urban Flood Risk Proxy derivation** by integrating hazard, built-environment exposure, and population concentration

All datasets were harmonized to a **common 30 m national grid**. :contentReference[oaicite:4]{index=4}

## Input Data

The study integrates publicly available multisource geospatial datasets. Major inputs include:

- **FABDEM** for elevation, slope, aspect, curvature, TWI, SPI, and flow accumulation
- **CHIRPS v2.0** for rainfall
- **HydroSHEDS** for distance to river and drainage density
- **Landsat-8 OLI** for NDVI, MNDWI, and NDBI
- **ESA WorldCover 2021** for land use/land cover
- **OpenStreetMap / HDX** for road distance
- **WRI Aqueduct v2** for flood inventory generation
- **TEMPO 2023 Q4** for building density, height, and volume proxy
- **WorldPop 2020** for gridded population concentration :contentReference[oaicite:5]{index=5}

## Flood Inventory

A binary flood inventory was generated from the **WRI Aqueduct historical river-flood inundation depth map** using a **0.1 m threshold**. A total of **20,000 stratified sample points** were extracted for supervised learning, including **10,000 flood points** and **10,000 non-flood points**. :contentReference[oaicite:6]{index=6}

## Conditioning Factors

Eighteen candidate flood conditioning factors were initially considered. After VIF screening, **16 predictors** were retained:

- Elevation
- Slope
- Aspect
- Curvature
- TWI
- SPI
- Flow accumulation
- Monsoon mean rainfall
- Distance to river
- Drainage density
- NDVI
- MNDWI
- NDBI
- LULC
- Distance to road
- Distance to coast :contentReference[oaicite:7]{index=7}

## Model Development

All models were trained using a **stratified 70:30 train-test split** and **10-fold cross-validation**. XGBoost was optimized using **Optuna** with a **Tree-structured Parzen Estimator** over depth, learning rate, number of estimators, and subsample ratio. The stacking model used XGBoost and Random Forest as base learners with logistic regression as meta-classifier, while the ANN used a 128-64-32 dense architecture with dropout and Adam optimization. :contentReference[oaicite:8]{index=8}

## Best Model Performance

The selected **XGB-BO** model achieved:

- **AUROC:** 0.873
- **Accuracy:** 78.4%
- **F1-score:** 0.79
- **Sensitivity:** 0.806

SHAP analysis identified **elevation**, **rainfall**, and **distance to coast** as the most influential predictors. 

## Urban Flood Risk Proxy

The second stage transforms the flood susceptibility output into a **pixel-based Urban Flood Risk Proxy (UFRP)** by integrating:

- normalized hazard
- normalized built-environment exposure
- normalized population concentration

The final proxy is computed using the **geometric mean** of these three components so that high values emerge only where hazard, building exposure, and population co-occur. :contentReference[oaicite:10]{index=10}

## Main Findings

### Flood Susceptibility

- XGB-BO produced the reference national flood susceptibility surface.
- High and Very High susceptibility zones are concentrated in the **northeastern haor basin**, **north-central floodplain corridor**, **southwestern deltaic zone**, and **lower Meghna estuary**.
- The combined **High + Very High** susceptibility classes cover approximately **30%** of Bangladesh.
- **Sunamganj** ranked as the most flood-susceptible district, with **90%** of its area in High or Very High classes. :contentReference[oaicite:11]{index=11}

### Urban Flood Risk

- Nationally, **4.77%** of valid pixels fall in the **Very High** urban flood risk class.
- Combined **High + Very High** urban flood risk classes account for **11.62%** of valid pixels.
- **Narayanganj** ranked as the highest urban flood risk district with a score of **0.434**.
- Urban flood risk forms a strong **central-eastern corridor**, especially along the **Dhaka-Meghna system**. 

### Spatial Clustering

- Flood susceptibility showed significant clustering with **Global Moran’s I = 0.419**.
- Urban flood risk showed even stronger clustering with **Global Moran’s I = 0.501**.
- LISA analysis identified **10 High-High urban flood risk districts**, highlighting a compact regional hotspot in central-eastern Bangladesh. 

## Repository Contents

Current repository contents include:

- `README.md`
- `LICENSE`
- `BD_Fig2_Methodology.png`
- `BD_Fig.6_GeoAI_ML_ModelsAll.png`
- `BD_Fig.8_LISA_Hotspot_MoransI.png`
- `BD_Fig.9_NationalPixelBasedUrbanFloodRisk.png`

## Figures

### Figure 2. Methodological framework
`BD_Fig2_Methodology.png`  
Illustrates the full workflow from conditioning-factor preparation and preprocessing through machine learning modelling, explainable AI, hotspot analysis, and deployment. :contentReference[oaicite:14]{index=14}

### Figure 6. Comparative model outputs
`BD_Fig.6_GeoAI_ML_ModelsAll.png`  
Shows national flood susceptibility maps generated by the four tested machine learning models, enabling visual comparison of spatial patterns across XGB-BO, LightGBM, Ensemble, and ANN. The manuscript describes broadly similar national patterns, with sharper transitions in the boosting-based outputs. :contentReference[oaicite:15]{index=15}

### Figure 8. LISA hotspot and Moran’s I results
`BD_Fig.8_LISA_Hotspot_MoransI.png`  
Presents statistically significant district-level flood susceptibility clusters, including High-High and Low-Low areas, demonstrating non-random spatial organization of flood-prone regions. :contentReference[oaicite:16]{index=16}

### Figure 9. National pixel-based urban flood risk
`BD_Fig.9_NationalPixelBasedUrbanFloodRisk.png`  
Shows the national urban flood risk surface and district-level ranking of the top urban flood risk districts, highlighting the prominence of Narayanganj and the Dhaka-Meghna corridor. :contentReference[oaicite:17]{index=17}

## Interactive Web App

An interactive Google Earth Engine application is available here:

**https://tinyurl.com/GeoAIFloodBD** :contentReference[oaicite:18]{index=18}

## Suggested Citation

**Mukarram, M. M. T., Linderman, M., & Shokrana, M. S. B.**  
*Geospatial Artificial Intelligence-based Flood Susceptibility Mapping and Urban Flood Risk Assessment: A Machine Learning Framework to Reduce Flood Risk.* :contentReference[oaicite:19]{index=19}

## License

This repository is released under the **MIT License**.

## Contact

**Mirza Md Tasnim Mukarram**  
Department of Computer Science, University of Iowa  
School of Earth, Environment and Sustainability, University of Iowa :contentReference[oaicite:20]{index=20}
