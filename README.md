# AI-Assisted Digital Twin for EDM Process Optimisation

## Overview

This repository implements an ML-based digital twin prototype for Electrical Discharge Machining (EDM). It predicts:

- Material Removal Rate (MRR)
- Surface Roughness (Ra)
- Tool Wear Rate (TWR)

The pipeline includes feature engineering using Spark Energy and Duty Cycle, Random Forest and XGBoost regression, model evaluation, feature-importance analysis, and a Streamlit what-if dashboard.

## Dataset disclaimer

The included `data/edm_synthetic.csv` is **synthetic** and was generated only to make the code runnable end-to-end.

Do not use its metrics as experimental results or claim them as results from the original project. Replace it with your actual project dataset if you are permitted to publish that data.

## Quick start

### 1. Install

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Then:

```bash
pip install -r requirements.txt
```

### 2. Train all models

```bash
python src/train.py
```

This creates six models:

```text
MRR_RandomForest.joblib
MRR_XGBoost.joblib
Ra_RandomForest.joblib
Ra_XGBoost.joblib
TWR_RandomForest.joblib
TWR_XGBoost.joblib
```

### 3. Generate feature-importance plots

```bash
python src/feature_importance.py
```

### 4. Run the dashboard

```bash
streamlit run app/streamlit_app.py
```

### 5. Run command-line what-if analysis

```bash
python src/what_if.py
```

## Inputs

The model takes four EDM process parameters:

| Input | Unit |
|---|---|
| Current | A |
| Pulse-On Time | µs |
| Pulse-Off Time | µs |
| Voltage | V |

Two derived features are added:

- Spark Energy
- Duty Cycle

## Outputs

The models independently predict:

- MRR
- Ra
- TWR

## Model comparison

Both models are trained and evaluated using:

- MAE
- RMSE
- R²

Metrics are saved to `reports/metrics.json`.

## Project workflow

```text
EDM Parameters
      ↓
Feature Engineering
      ↓
Spark Energy + Duty Cycle
      ↓
┌───────────────────────┐
│ Random Forest         │
│ XGBoost               │
└───────────────────────┘
      ↓
MRR / Ra / TWR
      ↓
Feature Importance
      ↓
What-If Analysis
      ↓
Streamlit Dashboard
```

## GitHub

```bash
git init
git add .
git commit -m "Add EDM digital twin ML pipeline"
git branch -M main
git remote add origin https://github.com/<USERNAME>/<REPOSITORY>.git
git push -u origin main
```
