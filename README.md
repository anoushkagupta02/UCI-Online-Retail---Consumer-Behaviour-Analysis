# UCI-Online-Retail---Consumer-Behaviour-Analysis

**Dataset:** UCI Online Retail II — Real UK e-commerce transactions (2009–2011)  
**Stack:** Python · pandas · scikit-learn · SQLite · matplotlib · seaborn

---

## Overview

End-to-end customer analytics pipeline built on ~500K real e-commerce transactions. The project covers the full analytical lifecycle, from raw data cleaning through to actionable retention strategy, combining SQL-based exploration, RFM scoring with OLS-derived weights, unsupervised clustering, cohort retention analysis, and CLV estimation.

---

## Analytical Flow

| Step | Description |
|------|-------------|
| 1. Data Cleaning | Remove cancellations, null Customer IDs, negative quantities/prices; parse dates; compute line-item order value |
| 2. Feature Engineering | Build invoice-level transaction table with basket value, item count, and unique product count |
| 3. SQL Exploration | KPIs (revenue, orders, avg basket), revenue by country, top products, monthly trend via SQLite |
| 4. RFM Scoring | Recency, Frequency, Monetary computation with OLS-derived weights rather than arbitrary 1–5 binning |
| 5. Rule-Based Segmentation | Eight segments: Champions, Loyal, New Customers, At Risk, Cannot Lose Them, Lost, Promising, Hibernating |
| 6. K-Means Clustering | Elbow + silhouette scoring to determine optimal k; log-transformed + standardised features |
| 7. Cohort Retention | Monthly cohort heatmap (first 12 cohorts × 8 periods) |
| 8. CLV Estimation | 3-year CLV projection by segment using annualised purchase frequency and avg order value |
| 9. Business Recommendations | Segment-specific retention and re-engagement strategies |

---

## Key Techniques

- **OLS-derived RFM weights**: linear regression on rank-normalised R/F/M features to replace subjective equal-weight assumptions  
- **K-Means with log-transform**: log1p applied to monetary and frequency before StandardScaler to address distribution skew  
- **Cohort retention matrix**: customer counts pivoted by acquisition cohort and months-since-first-purchase, normalised to retention rates  
- **SQLite in-memory queries**: pandas DataFrames loaded into SQLite for KPI and segmentation queries without a database dependency  

---

## Outputs

- RFM segment distribution (customer count + avg spend per segment)
- Monthly revenue & active customer trend chart
- K-Means cluster scatter plots (Recency vs Monetary, Frequency vs Monetary)
- Cohort retention heatmap
- 3-year CLV bar chart by segment

---

## Setup
```bash
git clone https://github.com/anoushkagupta02/customer-segmentation-retention.git
cd customer-segmentation-retention
pip install -r requirements.txt
jupyter notebook UCI_Online_Retail_Customer_Segmentation_Retention.ipynb
```

**Dependencies:** `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `ucimlrepo`

The dataset is fetched directly from the UCI ML Repository at runtime — no manual download needed.

---

## Business Recommendations Summary

| Segment | Strategy |
|---------|----------|
| **Champions** | Reward, early access, review requests |
| **Loyal** | Upsell, loyalty programme enrolment |
| **At Risk** | Winback email + personalised discount |
| **Cannot Lose Them** | VIP / direct outreach |
| **Lost** | Low-cost re-engagement series |
| **New Customers** | Onboarding flow + second-purchase nudge |
| **Promising** | Targeted product recommendations |

**North star metric:** % of At Risk customers migrating to Loyal or Champions month-over-month.

---

## Portfolio Context

This project is part of a broader data science and marketing analytics portfolio targeting paid media, attribution, customer segmentation, and budget optimisation — built in Python and SQL.
