# Dataset: Ionosphere (UCI Machine Learning Repository)

## Source
- **Name:** Ionosphere Dataset  
- **Origin:** UCI Machine Learning Repository  
- **URL:** https://archive.ics.uci.edu/ml/datasets/ionosphere  
- **License:** Public Domain / CC BY 4.0  

The notebooks load the data via `sklearn.datasets.fetch_openml`; no manual download or path setup is needed.

## Dataset files in this folder
- **X_train.npy, X_test.npy, y_train.npy, y_test.npy** — Preprocessed train/test arrays (normalised features, labels in {+1,-1}) produced by **task 2 1.ipynb** when run from `partB/`. Task 3 1 loads these if present; otherwise it fetches and preprocesses from OpenML.

## Description
The Ionosphere dataset consists of radar returns from the ionosphere collected by a system in Goose Bay, Labrador. Each instance is either classified as **"good"** (radar returns show some structure in the ionosphere) or **"bad"** (signals passed through without structure).

- **Samples:** 351  
- **Features:** 34 (continuous numeric)  
- **Classes:** 2 (binary: 'g' = good, 'b' = bad, mapped to +1 / -1 in the notebooks)  
- **Missing values:** None  

## Why this dataset?
Ionosphere is a good fit for reproducing the FGM paper because:
1. It is **binary classification** — same setting as in the paper (Section 2: \(y_i \in \{\pm 1\}\)).
2. It has **34 real-valued features** with known redundancy and correlation — exactly the setting where sparse feature selection (budget \(B\)) is useful.
3. It is **not** one of the paper’s datasets (WDBC, USPS, Breast Cancer, Leukemia, etc.), as required in Part B.
4. It is freely available and can be loaded in code via `fetch_openml` with no manual steps.

## How it is used
- **task 2 1.ipynb:** Loads dataset via `fetch_openml`, preprocesses, saves arrays to `data/`.
- **task 2 2.ipynb, task 2 3.ipynb:** Load and preprocess from OpenML (or use data from task 2 1).
- **task 3 1.ipynb:** Loads from `data/X_train.npy` etc. if present; otherwise fetches and preprocesses.

Run all notebooks from the **partB/** directory so paths `results/` and `data/` resolve correctly.

## Loading in code
The notebooks use:
```python
from sklearn.datasets import fetch_openml
ionosphere = fetch_openml(name='ionosphere', version=1, as_frame=True, parser='auto')
```
No manual download or path setup is needed.

## Preprocessing
- **Normalisation:** Zero mean, unit variance (StandardScaler) on the training set only; same scaler applied to the test set (paper Section 3.1).
- **Labels:** 'g' → +1, 'b' → -1.
