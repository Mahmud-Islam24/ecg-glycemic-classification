# ecg-glycemic-classification
Code for non-invasive classification of glycemic status (ND, PD, T2D) using ECG-derived HRV and morphological biomarkers with machine learning. Includes preprocessing, feature selection, cross-validation, sampling strategies, SHAP interpretability, and figure generation. Supporting manuscript submitted to npj Digital Medicine.

## Overview

This repository contains the complete analysis pipeline supporting the manuscript:

**“Non-Invasive Classification of Glycemic Status Using ECG-Derived Biomarkers and Machine Learning.”**

We present a reproducible framework for detecting glycemic dysregulation — Normoglycemic (ND), Prediabetes (PD), and Type 2 Diabetes (T2D) — using electrocardiogram (ECG)-derived physiological biomarkers combined with machine learning. The codebase includes preprocessing, feature engineering, model training, validation, interpretability analysis, and publication-quality figure generation.

## Scientific Rationale

Chronic hyperglycemia alters autonomic balance and cardiac electrophysiology.  
This study evaluates whether ECG-derived heart rate variability (HRV) and morphological biomarkers encode sufficient signal to enable non-invasive classification of glycemic state.

The pipeline emphasizes:
- Strict train-only feature selection to prevent leakage
- Stratified cross-validation
- Class imbalance mitigation (Under/Up/SMOTE)
- Model interpretability using SHAP

  ### Feature Extraction
- HRV: SDNN, RMSSD, pNN50, Shannon entropy, Mean HR
- Morphological: PR interval, QT/QTc duration, T-wave amplitude

### Modeling
- Logistic Regression
- Gradient Boosting
- Random Forest

### Evaluation
- ROC-AUC
- Balanced Accuracy
- Sensitivity / Specificity
- AUPRC
- Confusion matrices
- SHAP-based feature attribution

## Repository Structure
ecg-glycemic-classification/
│
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── environment.yml
├── .gitignore
│
├── configs/
│   ├── base.yaml
│   ├── three_class.yaml
│   ├── binary_scenarios.yaml
│
├── src/
│   ├── data/
│   │   ├── loader.py
│   │   └── preprocessing.py
│   │
│   ├── features/
│   │   ├── hrv.py
│   │   ├── morphology.py
│   │   └── feature_selection.py
│   │
│   ├── models/
│   │   ├── classifiers.py
│   │   ├── sampling.py
│   │   └── cross_validation.py
│   │
│   ├── evaluation/
│   │   ├── metrics.py
│   │   ├── confusion_matrix.py
│   │   └── roc_curves.py
│   │
│   ├── interpretability/
│   │   ├── shap_analysis.py
│   │   └── lr_coefficients.py
│   │
│   └── visualization/
│       ├── figure_style.py
│       ├── heatmaps.py
│       └── boxplots.py
│
├── experiments/
│   ├── 01_hr_extraction.py
│   ├── 02_three_class_training.py
│   ├── 03_binary_three_scenarios.py
│   ├── 04_binary_two_scenarios.py
│   ├── 05_fig3_heatmap_rank.py
│   ├── 06_shap_pipeline.py
│   └── run_all.py
│
├── data/
│   ├── README.md
│   ├── raw/          (gitignored)
│   └── processed/    (gitignored)
│
├── outputs/
│   ├── figures/
│   └── tables/
│
└── notebooks/

The current notebook contains: 
our notebook contains scripts that naturally become these experiments/ entry points:

HR extraction pipeline → experiments/01_hr_extraction.py

3-class ND/PD/T2D training → experiments/02_three_class_training.py

Binary CM+ROC (3 scenarios) → experiments/03_binary_three_scenarios.py

Binary CM+ROC (2 scenarios) → experiments/04_binary_two_scenarios.py

Fig 3 heatmap + best model + rank → experiments/05_fig3_heatmap_rank.py

LR coefficients + SHAP → experiments/06_shap_pipeline.py
    ├── 00_frozen_submission_snapshot.ipynb
    └── 01_demo.ipynb
