# Customer Churn & Retention Intelligence Platform

A business intelligence platform that converts e-commerce customer data into actionable retention decisions — from KPIs and churn trends through machine learning prediction and data-driven recommendations, all surfaced in an interactive five-tab dashboard.

---

## Dataset Source

**E-Commerce Customer Churn Analysis and Prediction**  
Kaggle: https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction

- File: `E Commerce Dataset.xlsx` (sheet: `E Comm`)
- 5,630 customer records × 20 features
- Target variable: `Churn` (binary 0/1, 16.84% positive rate)

---

## Project Overview

This platform processes raw customer data through a complete analytics pipeline:

1. **Data quality audit** — missing values, outliers, label inconsistencies
2. **Preprocessing** — median imputation, label fixing, feature engineering (TenureBand, CouponAdoptionRate, EngagementScore)
3. **Exploratory analysis** — churn distributions across all 19 feature dimensions
4. **Business KPIs** — 20 computed metrics from the dataset (churn rate, retention rate, cashback gap, complaint-churn rate, etc.)
5. **Churn trend analysis** — churn rates across tenure bands, city tiers, login devices, payment modes, order categories, satisfaction scores, marital status
6. **Churn driver analysis** — point-biserial correlations, mean comparisons, chi-square tests, correlation heatmap
7. **Customer segmentation** — KMeans (K=4) on behavioural features; segments labelled from actual churn-rate profiles
8. **Churn prediction** — Random Forest with RandomizedSearchCV hyperparameter tuning, stratified split, class-weight balancing
9. **Model evaluation** — accuracy, precision, recall, F1, ROC-AUC, confusion matrix, ROC curve, PR curve, feature importances
10. **High-risk identification** — churn probability assigned to all 5,630 customers; risk-tiered (High ≥70%, Medium 40–69%, Low <40%)
11. **Risk & opportunity analysis** — 4 risk signals and 3 opportunity signals quantified from actual data
12. **Retention recommendations** — 6 data-supported recommendations, all values referenced from computed results

---

## Technologies

| Library | Version | Purpose |
|---------|---------|---------|
| `pandas` | 2.2.2 | Data loading and manipulation |
| `numpy` | 1.26.4 | Numerical operations |
| `openpyxl` | 3.1.2 | Excel file reading engine |
| `scikit-learn` | 1.5.1 | KMeans, RandomForestClassifier, StandardScaler, metrics, RandomizedSearchCV |
| `scipy` | 1.13.1 | Point-biserial correlation, chi-square tests |
| `plotly` | 5.22.0 | All interactive charts |
| `dash` | 2.17.1 | Multi-tab dashboard framework |
| `dash-bootstrap-components` | 1.6.0 | Layout and card styling |

---

## Project Files

```
customer-churn-retention/
├── app.py                      # Single Python file — all logic + dashboard
├── requirements.txt            # Pinned dependencies
├── README.md                   # This file
├── report.md                   # Full project report
└── E Commerce Dataset.xlsx     # Source data (not modified)
```

---

## Setup

**Requirements:** Python 3.10 or later

1. **Clone / navigate to the project directory**

   ```bash
   cd customer-churn-retention
   ```

2. **Create and activate a virtual environment** (recommended)

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate        # macOS / Linux
   # .venv\Scripts\activate         # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

---

## Run

```bash
python app.py
```

The terminal will print progress:
```
Loading and processing data…
Training Random Forest model (this may take ~30–60 seconds)…
Model metrics — Accuracy: 96.27%  |  F1: 88.46%  |  ROC-AUC: 99.1%
Data pipeline complete. Starting dashboard…
```

Open your browser and navigate to:

```
http://127.0.0.1:8050
```

---

## Dashboard Tabs

| Tab | Contents |
|-----|---------|
| 📊 Executive Overview | 12 KPI cards, churn pie, city-tier bar, cashback comparison, tenure comparison, high-risk snapshot |
| 📉 Churn Analysis | Churn rates by tenure band, satisfaction score, complaint status, marital status, gender, login device, device count, order category, payment mode |
| 🔍 Churn Drivers | Correlation bar, feature importance, mean comparison, full heatmap, chi-square table |
| ⚠️ Customer Risk & Prediction | Model metrics, confusion matrix, ROC curve, PR curve, risk pie, risk scatter, sortable top-200 customer table |
| 🎯 Risks, Opportunities & Actions | Risk signal bars, opportunity bars, KMeans segment profiles, elbow chart, 6 retention recommendation cards |

---

## Model Performance (on held-out test set)

| Metric | Value |
|--------|-------|
| Accuracy | 96.27% |
| Precision | 92.53% |
| Recall | 84.74% |
| F1 Score | 88.46% |
| ROC-AUC | 99.1% |

---

## Notes

- The original `E Commerce Dataset.xlsx` file is never modified.
- All analysis, KPIs, findings, and recommendations are derived strictly from the dataset — no values are invented.
- The model uses `class_weight='balanced'` to handle the 1:4.9 class imbalance.
- The dashboard runs entirely in-memory; no database or external service is required.
