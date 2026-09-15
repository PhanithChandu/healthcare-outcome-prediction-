# healthcare-outcome-prediction

# Healthcare Outcome Prediction — Disease Progression Modeling

An end-to-end machine learning project that predicts a **continuous diabetes disease-progression outcome** from baseline patient measurements.

## Project overview

Healthcare datasets frequently contain noisy measurements, different feature scales, and variables that require careful preprocessing. This project builds and compares:

- **ElasticNet Regression** — regularized linear baseline with L1 + L2 penalties
- **Gradient Boosting Regressor** — nonlinear ensemble model
- **XGBoost Regressor** — gradient-boosted tree model
- Missing-value imputation with a median strategy
- Cross-validation and hold-out test evaluation
- **SHAP** model interpretability
- **LIME** local explanations
- Subgroup performance analysis using age and sex-derived groups
- RMSE, MAE and R² evaluation

> **Important:** This is an educational machine-learning project, not a clinical decision-support system. The scikit-learn diabetes dataset is a small benchmark dataset and should not be treated as representative clinical data.

## Dataset

The project uses the **Diabetes regression dataset distributed with scikit-learn** (`sklearn.datasets.load_diabetes`).

The local copy is provided at:

`data/diabetes_progression.csv`

A data dictionary is provided at:

`data/data_dictionary.csv`

The original dataset contains 442 observations and 10 baseline features. The target is a quantitative measure of disease progression one year after baseline.

The feature values in the scikit-learn dataset are standardized/normalized representations rather than raw clinical laboratory units.

## Repository structure

```text
healthcare-outcome-prediction/
│
├── data/
│   ├── diabetes_progression.csv
│   └── data_dictionary.csv
│
├── notebooks/
│   └── 01_healthcare_outcome_prediction.ipynb
│
├── src/
│   ├── __init__.py
│   ├── train.py
│   └── explain.py
│
├── reports/
│   └── figures/
│
├── .gitignore
├── LICENSE
├── requirements.txt
└── README.md
```

## Installation

Python 3.10+ is recommended.

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
cd healthcare-outcome-prediction

python -m venv .venv
```

### Windows

```bash
.venv\Scripts\activate
```

### macOS/Linux

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Run the project

Train all models and generate evaluation outputs:

```bash
python src/train.py
```

Generate SHAP and LIME explanations:

```bash
python src/explain.py
```

The scripts create:

```text
reports/
├── model_metrics.csv
├── subgroup_metrics.csv
└── figures/
    ├── model_comparison.png
    ├── actual_vs_predicted.png
    ├── shap_summary.png
    └── lime_explanation.html
```

## Methodology

### 1. Data preparation

1. Load the local CSV.
2. Separate predictors and target.
3. Inspect missing values.
4. Use a `Pipeline` so imputation and modeling are learned only from training data.
5. Split the data into training and test sets.

### 2. Exploratory analysis

The notebook examines:

- Feature distributions
- Correlations
- Target distribution
- Relationships between BMI, blood pressure and disease progression
- Missing-value profile

### 3. Models

**ElasticNet**

Combines L1 and L2 regularization. It provides a useful interpretable linear benchmark and can shrink less useful coefficients toward zero.

**Gradient Boosting**

Captures nonlinear relationships and feature interactions.

**XGBoost**

A high-performance gradient boosting implementation commonly used for structured/tabular data.

### 4. Evaluation

Models are evaluated on the untouched test set using:

- **RMSE:** penalizes larger errors more strongly
- **MAE:** average absolute prediction error
- **R²:** proportion of target variance explained by the model

The project also performs cross-validation during model selection.

### 5. Interpretability

**SHAP** is used for global and per-feature explanations.

**LIME** is used to create a local explanation for an individual prediction.

Interpretability results are intended to describe model behavior, not establish medical causation.

### 6. Fairness / subgroup consistency

Performance is compared across:

- Sex-derived groups
- Age-derived groups

The subgroup analysis reports MAE, RMSE and R² for each group. Because this is a small benchmark dataset, subgroup results should be interpreted cautiously and are not evidence of clinical fairness.

## Expected outputs

After running the scripts, check:

```text
reports/model_metrics.csv
reports/subgroup_metrics.csv
reports/figures/
```

Your exact metric values may vary slightly with library versions.

## Reproducibility

A fixed random seed is used where applicable. All preprocessing steps are implemented inside scikit-learn pipelines to reduce train/test leakage.

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- SHAP
- LIME
- Matplotlib
- Seaborn
- Jupyter

## Resume-ready project description

**Healthcare Outcome Prediction | Python, Scikit-learn, XGBoost, SHAP, LIME**

Developed an end-to-end regression pipeline to predict continuous diabetes disease progression from baseline patient measurements. Compared ElasticNet, Gradient Boosting and XGBoost models using RMSE, MAE and R², implemented leakage-safe missing-value imputation, analyzed subgroup performance, and used SHAP/LIME to explain global and individual model predictions.

## GitHub upload checklist

Upload these files/folders:

- `README.md`
- `requirements.txt`
- `.gitignore`
- `LICENSE`
- `data/diabetes_progression.csv`
- `data/data_dictionary.csv`
- `src/train.py`
- `src/explain.py`
- `src/__init__.py`
- `notebooks/01_healthcare_outcome_prediction.ipynb`

You do **not** need to upload your virtual environment (`.venv/`) or Python cache files.

## Suggested GitHub repository name

`healthcare-outcome-prediction`

## Suggested repository description

`End-to-end healthcare regression project predicting diabetes disease progression with ElasticNet, Gradient Boosting, XGBoost, SHAP, LIME and subgroup analysis.`
