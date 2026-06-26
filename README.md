# Data Visualization Final Project
**Author:** Wesley Cutler
**Date:** June 2026

---

## Executive Summary

This repository contains three data visualization projects completed for the Data Visualization course. Each project explores a different dataset and applies progressively advanced analytical techniques.

**Project 1** analyzes the 2017 Boston Marathon to understand how age and gender influence finish times. Men finish significantly faster (Δ = 29 minutes, p < 0.001), and finish times increase progressively with age—a 94-minute gap from the youngest to oldest runners.

**Project 2** explores the West Roxbury housing market to identify what factors drive home values. Recent remodels command a 43% premium ($672k vs. $469k), and living area shows diminishing returns beyond 2,500 sq ft. The linear model explains 72% of the variance in home values.

**Project 3** extends the housing analysis with spatial data, revealing that homes within 500m of a T-station command a $98,000 premium and proximity to a park adds $42,000 in value. Geographically Weighted Regression explains 89% of the variance—up from 72% with the baseline model.

---

## Project 01: Boston Marathon Analysis
**Theme:** Age and gender influence finish times in the 2017 Boston Marathon

**Key Findings:**
- Men finish significantly faster than women (Δ = 29 minutes, p < 0.001)
- Finish times increase progressively with age (94-minute gap from 18–29 to 70+)
- The gender gap narrows after age 60
- Variability increases with age

**My Favorite Chart:** The **Raincloud Plot** combines a half-violin (density shape), boxplot (summary statistics), and jittered points (every runner) into one graphic. It reveals skewness, multimodality, and individual spread better than any single chart type.

**Techniques Used:** t-test, ANOVA, Tukey HSD, two-way ANOVA, LOESS smoothing, hexbin heatmap, raincloud plot

**[View Project 1](./project_01/)**

---

## Project 02: West Roxbury Housing Analysis
**Theme:** What factors drive home values in West Roxbury, MA?

**Key Findings:**
- Recent remodels command a **43% premium** ($672k vs. $469k)
- Living area shows **diminishing returns** beyond 2,500 sq ft
- Older homes lose approximately **0.3% value per year**
- The linear model explains **72% of variance** (Adjusted R² = 0.72)

**My Favorite Chart:** The **Scatter + LOESS** plot shows every property as a point with a smooth trend line, revealing the critical inflection point at 2,500 sq ft where returns flatten. The color coding by remodel status shows that renovation adds value at every size level.

**Techniques Used:** ANOVA, Tukey HSD, Levene's test, Kruskal-Wallis, linear regression, VIF, Breusch-Pagan test, interactive Plotly visualization, spatial mapping

**[View Project 2](./project_02/)**

---

## Project 03: The Geography of Value
**Theme:** Unlocking West Roxbury's hidden premium with spatial analysis

**Key Findings:**
- Homes within 500m of a T-station command a **$98,000 premium** (18% above average)
- Proximity to a park adds **$42,000 in value**
- Adding spatial features increases model R² from **0.72 to 0.81**
- **GWR explains 89%** of value variance

**My Favorite Chart:** The **Interactive Leaflet Map** allows users to explore individual properties, zoom into street corridors, hover over parcels to view exact valuations, and identify localized arbitrage opportunities. It transforms the "mosaic of micro-markets" concept from abstract to tangible.

**Techniques Used:** OpenStreetMap API enrichment, distance computations, Geographically Weighted Regression (GWR), spatial lag models, Leaflet interactive mapping, bad chart redesign

**[View Project 3](./project_03/)**

---

## Data Sources

| Project | Dataset | Source |
| :--- | :--- | :--- |
| Project 01 | Marathon Results 2017 | Boston Athletic Association |
| Project 02 | West Roxbury Property Data | City of Boston (2018) |
| Project 03 | West Roxbury Property Data + OpenStreetMap | City of Boston (2018) + OSM Contributors (2026) |

---

## How to Reproduce

1. Clone this repository
2. Open each project's `.Rmd` file in RStudio
3. Install required packages (see each project's README)
4. Click **Knit** → **Knit to HTML**

---

## Required Packages

```r
install.packages(c(
  "tidyverse", "janitor", "lubridate", "hexbin", "ggdist", "ggridges",
  "plotly", "broom", "htmlwidgets", "viridis", "knitr", "kableExtra",
  "sf", "tigris", "osmdata", "leaflet", "spdep", "GWmodel", "spatialreg",
  "car", "e1071", "corrplot", "ggspatial", "lmtest", "gganimate", "gifski"
))
