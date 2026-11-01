# Network Intrusion Detection on NSL-KDD

A machine learning project that classifies network traffic as **normal** or **attack**,
tested on the official NSL-KDD train/test split. The test set contains 17 attack types
that never appear in training, so it measures how well a model handles novel attacks.

## What it does
- Preprocesses 41 traffic features (one-hot encoding for protocol, service and flag; scaling for numeric features)
- Compares 5 models: Logistic Regression, Decision Tree, Random Forest, Neural Net (MLP) and XGBoost
- Trains on 125,973 records and tests on 22,544 unseen records
- Builds a five-class model (Normal, DoS, Probe, R2L, U2R)

## Results (XGBoost, official test set)
| Metric | Value |
|---|---|
| Precision | 96.9% |
| Accuracy | 79.7% |
| ROC-AUC | 0.971 |
| False alarm rate | 2.9% |

Five-class model: detects 84% of DoS and 65% of Probe attacks. R2L and U2R remain weak
because they have very few training examples and resemble normal behavior.

## Key finding
Cross-validation F1 was 99.9%, but test F1 was 78.8%. Random cross-validation only measures
performance on attack types already seen in training, so it overestimates real-world
performance when new attacks appear (distribution shift).

## Tech stack
Python, pandas, NumPy, scikit-learn, XGBoost, Jupyter Notebook

## How to run
1. Clone the repo and install dependencies:
   `pip install pandas numpy scikit-learn xgboost`
2. Open `nsl_kdd_notebook.ipynb`.
3. Run the first cell to download the dataset into `data/`, then run the remaining cells in order.

## Dataset
NSL-KDD (an improved version of KDD Cup 99): https://www.unb.ca/cic/datasets/nsl.html
