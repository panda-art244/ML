# SOC ML Pipeline for Authentication Event Triage

## Overview

This project implements a reproducible machine learning pipeline for prioritizing suspicious authentication events in a Security Operations Center (SOC).

The pipeline analyzes 15-minute authentication windows and generates a ranked daily investigation queue under a strict operational constraint: no more than 8 events can be reviewed per UTC day across 20 synthetic user accounts.

The system is designed to support security analysts, not to automatically block accounts or replace human decision-making.

## Objectives

- Prepare and audit authentication event data.
- Build and compare supervised and unsupervised ML models.
- Evaluate model performance under a limited daily review budget.
- Generate ranked Top-8 investigation queues.
- Analyze false positives and false negatives.
- Develop an operational recommendation for SOC deployment.

## Models

Three approaches were evaluated:

| Model | Type |
|---|---|
| Logistic Regression | Supervised classification |
| Random Forest | Supervised classification |
| Isolation Forest | Unsupervised anomaly detection |

Random Forest was selected based on validation performance.

## Methodology

- Temporal train / validation / test split.
- Feature preprocessing using imputation, encoding and scaling.
- Model training using training data only.
- Daily Top-8 ranking based on model scores.
- Threshold-based comparison.
- Final evaluation on an independent test set.
- Error analysis across user groups.

## Test Results

| Metric | Result |
|---|---:|
| Selected events | 40 |
| True Positives (TP) | 28 |
| False Positives (FP) | 12 |
| True Negatives (TN) | 9,482 |
| False Negatives (FN) | 78 |
| Precision@8 | 0.700 |
| Recall@8 | 0.264 |
| Maximum reviews per day | 8 |

## Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Google Colab
- Jupyter Notebook

## Repository Contents

- `soc-ml-triage.ipynb` — complete notebook with data preparation, model training, evaluation and error analysis.

## Limitations

The experiment uses synthetic authentication data representing 20 accounts over a limited time period. The results do not establish real-world SOC effectiveness.

The model is intended as a decision-support tool. All selected events require human review.

## Future Improvements

- Evaluate the pipeline on anonymized real-world authentication logs.
- Investigate false negatives and improve recall.
- Monitor model drift and performance over time.
- Test the system in shadow mode before deployment.
