# AML Venetoclax Resistance

Code and resources for key figures from the study:

---

## Overview
This repository contains scripts and notebooks to reproduce selected figures from the paper.  
The goal is to provide transparency and reproducibility for the main analyses.

---

## Contents
- `XXX.ipynb`

---

## Status
**Note:** This repository is under active development. Additional scripts, data, and documentation will be added soon.

```python
# To run the code:
n_bootstrap = 10000

gene_names = X.columns

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
    epsilon=0.01,
    n_jobs=-1,               
    random_state=42,
    params=params
)

summary = summarize_bootstrap_coefficients(
    coef_matrix=coef_matrix,
    gene_names=gene_names,
    threshold_ratio=0.8
)
```


