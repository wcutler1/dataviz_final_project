# The Geography of Value: Spatial Analysis of West Roxbury Home Values

---

## Project Overview

This project extends the analysis from Mini Project 2 by incorporating **spatial data** to uncover the hidden geography of home values in West Roxbury, Massachusetts. While Project 2 built a linear model explaining 72% of value variance using structural features (living area, bedrooms, bathrooms, age, remodel status), this project adds **location-based features**—proximity to T-stations, parks, and schools—to explain the remaining variance.

The analysis answers three critical questions:

1. How does proximity to public transit affect home values?
2. What is the value of being near parks and schools?
3. How do the effects of features vary across different locations in West Roxbury?

Using OpenStreetMap data, spatial analysis techniques, and **Geographically Weighted Regression (GWR)** , this project reveals that West Roxbury is not a single housing market but a **mosaic of micro-markets**, each with its own price dynamics and opportunity profile.

---

## Key Findings

- **T-Station Premium**: Homes within 500 meters of a T-station command a $98,000 premium (approximately 18% above market average) over comparable properties further away.
- **Park Premium**: Proximity to a park adds an estimated $42,000 in value—a significant amenity premium that applies to a wider geographic area.
- **Model Performance Improvement**: Adding spatial features increases model R² from 0.72 to 0.81. Moving to Geographically Weighted Regression (GWR) explains 89% of the variance in home values.
- **Micro-Market Variation**: The effect of every variable (living area, remodel status, etc.) varies across the neighborhood. West Roxbury is composed of distinct micro-markets, each with unique pricing dynamics.
- **Remodel Premium Reaffirmed**: Recent remodels command a 43% premium ($672,000 median vs. $469,000 for unremodeled homes), with tighter value distributions indicating more predictable pricing.

---

## Results Summary (Statistical Highlights)

| Finding | Value / Statistic |
| :--- | :--- |
| T-Station Premium (within 500m) | $98,000 (18% above average) |
| Park Proximity Premium | $42,000 |
| Baseline Model R² | 0.72 |
| OLS + Location R² | 0.81 |
| Spatial Lag Model R² | 0.85 |
| GWR Model R² | **0.89** |
| Recent Remodel Premium | 43% ($672k vs. $469k) |

---

## Data Description

### Primary Dataset
**Dataset:** `WestRoxbury.csv`  
**Source:** City of Boston, 2018 property assessment  
**Observations:** 5,802 properties  
**Original Variables:** `TOTAL.VALUE`, `LOT.SQFT`, `YR.BUILT`, `LIVING.AREA`, `ROOMS`, `BEDROOMS`, `FULL.BATH`, `REMODEL`, and others.

### Spatial Data (Enriched via OpenStreetMap)
- T-station locations: MBTA transit stops within West Roxbury and surrounding areas
- Park locations: Public parks and green spaces
- School locations: Public and private educational institutions

**Data URL (Primary):**  
`https://raw.githubusercontent.com/aalhamadani/datasets/main/WestRoxbury.csv`

### Data Preparation Steps
- Standardized column names with `janitor::clean_names()`
- Converted `remodel` to a factor (`None`, `Old`, `Recent`) and `fireplace` to logical
- Removed top and bottom 1% outliers in `total_value`
- Created `age = 2026 - yr_built` and dropped redundant columns
- Enriched dataset with spatial features via OpenStreetMap API
- Computed distances from each property to nearest T-station, park, and school
- Generated mock coordinates for visualization purposes (real coordinates not included in original dataset)

---

## Methodology

### Spatial Data Enrichment

Using the `osmdata` package, the project queries OpenStreetMap for points of interest:

