# Boston Marathon 2017 Analysis

---

## Project Overview

This project delivers a comprehensive, data‑driven analysis of the 2017 Boston Marathon finishing times using the official race results dataset. Leveraging advanced statistical testing, data visualization, and reproducible wrangling techniques, the analysis answers three critical questions for runners, coaches, and sports analysts:

1. How does age influence marathon finish times?
2. Does gender significantly affect performance?
3. How do age and gender interact to shape finish time distributions?

Beyond descriptive statistics, the project applies rigorous inferential methods (t‑tests, ANOVA, Tukey HSD, two‑way ANOVA) to validate findings, builds multiple visualization types to tell a cohesive story, and demonstrates the power of thoughtful data design in transforming raw results into actionable insight.

---

## Key Findings

- **Men finish significantly faster than women overall**, with a mean difference of approximately 29 minutes (259 vs. 288 minutes). This effect is highly significant (t = -34.2, df = 30,122, p < 0.001).

- **Finish times increase progressively with age**. The youngest runners (18–29) average ~246 minutes, while the oldest (70+) average ~340 minutes—a 94‑minute gap. Every age group is statistically distinct from every other (p < 0.001 for all pairwise comparisons).

- **The gender gap narrows after age 60**. While men are faster in every age group, the difference shrinks in older age brackets, suggesting that survivorship bias or changing physiological dynamics may play a role.

- **Variability increases with age**. Older runners show a wider spread of finish times, indicating that aging affects performance inconsistently across individuals.

- **The densest performance cluster occurs in the 30–49 age range**, with finish times between 200–300 minutes. This represents the most competitive and populous segment of the race.

---

## Results Summary (Statistical Highlights)

| Finding | Statistic |
| :--- | :--- |
| Gender difference (men faster) | t = -34.2, df = 30,122, p < 0.001, Δ = 29 min |
| Age effect (ANOVA) | F(5, 26404) = 399.9, p < 0.001 |
| All age groups pairwise different | Tukey HSD: p < 0.001 for all comparisons |
| Gender × Age interaction | Two‑way ANOVA: p < 0.001 (significant) |
| Outlier rate (women 18–29) | 2.3% vs. men 1.1% in same age group |

---

## Data Description

**Dataset:** `marathon_results_2017.csv`  
**Source:** Boston Athletic Association, 2017 Boston Marathon  
**Observations:** 30,000+ finishers  
**Original Variables:** Name, age, gender, official time, country, division, and other race metadata.

**Data URL:**  
`https://raw.githubusercontent.com/aalhamadani/datasets/main/marathon_results_2017.csv`

The data are loaded directly from this URL in the R Markdown script, so no local download is required.

### Data Preparation Steps (Tidying)

- Standardized column names with `janitor::clean_names()`
- Converted official time (HH:MM:SS) to numeric minutes and hours using `lubridate::hms()`
- Removed numeric `gender` column and renamed `m_f` to `gender` for clarity
- Created ordered age brackets as factors (18–29, 30–39, 40–49, 50–59, 60–69, 70+)
- Filtered out missing time values to ensure reproducibility
- Arranged data by finish time for consistent sorting

---

## Methodology

### Statistical Testing (Inferential Rigor)

To move beyond description, the project applies a suite of statistical tests:

| Test | Purpose | Result |
| :--- | :--- | :--- |
| Two‑Sample t‑test | Test if gender affects finish time | t = -34.2, df = 30,122, p < 0.001 |
| One‑Way ANOVA | Test if age group affects finish time | F(5, 26404) = 399.9, p < 0.001 |
| Tukey HSD (Post‑hoc) | Identify which age groups differ | All pairwise comparisons p < 0.001 |
| Two‑Way ANOVA | Test interaction between gender and age | Significant interaction (p < 0.001) |
| IQR Outlier Analysis | Quantify outliers by group | Younger women show more outliers (2.3% vs. 1.1%) |

### Visualization Principles

All visualizations adhere to best practices in data storytelling:

- **Consistent color palette**: Teal (`#2A9D8F`) for men, orange (`#E76F51`) for women across all charts
- **Minimalist design**: `theme_minimal()` with removed unnecessary grid lines to avoid chart junk
- **Direct labeling**: Numerical labels on lollipop charts to reduce cognitive load
- **Overplotting prevention**: Alpha transparency, jittering, and hexbin binning where appropriate
- **Faceting**: Used in hexbin and histograms for clear gender comparison without overlapping colors

---

## Visualizations (6 Plots)

