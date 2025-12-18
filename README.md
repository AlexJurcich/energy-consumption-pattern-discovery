# Energy Consumption Pattern Discovery

This project analyzes apartment-level electricity usage using unsupervised learning and
association rule mining to uncover patterns driven by weather and seasonality. The goal
is to determine whether meaningful behavioral clusters exist in daily energy consumption
and to identify environmental conditions that consistently co-occur with high or low usage.

---

## Project Overview

- **Dataset:** Smart* Apartment Electricity Dataset (UMASS)
- **Scope:** 114 apartments, daily observations from 2014–2016 (~85k records)
- **Problem Type:** Unsupervised learning / pattern discovery
- **Focus:** Clustering structure, dimensionality reduction, and rule mining

This project intentionally evaluates *multiple* unsupervised approaches to assess whether
natural groupings exist in the data, rather than forcing artificial separation.

---

## Dataset

The dataset combines:
- Daily aggregated electricity usage (mean, min, max, total, standard deviation)
- Daily weather conditions (temperature, humidity)
- Calendar features (season, weekday vs weekend)

After cleaning and IQR-based outlier removal, the final analysis dataset contains
approximately 70k daily apartment records.

Source:
- Smart*: An Open Data Set for Enabling Research in Sustainable Homes (UMASS)

---

## Methods

### Data Preprocessing
- Merged 300+ raw CSV files
- Removed missing values and extreme outliers using IQR filtering
- Engineered categorical features:
  - Season (winter, spring, summer, fall)
  - Weekday vs weekend
- Standardized numeric variables

### Dimensionality Reduction
- Principal Component Analysis (PCA)
- Retained 7 components explaining ~90% of total variance
- Used PCA space for visualization and clustering diagnostics

### Clustering Approaches
- **K-Means++**
  - Selected k = 4 using the elbow method
  - Captured broad seasonal usage patterns
- **DBSCAN**
  - Grid search over eps and min_samples
  - Performed poorly due to extreme data density
- **Gaussian Mixture Models (GMM)**
  - Selected k using AIC/BIC
  - Produced results nearly identical to K-Means

### Association Rule Mining
- Apriori
- FP-Growth
- Quantile-based binning for interpretability

---

## Key Findings

- **Temperature and seasonality dominate electricity usage**
- Daily usage patterns form a dense, overlapping structure
- Clustering methods struggle to produce clean separation due to lack of low-density regions
- DBSCAN is not well-suited for this dataset
- Association rules consistently reinforce weather-driven patterns:
  - Cold days → higher total power usage
  - Mild temperatures → lower overall usage

The strongest patterns are environmental rather than behavioral.

---

## Limitations

- Daily aggregation smooths intra-day behavioral differences
- No occupancy or appliance-level data
- All apartments are from a single geographic region (UMASS)
- Temperature masks weaker secondary effects

These limitations are intrinsic to the data and help explain why clustering separation is weak.

---

## Code

- `energy-consumption-pattern-discovery.ipynb`  
  End-to-end analysis notebook including:
  - Data cleaning and feature engineering
  - PCA and visualization
  - K-Means, DBSCAN, and GMM clustering
  - Association rule mining with Apriori and FP-Growth

The notebook is structured to run top-to-bottom and is intended as a reproducible analysis.

---

## Files

- `energy-consumption-pattern-discovery.ipynb` – Full analysis notebook
- `report/` – Final written report (PDF)
- `slides/` – Presentation slides
- `proposal/` – Original project proposal

---

## Next Steps

- Explore time-series segmentation or dynamic clustering
- Evaluate alternative dimensionality reduction techniques
- Train predictive models for daily energy demand

---

## Author

**Alex Jurcich**  
M.S. Data Science  
