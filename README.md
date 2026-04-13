# Customer Segmentation with Clustering

**K-Means clustering applied to 951,669 e-commerce transactions across 68,300 customers to identify actionable customer segments.**

---

## Overview

Customer segmentation is a critical strategic tool for retail businesses — enabling targeted marketing, improved retention, price optimisation, and smarter resource allocation. This project applies unsupervised machine learning to a large real-world e-commerce dataset to identify five distinct customer segments and provide the business with data-driven marketing recommendations.

---

## Dataset

- **951,669** transactional records (April 2012 – October 2016)
- **68,300** unique customers across **47 countries** on five continents
- 20 features covering order details, customer demographics, and order metadata
- Source: 'https://github.com/FourthRevGitHub/CAM_DS_Public-Data-Sets/raw/main/Course%201/Week%206/CUSTOMERS_CLEAN.zip'

---

## Methodology

### 1. Data Cleaning
- Removed 21 duplicate rows → 951,648 clean records
- Handled missing values in City, Postal_Code, and State_Province fields

### 2. Feature Engineering
Five features were derived from the raw transactional data:

| Feature | Description |
|---|---|
| Frequency | Count of orders per customer — engagement and loyalty marker |
| Recency | Days since most recent delivery (inverted: higher = more recent) |
| CLV | Customer Lifetime Value — sum of all revenue per customer |
| Avg_Unit_Cost | Mean unit cost per order — purchasing behaviour indicator |
| Age | Customer age derived from birthdate |

### 3. EDA & Preprocessing
- Identified right skew and outliers in Frequency, CLV, and Avg_Unit_Cost
- Capped extreme outliers using the **3×IQR method**
- Standardised all features using **StandardScaler** for equal contribution to distance-based clustering

### 4. Optimal Cluster Selection
Three complementary methods used to determine optimal k:
- **Elbow Method** — WCSS improvement slows significantly from k=5 onwards
- **Silhouette Score** — peaked at k=2; k=5 was second highest with better business interpretability
- **Hierarchical Clustering** — Ward linkage dendrogram on 2,000-customer sample

**k=5 selected** based on elbow method, silhouette analysis, and business interpretability.

### 5. Dimensionality Reduction
- **PCA** — captured 65.6% of variance in two components; broad cluster overview
- **t-SNE** — applied to 5,000-customer sample (perplexity=40); sharper cluster boundaries confirming five-segment structure

---

## Results

| Cluster | Segment | Avg Frequency | Avg Recency | Avg CLV | Avg Unit Cost | Avg Age |
|---|---|---|---|---|---|---|
| 0 | Premium Buyers | 8.1 | 1,387 | £1,783 | £128.70 | 52 |
| 1 | Older Regulars | 10.7 | 1,598 | £1,276 | £65.60 | 69 |
| 2 | Lapsed Customers | 4.8 | 690 | £550 | £59.48 | 57 |
| 3 | High Value Active | 30.0 | 1,696 | £4,387 | £81.91 | 48 |
| 4 | Young Regulars | 12.2 | 1,594 | £1,481 | £67.53 | 37 |

*Recency (inverted): higher value = more recent purchase.*

### Key Findings
- **Cluster 3 (High Value Active)** is the most commercially significant: highest frequency (30x), recency, and CLV (£4,387). Priority for retention investment.
- **Cluster 0 (Premium Buyers)** is distinguished by markedly higher avg unit cost (£128.70 vs £59–82 for all others) — a niche group purchasing high-value products at moderate frequency. Requires a different strategy to other segments.
- **Cluster 2 (Lapsed Customers)** has the lowest values across all metrics — clear re-engagement target.
- **Clusters 1 & 4** represent 54% of the customer base, differentiated primarily by age (69 vs 37) despite similar CLV profiles — suggesting different channel strategies.

---

## Marketing Recommendations

- **High Value Active (Cluster 3):** Dedicated loyalty programme, personalised communications, exclusive product access. Highest financial risk if lost.
- **Lapsed Customers (Cluster 2):** Time-limited win-back discounts and personalised re-engagement emails. Control investment per customer given low CLV.
- **Premium Buyers (Cluster 0):** Curated high-value product recommendations and upselling — avoid volume promotions.
- **Older Regulars (Cluster 1):** Traditional email and direct mail; bundle deals to drive frequency.
- **Young Regulars (Cluster 4):** Digital-first, social media and app-based offers; bundle deals to grow CLV toward High Value Active tier.

---

## Tech Stack

```
Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · Jupyter
```

**Key techniques:** K-Means clustering · Elbow method · Silhouette scoring · Hierarchical clustering (Ward linkage) · PCA · t-SNE · StandardScaler · IQR outlier capping · Feature engineering

---

## Repository Structure

```
├── notebook.ipynb          # Full analysis notebook
├── report.pdf              # Written report with visualisations and recommendations
└── README.md
```

---


