# AML Venetoclax Resistance

Code and resources for key figures from the study:

---

## Overview
This repository contains scripts and notebooks to reproduce selected figures from the paper.  
The goal is to provide transparency and reproducibility for the main analyses.

---

## Contents

#### `bootstrap_iteration.py`
Runs one bootstrap iteration of **L1-regularized logistic regression**:  
- Resamples data, adds noise, fits model.  
- Returns: selection mask (`|coef| > epsilon`), coefficients, and OOB indices.

---

#### `fit_lasso_logistic_bootstrap.py`
Runs multiple bootstrap iterations in parallel:  
- Aggregates coefficients into a matrix `(n_bootstrap × n_features)`.  
- Returns: `coef_matrix` and OOB indices list.

---

#### `summarize_bootstrap_coefficients.py`
Summarizes bootstrap results:  
- Computes feature selection frequency, mean, and std.  
- Returns: selected features and summary stats.


---

## Status
**Note:** This repository is under active development. Additional scripts, data, and documentation will be added soon.

```python
# To run the code:
gene_names = X.columns
n_bootstrap = 10000
epsilon = 0.01
random_state = 2025
n_jobs = -1
threshold_ratio = 0.8

params = {
    'C': 10,
    'class_weight': 'balanced',
    'max_iter': 10000,
}

coef_matrix, oob_indices = fit_lasso_logistic_bootstrap(
    X.values, 
    y, 
    gene_names=gene_names,        
    n_bootstrap=n_bootstrap,
    epsilon=epsilon,
    n_jobs=n_jobs,               
    random_state=random_state,
    params=params
)

summary = summarize_bootstrap_coefficients(
    coef_matrix=coef_matrix,
    gene_names=gene_names,
    threshold_ratio=threshold_ratio
)
```

### Data Assumptions

- **X**: A numeric matrix where  
  - Rows represent **samples**  
  - Columns represent **features (genes)**  
  - Values are **TPM-normalized**, then **log-transformed**, and finally **Z-score standardized** across samples.

- **y**: A binary list or array of labels (`0` and `1`), corresponding to the sample classes.

