# Cars24 Used-Car Price Prediction

A reproducible Linear Regression case study for predicting used-car selling prices from vehicle attributes.

## Project contents

- `Linear_regression_cars24_case_study.ipynb` — polished notebook covering EDA, preprocessing, model training, evaluation, and residual diagnostics.
- `requirements.txt` — Python dependencies.
- `cars24-car-price-cleaned.csv` — **not included**; provide the dataset locally before running the notebook.

## Dataset setup

Place `cars24-car-price-cleaned.csv` in the repository root. The notebook expects a cleaned dataset with a numeric `selling_price` target and vehicle attributes, including `make` and `model`.

The dataset is not bundled because its distribution rights/source details were not established here. Add a source link and license information to this README if you are permitted to redistribute or reference the original dataset.

## Run locally

Python 3.10+ is recommended.

```bash
# Create and activate a virtual environment
python -m venv .venv

# Windows PowerShell
.venv\\Scripts\\Activate.ps1

# macOS/Linux
source .venv/bin/activate

# Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

Open `Linear_regression_cars24_case_study.ipynb` and run the cells from top to bottom.

## Methodology

1. Inspect data types, missing values, and target distribution.
2. Split into train and test sets before target encoding to avoid target leakage.
3. Learn category means from training data only; unseen test categories fall back to the training target mean.
4. Standardize features using parameters learned from the training set.
5. Train `sklearn.linear_model.LinearRegression`.
6. Evaluate with R², MAE, and RMSE on train and test data.
7. Inspect residuals and run Breusch–Pagan and normality diagnostics.

## Important interpretation notes

- R² is not the percentage of predictions that are correct.
- Residual diagnostics help identify model limitations; they do not automatically determine whether a model is useful.
- The Shapiro–Wilk test can be overly sensitive in large samples. The notebook uses a reproducible sample of at most 5,000 residuals for this test and recommends interpreting it alongside the Q–Q plot.
- Target encoding can overfit high-cardinality categories such as `model`; consider smoothing or out-of-fold target encoding for a more robust experiment.
- Treat this as a learning case study, not a production-ready pricing system.

## Reproducibility

The train/test split and sampling operations use a fixed random seed (`42`).
