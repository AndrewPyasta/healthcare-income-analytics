# Healthcare Income, Physical Activity & Obesity Analytics

**Data analytics externship project | Summer 2026**  
**Focus:** Individual-level health survey analysis and Wisconsin/Milwaukee County geographic patterns  
**Tools:** Python · Pandas · NumPy · Matplotlib · Seaborn · SciPy · scikit-learn · GeoPandas · Google Colab

## Project overview

This portfolio project explores the association between household income, physical activity, body mass index (BMI), and obesity. Completed as part of a **TruBridge data analytics externship**, the work combines exploratory statistics, hypothesis testing, introductory regression/classification, and geographic visualization to communicate public-health patterns.

**Primary question:** How is household income associated with physical activity and obesity, and what geographic patterns appear across Wisconsin census tracts, especially Milwaukee County?

> **Two distinct analyses:** The individual-level CDC Diabetes Health Indicators dataset is **not** Milwaukee-specific. The geographic analysis separately joins **2024 ACS** income estimates and **2025 CDC PLACES** prevalence estimates to **Wisconsin census tracts**. Findings from the two levels must not be conflated.

## Interactive dashboard & final presentation

- **[Explore the interactive healthcare analytics dashboard](https://claude.ai/public/artifacts/cfe4827b-b074-481e-9cf8-f6d0760e88f1)** — browse the visual summary of income, physical activity, obesity, and geographic findings.
- **[View the TruBridge Healthcare Data Analytics presentation](https://gamma.app/docs/TruBridge-Healthcare-Data-Analytics-Project-7whwlf847gxqjhv?mode=doc)** — review the research question, methods, findings, and interpretation.

These are externally hosted project materials. Availability may depend on the sharing permissions of each platform.

## Key findings

### 1. Individual-level analysis

The original notebook starts with **253,680 records** and reports **229,474 rows after dropping identical records**. This reduction is documented as a methodological limitation, not proof of duplicate people.

| Relationship | Pearson r | Description |
|---|---:|---|
| Income category ↔ physical activity | **+0.166** | Modest positive association |
| Income category ↔ BMI | **−0.069** | Very weak negative association |
| Income category ↔ obesity indicator | **−0.056** | Very weak negative association |

*Values transcribed from the saved output of `03_statistical_analysis.ipynb`, not independently recalculated for this package. Income is encoded as ordinal categories rather than actual dollars.*

![Physical activity by income category](images/activity_by_income.png)

### 2. Wisconsin and Milwaukee tract-level analysis

The geographic workflow merges median household income with estimated health-outcome prevalence using census-tract identifiers.

| Geography | Relationship | Pearson r from saved output |
|---|---|---:|
| Wisconsin tracts | Income ↔ physical inactivity | **−0.713** |
| Milwaukee County tracts | Income ↔ physical inactivity | **−0.726** |
| Milwaukee County tracts | Income ↔ obesity prevalence | **−0.705** |

These are stronger *tract-level* negative correlations, meaning higher-income tracts tended to have lower modeled obesity/inactivity prevalence in these outputs. **They do not establish causation** and do not describe person-level relationships.

![Milwaukee County median income by census tract](images/milwaukee_income.png)
![Milwaukee County obesity by census tract](images/milwaukee_obesity.png)

## What I worked on

- Collected and examined public health and Census data; assessed missing values and identical records.
- Conducted exploratory visualizations, summary statistics, correlations and hypothesis tests.
- Built introductory linear/logistic regression models and reviewed their performance.
- Joined **CDC PLACES**, **ACS B19013** household income, and Census tract geometries using GEOIDs/tract FIPS.
- Created Wisconsin and Milwaukee choropleth maps, comparisons, and area summaries.
- Translated analyses into visual storytelling for a nontechnical audience.

## Repository guide

| Notebook | Purpose |
|---|---|
| [`01_cdc_data_preparation.ipynb`](notebooks/01_cdc_data_preparation.ipynb) | Download UCI source, inspect data, prepare records |
| [`02_exploratory_analysis.ipynb`](notebooks/02_exploratory_analysis.ipynb) | Distributions, obesity indicator, group comparisons |
| [`03_statistical_analysis.ipynb`](notebooks/03_statistical_analysis.ipynb) | Correlations, tests, exploratory regression and classification |
| [`04_data_storytelling.ipynb`](notebooks/04_data_storytelling.ipynb) | Communication-ready charts and findings |
| [`05_wisconsin_milwaukee_mapping.ipynb`](notebooks/05_wisconsin_milwaukee_mapping.ipynb) | Geographic joins, choropleths, Milwaukee comparisons |

`images/` contains preview charts exported from the original notebook outputs. `docs/` explains data acquisition and remaining checks.

## How to reproduce

1. Install Python packages: `pip install -r requirements.txt`.
2. Run **notebook 01**, which retrieves UCI dataset 891 and generates `data/processed/cdc_diabetes_prepared.csv`.
3. Run notebooks **02–04** in order, using the prepared data.
4. For the **independent mapping notebook 05**, download the 2025 CDC PLACES tract CSV, 2024 ACS B19013 ZIP, and 2024 Wisconsin tract TIGER/Line ZIP into `data/raw/`, following [Data setup](docs/DATA_SETUP.md).
5. Run notebook 05. The optional municipality/neighborhood labeling section requires two additional boundary ZIP files.

**Data files are intentionally not included** in this public portfolio package. Notebooks contain saved historical outputs and have **not been fully rerun** here because original source GIS files were not provided in this upload.

## Sources

- [UCI Machine Learning Repository — CDC Diabetes Health Indicators, dataset 891](https://archive.ics.uci.edu/dataset/891/cdc+diabetes+health+indicators)
- [CDC PLACES Data Portal](https://www.cdc.gov/places/tools/data-portal.html)
- [U.S. Census Bureau ACS data](https://data.census.gov/) — 2024 ACS five-year, table B19013
- [U.S. Census TIGER/Line shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html) — 2024 Wisconsin census tracts

## Limitations

Individual-level income categories are ordinal, and the original analysis removed all identical records, which may remove genuinely different respondents with matching answers. Tract-level analyses rely on ACS income estimates and **model-based** CDC PLACES prevalence. Ecological association must not be interpreted as an individual effect. Multiple datasets, geographies, and release years have different measurement definitions. Further validation of source files and rerunning results are recommended before any policy or operational use. See [Review notes](docs/REVIEW_NOTES.md).

## Project author

**Andrew Pyasta** · Information Systems and Business Analytics · Marquette University
