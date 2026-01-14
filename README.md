# UIDAI Geospatial Equity & Accessibility Mapping

## Hackathon Project - Geospatial Analysis for Aadhaar Service Delivery

---

## 📋 Project Overview

This project analyzes Aadhaar enrollment and biometric update data to identify geographic inequities in service delivery and recommend infrastructure improvements through geospatial analysis.

**Problem Statement:** Identify geographic inequities in Aadhaar service delivery using spatial analysis to recommend mobile enrollment unit routes, new center locations, and targeted outreach programs.

---

## 📁 Project Structure

```
UIDAI/
├── README.md                          # This file
├── .gitignore                         # Git ignore rules
│
├── data/                              # All data files
│   ├── raw/                           # Original raw data (DO NOT EDIT)
│   │   ├── biometric/                 # Biometric data splits
│   │   ├── demographic/               # Demographic data splits
│   │   └── enrolment/                 # Enrolment data splits
│   │
│   └── processed/                     # Cleaned and combined datasets
│       ├── biometric_clean.csv
│       ├── demographic_clean.csv
│       ├── enrolment_clean.csv
│       ├── api_data_aadhar_biometric_combined.csv
│       ├── api_data_aadhar_demographic_combined.csv
│       └── api_data_aadhar_enrolment_combined.csv
│
├── notebooks/                         # Jupyter notebooks (in sequence)
│   ├── 01_data_preprocessing.ipynb    # Data cleaning & preparation
│   ├── 02_eda_analysis.ipynb          # Exploratory data analysis
│   ├── 03_combined_analysis.ipynb     # Initial combined analysis
│
├── scripts/                           # Python scripts for utilities
│
├── outputs/                           # All generated outputs
│   ├── visualizations/                # Maps, charts, plots (HTML/PNG)
│   │
│   ├── reports/                       # Analysis reports & findings
│   │
│   └── models/                        # Saved models and data
│
└── docs/                              # Documentation
    ├── PROBLEM_STATEMENT.md           # Hackathon problem & evaluation metrics
    ├── METHODOLOGY.md                 # Detailed approach & algorithms
    ├── DATA_DICTIONARY.md             # Column definitions & data quality notes
    └── TECHNICAL_SETUP.md             # Environment setup instructions
```

---

## 🎯 Key Objectives

1. **Identify Underserved Regions**

   - Map pincodes with low/zero enrollment activity
   - Calculate service density metrics (enrollments/km²)
   - Identify geographic gaps (>50km from active centers)

2. **Quantify Inequity**

   - Calculate Gini coefficient for enrollment distribution
   - Urban vs. rural disparity analysis
   - State-level equity scorecards

3. **Optimize Service Delivery**

   - Recommend mobile unit routes using TSP logic
   - Identify optimal new center locations using centroid analysis
   - Estimate coverage improvement potential

4. **Create Actionable Insights**
   - Interactive geospatial dashboards
   - Prioritized intervention recommendations
   - Cost-benefit analysis of proposed solutions

--

## 📞 Support & Questions

For technical issues or questions about the analysis, refer to:

- `docs/METHODOLOGY.md` - Detailed algorithm explanations
- `docs/TECHNICAL_SETUP.md` - Environment setup help
- Individual notebook comments for step-by-step guidance

---

## 📜 License
Hackathon project - All data sourced from UIDAI public APIs