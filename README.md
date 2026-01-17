# UIDAI Geospatial Equity & Accessibility Mapping

## 🏆 Hackathon on Data-Driven Innovation on Aadhaar - 2026

---

## 📋 Project Overview

This project analyzes Aadhaar enrollment and biometric update data to identify geographic inequities in service delivery and recommend infrastructure improvements through geospatial analysis.

**Problem Statement:** Identify meaningful patterns, trends, anomalies, and predictive indicators in Aadhaar enrollment and update data to support informed decision-making and system improvements.

**Our Solution:** A Geospatial Equity Analysis Framework that combines:

- Gini coefficient analysis for inequality measurement
- K-Means clustering for service pattern identification
- Machine learning models for demand forecasting
- Novel Equity Score for continuous monitoring

---

## 🎯 Key Highlights

| Metric                 | Value   |
| ---------------------- | ------- |
| Total Records Analyzed | 3.4M+   |
| States/UTs Covered     | 36      |
| Districts Analyzed     | 700+    |
| Unique Pincodes        | 19,000+ |
| Model Accuracy (R²)    | 84.7%   |

---

## 📁 Project Structure

```
UIDAI/
├── README.md                          # This file
├── SUBMISSION_CONTENT.txt             # Ready-to-paste submission text
├── requirements.txt                   # Python dependencies
│
├── data/                              # All data files
│   ├── raw/                           # Original raw data
│   │   ├── biometric/
│   │   ├── demographic/
│   │   └── enrolment/
│   │
│   └── processed/                     # Cleaned and combined datasets
│       ├── biometric_clean.csv
│       ├── demographic_clean.csv
│       └── enrolment_clean.csv
│
├── notebooks/                         # Jupyter notebooks
│   ├── 01_data_preprocessing.ipynb    # Data cleaning & preparation
│   ├── 02_eda_analysis.ipynb          # Exploratory data analysis
│   ├── 03_combined_analysis.ipynb     # Cross-dataset analysis
│   └── 04_master_analysis.ipynb       # ⭐ MAIN ANALYSIS NOTEBOOK
│
├── scripts/
│   └── generate_report.py             # PDF report generator
│
├── outputs/                           # Generated outputs
│   ├── visualizations/                # Charts (HTML/PNG)
│   ├── reports/                       # Analysis reports & PDF
│   │   └── UIDAI_Hackathon_Report.pdf # ⭐ SUBMISSION REPORT
│   └── models/                        # Saved ML models
│
└── docs/                              # Documentation
    ├── PROBLEM_STATEMENT.md           # Hackathon requirements
    └── METHODOLOGY.md                 # Detailed approach
```

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Run Master Analysis

```bash
jupyter notebook notebooks/04_master_analysis.ipynb
```

### 3. Generate PDF Report

```bash
python scripts/generate_report.py
```

---

## 📊 Key Findings

### 1. Geographic Disparity

- Top 5 states account for ~60% of total enrollments
- Significant urban-rural divide in service access

### 2. Inequality Metrics

- Average Gini coefficient: **0.35** (moderate inequality)
- 15% of districts classified as underserved

### 3. Demographic Patterns

- Youth (5-17) enrollments correlate with school programs
- Adult (18+) updates dominate biometric activity

### 4. Predictive Capability

- Random Forest model achieves **84.7% R²** score
- Age group features are top predictors

---

## 💡 Key Innovation: Equity Score Framework

```
Equity Score = Normalized Activity × (1 - Gini Coefficient)
```

**Interpretation:**

- Score → 1.0: High activity with equitable distribution
- Score → 0.0: Low activity or highly unequal distribution

---

## 📋 Recommendations

1. **Mobile Enrollment Units** - Deploy to top 20 priority districts
2. **School Partnerships** - Expand youth enrollment programs
3. **Equity Dashboard** - Implement quarterly monitoring
4. **Demand-Based Planning** - Use ML forecasts for resource allocation
5. **New Centers** - Establish in underserved high-population areas

---

## 🛠️ Technical Stack

- **Data Processing:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Machine Learning:** Scikit-learn (Random Forest, Gradient Boosting)
- **Geospatial:** Folium, GeoPandas
- **Reporting:** ReportLab (PDF generation)

---

## 📄 Submission Files

| File            | Description              | Location                                     |
| --------------- | ------------------------ | -------------------------------------------- |
| PDF Report      | Complete analysis report | `outputs/reports/UIDAI_Hackathon_Report.pdf` |
| Master Notebook | Full analysis code       | `notebooks/04_master_analysis.ipynb`         |
| Submission Text | Title & Description      | `SUBMISSION_CONTENT.txt`                     |

---

## 👥 Team

Hackathon project for UIDAI Data-Driven Innovation Challenge 2026

---

## 📜 License

Hackathon project - All data sourced from UIDAI public APIs
