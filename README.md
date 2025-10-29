# Predicting Operational Efficiency of Manufacturing Teams

This project analyzes and predicts the operational efficiency of manufacturing teams, focusing on two departments: **Stitching Unit** and **Finishing & Quality**. Using real-world manufacturing data, we perform comprehensive data cleaning, exploratory data analysis (EDA), feature engineering, model building, and evaluation to determine key drivers and best predictive models for team efficiency.

---

## Table of Contents

- [Contents](#contents)
- [Data Overview](#data-overview)
- [Workflow Summary](#workflow-summary)
  - [1. Data Preprocessing](#1-data-preprocessing)
  - [2. Exploratory Data Analysis (EDA)](#2-exploratory-data-analysis-eda)
  - [3. Model Building & Evaluation](#3-model-building--evaluation)
- [Key Insights](#key-insights)
- [How to Use](#how-to-use)
- [Requirements](#requirements)
- [Customization](#customization)

---

## Contents

- `MFG_StitchingUnit.ipynb` — Analysis and modeling for the Stitching Unit department.
- `MFG_Finishing&Quality.ipynb` — Analysis and modeling for the Finishing & Quality department.
- *(EDA notebook mentioned but not shared due to size constraints; the workflow and insights are described below.)*

---

## Data Overview

- **Source:** `manufacturing_data.csv`
- **Features:**
  - Operational, time, and team attributes (e.g., planned efficiency, overtime, bonuses, work in progress, team, day of week, etc.)
  - Target: `efficiencyScore` — the measured operational efficiency of each team on each record.

---

## Workflow Summary

### 1. Data Preprocessing
- **Cleaning:** Whitespace removal, handling NaNs, type conversions.
- **Filtering:** Split data by department (`productionDept`) to analyze Stitching Unit and Finishing & Quality separately.
- **Feature Engineering:**
  - Extracted `month` from dates.
  - Dropped constant or irrelevant columns (e.g., `fiscalQuarter`, `productionDept`, `recordDate`, and all-NaN columns).
  - Encoded categorical data:
    - **Label Encoding** for `team` (many unique values).
    - **One-Hot Encoding** for `dayOfWeek` and `styleChangeCount`.
  - Added derived features:
    - `efficiencyPerWorker` and `bonusPerWorker`.

- **Scaling:** MinMax scaling applied to numeric features (e.g., overtime, worker count, performance bonus, efficiency score, month).
- **Outlier Handling:** MinMax scaling helps mitigate the effect of large outliers.

### 2. Exploratory Data Analysis (EDA)
- **Distribution checks, correlations, and summary statistics** performed for each department.
- **Key findings:**
  - Some features (e.g., `idleWorkers`, `idleMinutes`) often have zero or limited variance.
  - Team and bonus-related features are strong differentiators.
  - `styleChangeCount` may be constant in some subsets.

### 3. Model Building & Evaluation

#### **For Each Department:**
- **Train/Test Split:** 80/20 random split.
- **Models Evaluated:**
  - Linear Regression
  - Random Forest Regressor
  - Gradient Boosting Regressor
- **Metrics:**
  - R² (Coefficient of Determination)
  - MSE (Mean Squared Error)
  - MAE (Mean Absolute Error)

#### **Results:**
- **Stitching Unit:**
  - All models (R² ≈ 0.75–0.76) — strong fit to data.
  - Random Forest is best (highest R², lowest MAE).

- **Finishing & Quality:**
  - Lower scores overall (R² up to ~0.31).
  - Gradient Boosting is best for this group.

#### **Feature Importance:**
- **Stitching:** Performance Bonus, Planned Efficiency, Work In Progress, Overtime, and Team are the most important features.
- **Finishing & Quality:** Worker Count, Overtime Minutes, Standard Minute Value, and Team are most important.

#### **Hyperparameter Tuning:**
- GridSearchCV used for Gradient Boosting in Finishing & Quality.
- Best params found and reported; modest performance improvement achieved.

---

## Key Insights

- **Stitching Unit efficiency is more predictable** with chosen features and models than Finishing & Quality.
- **Financial incentives (performance bonus)** and **workforce parameters** are the strongest drivers of team efficiency.
- **Team identity (encoded)** remains a significant predictor due to inherent differences between team lines.
- **Temporal and categorical effects** (e.g., month, day of week) are weaker predictors.
- **Gradient boosting and random forest** are superior to linear regression for these data, especially when relationships are nonlinear.

---

## How to Use

1. Place `manufacturing_data.csv` in the working directory.
2. Open and run the Jupyter notebooks in order:
   - `MFG_StitchingUnit.ipynb`
   - `MFG_Finishing&Quality.ipynb`
3. Review results, feature importances, and model performance in the notebook outputs.

---

## Requirements

- Python 3.7+
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- Jupyter Notebook

---

## Customization

- Adjust train/test splits, feature sets, or models as needed.
- Extend feature engineering or add new ML algorithms as desired.

---
