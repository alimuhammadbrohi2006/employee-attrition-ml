# Reproducibility and evaluation

## Environment

Install `requirements.txt` in a fresh Python environment, open `LAB07_OPEN_ENDED.ipynb` and run all cells from top to bottom. The requirements list reflects the notebook imports; exact original package versions are not recorded, and a fresh execution has not been verified. Record `python --version` and `python -m pip freeze` when reproducing the experiment.

The saved notebook uses the deprecated `kagglehub.load_dataset` method. The dependency is conservatively bounded below major version 1, but this does not guarantee that the legacy method remains available. If it is missing, consult the installed KaggleHub documentation and replace `kagglehub.load_dataset` with `kagglehub.dataset_load` if supported, retaining the adapter, dataset identifier and CSV filename. The original notebook remains unchanged.

## Data access

Dataset: [IBM HR Analytics Employee Attrition](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset). Internet access and possibly Kaggle authentication are required. Never commit Kaggle credentials or private employee data.

## Experimental protocol

- Positive class: Attrition = Yes (1).
- Train/test: 80/20 stratified split, random state 42; 1,176 training and 294 test rows in saved outputs.
- Preprocessing: median imputation and scaling for numerical variables; most-frequent imputation and one-hot encoding for categorical variables. Fit on training data only.
- Compare Logistic Regression, Decision Tree and Random Forest using accuracy and binary F1-score. Inspect confusion matrices for false positives and false negatives.
- Feature importance is computed separately for a fitted Random Forest and is not causal evidence.

## Interpretation

The saved outputs report 86.05% accuracy and 0.4384 F1 for Logistic Regression, 83.67% and 0.2727 for Decision Tree, and 85.03% and 0.2414 for Random Forest. These are rounded results from one run, not independently replicated results. Because the positive class is uncommon, compare with a majority-class baseline and prioritize precision, recall and F1 over accuracy alone. For future experiments, use cross-validation and tune thresholds on validation data, not the final test set. Assess fairness and privacy before considering any practical use; this notebook is not suitable for individual employment decisions.