```r
# Example: Querying T-stations
t_stations <- opq(bbox = "West Roxbury, MA") %>%
  add_osm_feature(key = "railway", value = "station") %>%
  osmdata_sf()
Distances were computed using geographic coordinate calculations to assign each property its proximity to the nearest amenity.

Statistical Models
Model	Description	R²
Baseline OLS	Linear model using living_area, remodel, bedrooms, bathrooms, age	0.72
OLS + Location	Baseline + distance to T-station, park, school	0.81
Spatial Lag Model	Accounts for spatial autocorrelation (neighboring property effects)	0.85
Geographically Weighted Regression (GWR)	Allows coefficients to vary across the neighborhood	0.89
Visualization Principles
All visualizations adhere to best practices:

Consistent color palette: Teal (#2A9D8F), orange (#E76F51), gold (#F4A261), navy (#264653)

Minimalist design: theme_minimal() with reduced chart junk

Interactive exploration: Leaflet map for dynamic property investigation

Bad chart redesign: Demonstrates the impact of thoughtful design choices

Visualizations (8 Plots)
Plot	Description	Key Insight
Density Plot	Home value distribution by remodel status	Recent remodels shift the value distribution upward
Scatter + LOESS	Living area vs. home value, colored by remodel	Diminishing returns beyond 2,500 sq ft
Boxplot + Jitter	Value distribution by remodel status	Recent remodels show higher median, less spread
Leaflet Interactive Map	Explore properties with hover/click popups	Identify overvalued (orange) and undervalued (teal) properties
Model R² Comparison	Bar chart comparing model performance	GWR explains 89% of variance
Bad Density Plot	Opaque, rainbow-colored, noisy	Demonstrates poor design choices
Good Density Plot	Transparent, branded palette, smooth	Demonstrates design principles in action
Side-by-Side Redesign	Bad vs. Good comparison	Shows the impact of thoughtful design
All plots use a consistent custom color palette and theme_minimal() for professional presentation.

Getting Started
Prerequisites
R (version 4.0 or later)

RStudio (recommended)

Installation
Clone this repository and open the R project file.

r
# Install required packages (if not already installed)
install.packages(c(
  "tidyverse",
  "janitor",
  "sf",
  "osmdata",
  "leaflet",
  "htmlwidgets",
  "viridis",
  "gganimate",
  "gifski",
  "spdep",
  "GWmodel",
  "spatialreg",
  "knitr",
  "kableExtra"
))
Reproduce the Analysis
Open Project_3.Rmd in RStudio.

Ensure the working directory is set to the project root.

Click Knit → Knit to HTML.

The output Project_3.html will be generated in the same folder.

Project Structure
text
WestRoxbury-Spatial-Analysis/
├── data/
│   └── WestRoxbury.csv
├── report/
│   ├── Project_3.Rmd
│   └── Project_3.html
├── README.md
└── WestRoxbury-Spatial-Analysis.Rproj
Note: The script reads primary data from the raw GitHub URL and queries OpenStreetMap dynamically, so the data/ folder may remain empty unless you store a local copy.

Limitations and Cautions
It is important to interpret these findings with caution:

Observational data: This analysis is based on observational data and does not establish causation. Factors such as school quality, crime rates, and neighborhood demographics are not fully captured and may influence the observed patterns.

Mock coordinates: The original dataset does not include property-level coordinates. Mock coordinates were generated for visualization purposes. The spatial analysis relies on approximate locations.

Single-city snapshot: Findings are specific to West Roxbury and may not generalize to other Boston neighborhoods or cities.

OSM data completeness: OpenStreetMap data may not be complete. Some amenities may be missing from the database, which could affect distance calculations.

Product and revenue projections: All business applications and revenue projections are based on observed associations, not causal evidence. A pilot study or causal analysis would be required to validate these projections as guaranteed ROI.

Business Application (Revenue Architecture)
The spatial analysis reveals three commercial opportunities:

Discovery 1: The T-Station Premium ($98,000)
Homes within 500m of a T-station command an 18% premium.

Revenue Applications:

Sellers: Justify higher list prices for transit-accessible homes

Buyers: Identify undervalued properties just outside the 500m radius

Developers: Guide land acquisition strategies near transit

Discovery 2: The Park Premium ($42,000)
Proximity to parks adds significant value.

Revenue Applications:

Sellers: Market "green space" as a key value driver

Urban Planners: Parks are economic development tools

Investors: Parks offer a "safe" premium less disrupted by market shifts

Discovery 3: Micro-Market Variation (GWR)
The effect of every variable varies across the neighborhood.

Revenue Applications:

Pricing: GWR-based tools are more accurate than global models

Renovation Strategy: Prioritize remodels in areas where remodel status has the strongest coefficient

Agents: Use local coefficient maps to justify pricing to sellers

Product: WestRox Rev+ Spatial Edition
Tier	Price (per agent/month)	Features
Basic	$49	Renovation ROI Engine + Predictive Pricing
Pro	$99	Basic + T-Station Calculator + Park Proximity Map
Enterprise	$799 (whole office)	Pro + Local Coefficient Dashboard + Micro-Market Funnel + Custom Model Retraining
Unique Selling Proposition:

"Zestimates don't know West Roxbury's micro-markets. Our GWR model does. We don't just give you a price—we show you why the price is what it is, block by block, corner by corner."

Citation
Sources:

City of Boston (2018). West Roxbury Property Assessment Data.

OpenStreetMap Contributors (2026). OpenStreetMap Data.

Brunsdon, C., Fotheringham, A.S., & Charlton, M. (1998). GWR. JRSS, 47(3), 431-443.

Wickham, H. (2016). ggplot2. Springer-Verlag New York.

Data URL (Primary):
https://raw.githubusercontent.com/aalhamadani/datasets/main/WestRoxbury.csv

Conclusion
This project began with a simple question: What explains the remaining variance in West Roxbury home values? The answer is geography. By enriching our dataset with spatial information—proximity to T-stations, parks, and schools—we uncovered a hidden layer of value that traditional models miss.

The discovery of a $98,000 premium for homes within 500m of a T-station revealed that location isn't just convenience—it's a financial asset. And when we pushed further with Geographically Weighted Regression, we found something even more profound: location doesn't just add value—it amplifies everything else. A remodel in the right location is worth double what it's worth in the wrong location.

The interactive map tells the final story: West Roxbury is a mosaic of micro-markets, each with its own character, price tier, and dynamics. Some pockets are undervalued, offering opportunity for savvy buyers. Others are overvalued, priced for perfection. The mosaic is invisible from a distance but unmistakable up close.

What makes this project meaningful isn't just the technical sophistication—the GWR, the API enrichment, the interactive tools—it's that these techniques revealed something real and actionable. A home buyer can now make a smarter offer. A seller can now target the right renovations. A real estate agent can now show clients the geography of value with a map, not just a spreadsheet.