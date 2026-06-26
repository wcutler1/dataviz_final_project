# West Roxbury Housing Analysis

# Project Overview

This project delivers a comprehensive, data‑driven analysis of the West Roxbury, Massachusetts housing market using the 2018 City of Boston property assessment dataset. Leveraging advanced statistical testing, predictive modeling, and interactive data visualization, the analysis answers three critical questions for homeowners, buyers, and real estate professionals:

1. How does living area relate to home value?
2. Does remodel status significantly affect property values?
3. What combination of features best predicts home value?

Beyond descriptive statistics, the project applies rigorous inferential methods (ANOVA, Tukey HSD, Levene's test, Kruskal‑Wallis) to validate findings, builds a linear regression model that explains 72% of the variance in home values, and transforms the insights into a commercial product pitch—demonstrating the real‑world ROI of data science.

---

# Key Findings

- Recent remodels command a 43% premium ($203,000) over homes with no remodels. This effect is statistically significant (p < 0.001) across multiple tests.
- Living area has diminishing returns: Home values increase with square footage up to ~2,500 sq ft, after which the marginal gain flattens significantly.
- Age is a consistent drag on value: Each additional year reduces home value by approximately 0.3% (log‑scale).
- Market bifurcation: The market splits into two distinct tiers—a dense cluster of standard homes ($450k–$750k) and a premium tier of larger, renovated properties approaching $1M.
- The linear model (Adjusted R² = 0.72) confirms that living area, remodel status, and age are the strongest drivers of property value.

---

# Data Description

Dataset: `WestRoxbury.csv`  
Source: City of Boston, 2018 property assessment  
Observations: 5,802 properties  
Original Variables (14): `TOTAL.VALUE`, `LOT.SQFT`, `YR.BUILT`, `GROSS.AREA`, `LIVING.AREA`, `ROOMS`, `BEDROOMS`, `FULL.BATH`, `HALF.BATH`, `REMODEL`, and others.

*Data Preparation Steps (Tidying):*
- Standardized column names with `janitor::clean_names()`
- Converted `remodel` to a factor (`None`, `Old`, `Recent`) and `fireplace` to logical
- Removed top and bottom 1% outliers in `total_value` to prevent skew
- Created `age = 2018 - yr_built` and dropped redundant columns (`tax`, `gross_area`, `yr_built`)
- Log‑transformed `total_value` and `lot_sqft` for model assumptions
- Removed rows with missing `remodel` values

---

# Methodology

# Statistical Testing (Inferential Rigor)

To move beyond description, the project applies a suite of statistical tests:

| Test | Purpose | Result |
| :--- | :--- | :--- |
| One‑Way ANOVA | Test if remodel status affects value | F(2, 5800+) = 187.4, p < 0.001 |
| Tukey HSD (Post‑hoc) | Identify which remodel groups differ | All pairwise comparisons p < 0.001 |
| Levene's Test | Test equality of variances across groups | F = 12.562, p < 0.001 |
| Kruskal‑Wallis | Non‑parametric robustness check | χ² = 187.4, p < 0.001 |
| Pairwise Wilcoxon (Bonferroni) | Confirm all groups distinct | All p < 0.001 |
| Correlation Matrix | Explore linear associations | Living area (r = 0.62), Age (r = -0.34) |

# Predictive Modeling

A linear regression model was built predicting `log_value` from:
- `living_area` (sq ft)
- `bedrooms`
- `full_bath`
- `age`
- `remodel` (factor)

**Adjusted R² = 0.72** — the model explains 72% of the variance in home values.

---

# Visualizations (7 Plots)

| Plot | Description |
| :--- | :--- |
| Correlation Matrix | Heatmap of feature relationships (Figure 1). |
| Lollipop Chart | Median value by remodel status; shows the 43% premium visually. |
| Violin + Boxplot | Full value distributions; reveals narrower spread for recent remodels. |
| Scatter + LOESS | Living area vs. value; identifies the 2,500 sq ft inflection point. |
| Hexbin Density | Heatmap of property concentration; shows the standard vs. premium tiers. |
| Interactive Plotly | Hoverable scatter plot; allows exploration of individual properties. |
| Spatial Map | Suffolk County tracts with West Roxbury highlighted; includes scale bar and north arrow. |

All plots use a consistent custom color palette and `theme_minimal()` for professional presentation.

---

# Business Application (Extra Credit)

*Product Name:* *WestRox Rev+* – The Hyper‑Local Value Intelligence Platform

This analysis was extended into a commercial product pitch for real estate agents, demonstrating the tangible ROI of the statistical insights.

*Core Modules:*
1. Renovation ROI Engine – Simulates value uplift for specific upgrades (e.g., full remodel vs. adding a bath).
2. Diminishing Returns Alert – Flags properties > 2,500 sq ft and recommends modernizing over expanding.
3. Market Tier Funnel – Classifies properties into Standard vs. Premium tiers with comparable sales.
4. Predictive Pricing Calculator – Uses the linear model to generate a scientifically derived list price.

**Subscription Pricing:**

| Tier | Price | Features |
| :--- | :--- | :--- |
| Basic | $49/mo | ROI Engine + Predictive Pricing |
| Pro | $99/mo | Basic + Diminishing Returns + Market Tier + PDF reports |
| Enterprise | $799/mo | Pro + weekly updates + custom retraining + co‑branded portals |

*Why it works:* A $99/month subscription pays for itself on the first listing by capturing the 43% premium or avoiding overpricing on large homes.

---

# Project Structure

WestRoxbury-Housing-Analysis/
├── data/
│ └── WestRoxbury.csv
├── report/
│ ├── Wesley_Cutler_MiniProject2.Rmd
│ └── Wesley_Cutler_MiniProject2.html
├── README.md
└── WestRoxbury-Housing-Analysis.Rproj


---

# Required Packages

To reproduce the analysis, install and load the following R packages:

```r
install.packages(c(
  "tidyverse",
  "janitor",
  "plotly",
  "broom",
  "htmlwidgets",
  "viridis",
  "knitr",
  "sf",
  "tigris",
  "car",
  "e1071",
  "corrplot",
  "ggspatial",
  "lmtest"
))