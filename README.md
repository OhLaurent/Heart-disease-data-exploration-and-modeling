# Exploring Heart Disease Risk: An Analysis and Modelling Study

An exploratory analysis and modelling study of heart disease risk from clinical features, with an emphasis on understanding what the data reveals and how well different models can capture those signals.

## Motivation

Heart disease prediction is a well-studied problem, but it remains a rich domain for exploration. The clinical features available — chest pain type, exercise angina, max heart rate, vessel count, thallium scan results — tell a story about how the body responds under stress. This project is an attempt to read that story through data: to understand feature distributions, inter-variable relationships, and which signals most strongly separate presence from absence of disease.

The modelling work is guided by a question common in screening contexts: given the cost asymmetry between false negatives and false positives, how should thresholds be set? That question drives the evaluation choices throughout.

## What Was Found

- Logistic Regression with feature engineering matched Random Forest and XGBoost in ROC-AUC, suggesting the relationships in this dataset are largely linear after appropriate transformations.
- Test ROC-AUC: **0.9538** — CV ROC-AUC: **0.9527 ± 0.0008** (baseline), **0.9528 ± 0.0008** (feature-engineered).
- Threshold analysis: setting the decision boundary at **0.3796** achieves recall ≥ 0.90 with interpretable trade-offs in precision.
- Top predictive features: chest pain type, thallium scan outcomes, number of major vessels, exercise-induced angina, and maximum heart rate.

## Notebooks

### 1. Exploratory Analysis — [notebooks/01_exploratory_analysis.ipynb](notebooks/01_exploratory_analysis.ipynb)
- Distribution analysis of numerical and categorical features.
- Target class balance and relationship to individual predictors.
- Correlation structure and inter-feature patterns.
- Data quality checks and cleaning; cleaned dataset saved for modelling.

### 2. Modelling and Evaluation — [notebooks/02_modelling.ipynb](notebooks/02_modelling.ipynb)
- Baseline pipelines and feature-engineered variants.
- Candidate model comparison: Logistic Regression, Random Forest, XGBoost.
- Experiment tracking with MLflow to keep results organised and comparable.
- Hyperparameter search and model selection rationale.
- Threshold analysis: visualising precision/recall trade-offs and selecting an operating point.
- Permutation feature importance to understand what drove model decisions.

## Dataset

- Raw: `notebooks/data/heart_disease.csv`
- Cleaned: `notebooks/data/heart_disease_cleaned.csv`
- Approximately 630,000 rows (synthetically expanded clinical-style dataset).
- Target: `Heart Disease` — Presence vs Absence.

## Tech Stack

- Python 3.12+
- pandas, numpy, scipy
- scikit-learn
- xgboost, catboost
- matplotlib, seaborn, statsmodels
- MLflow for experiment tracking
- Jupyter Notebook
- uv for environment/dependency management

## Repository Structure

```text
.
|- notebooks/
|  |- 01_exploratory_analysis.ipynb
|  |- 02_modelling.ipynb
|  |- data/
|     |- heart_disease.csv
|     |- heart_disease_cleaned.csv
|- artifacts/
|  |- models/
|     |- 02_modelling_final_pipeline.joblib
|     |- 02_modelling_best_estimator.joblib
|     |- 02_modelling_threshold_config.yaml
|     |- best_model_feature_importance.csv
|  |- plots/
|- mlruns/
|- pyproject.toml
|- README.md
```

## Getting Started

### 1) Install dependencies

```bash
uv sync
```

### 2) Launch notebooks

```bash
uv run jupyter notebook
```

## Notes

- This project is focused on exploration and analysis — it is not intended as a deployment-ready system.
- It does not provide clinical diagnosis and should not be used as a medical decision tool.

## License

MIT License.