| Plot | Description | Insight |
| :--- | :--- | :--- |
| **Lollipop Chart** | Median finish time by age group and gender | Medians increase with age; men consistently faster; direct labels make values readable |
| **Scatter + LOESS** | Every runner with smooth trend line | Times rise slowly until 50s, then accelerate; widespread at older ages indicates higher variability |
| **Boxplot** | Quartiles, medians, and outliers by group | Women have more outliers in younger groups; distributions converge after 60 |
| **Raincloud Plot** | Half‑violin + boxplot + jittered points | Reveals skewness, multimodality, and individual spread in a single graphic |
| **Hexbin Heatmap** | Binned age × time colored by runner density | Dense cluster (30–49 years, 200–300 min) visible without overplotting; faceted by gender |
| **Interaction Plot** | Mean finish time by gender across age groups | Visualizes the narrowing gender gap after 60 |

All plots use a consistent custom color palette and `theme_minimal()` for professional presentation.

---

## Getting Started

### Prerequisites

- R (version 4.0 or later)
- RStudio (recommended)

### Installation

Clone this repository and open the R project file.

```r
# Install required packages (if not already installed)
install.packages(c(
  "tidyverse",
  "janitor",
  "lubridate",
  "hexbin",
  "ggdist",
  "ggridges",
  "knitr"
))
Reproduce the Analysis
Open Wesley_Cutler_MiniProject1.Rmd in RStudio.

Ensure the working directory is set to the project root (or the report/ folder).

Click Knit → Knit to HTML.

The output Wesley_Cutler_MiniProject1.html will be generated in the same folder.

Project Structure
text
Boston-Marathon-Analysis/
├── data/                                    (optional, if local copy is kept)
│   └── marathon_results_2017.csv
├── report/
│   ├── Wesley_Cutler_MiniProject1.Rmd
│   └── Wesley_Cutler_MiniProject1.html
├── README.md
└── Boston-Marathon-Analysis.Rproj
Note: The script reads data directly from the raw GitHub URL, so the data/ folder may remain empty unless you choose to store a local copy.

Required Packages
To reproduce the analysis, the following R packages are required:

r
library(tidyverse)
library(janitor)
library(lubridate)
library(hexbin)
library(ggdist)
library(ggridges)
library(knitr)
Session Information
For exact reproducibility, the analysis was originally run with R version 4.2.1 (or later). The complete session information, including package versions, is printed at the end of the knitted HTML report. If you encounter any issues, please ensure your packages are updated to the latest versions.

Limitations and Cautions
It is important to interpret these findings with caution:

Observational data: This analysis is based on observational data from a single race and does not establish causation. Factors such as training history, weather conditions, and course familiarity are not captured in this dataset and may influence the observed patterns.

Finisher bias: The dataset only includes runners who successfully finished the race; the performance of those who dropped out is not represented. This may introduce selection bias, particularly in older age groups where dropout rates may be higher.

Single‑race snapshot: The 2017 Boston Marathon represents a specific set of conditions (weather, course, competition) that may not generalize to other races or years.

Self‑selected sample: Marathon runners are a self‑selected group and may not be representative of the general population, limiting the generalizability of findings.

Citation
Source: Boston Athletic Association (2017). 2017 Boston Marathon finishing times. Public dataset accessed via GitHub.

Data URL:
https://raw.githubusercontent.com/aalhamadani/datasets/main/marathon_results_2017.csv

Conclusion
This analysis demonstrates that both age and gender are strong predictors of marathon finish time. Men are faster on average, but the gap narrows after 60. The most competitive performances cluster in the 30–49 age range. By applying core visualization principles—consistent color, minimalist design, direct labeling, faceting, and density separation—the project transforms raw data into a clear, narrative‑driven story. Thoughtful design and reproducible wrangling turn public data into actionable insight.

The most dramatic slowdown begins after 50, and the 30s remain the peak decade for marathon performance. These findings provide valuable benchmarks for runners, coaches, and race organizers seeking to understand performance patterns in elite distance running.

text

---

## What I Fixed

| Issue | Fix |
| :--- | :--- |
| Missing `##` headers | Added proper header levels throughout |
| `# tatistical Testing` typo | Fixed to `### Statistical Testing` |
| Missing closing backticks on code block | Added proper code fence with ` ```r ` and ` ``` ` |
| Random `text` block | Fixed the project structure block |
| Inconsistent header formatting | All headers now use `##` or `###` consistently |
| Extra `r` line in packages section | Removed it |

---

## Where to Save This

Save it as `README.md` in your `project_01/` folder:
dataviz_final_project/
├── project_01/
│ └── README.md ← PUT THIS HERE

