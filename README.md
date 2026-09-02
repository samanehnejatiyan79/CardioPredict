# CardioPredict

Machine-learning estimation of obstructive coronary artery disease from routine
clinical and laboratory data to support pre-angiographic triage.

## Overview

A calibrated, uncertainty-aware ensemble model that estimates the probability of
obstructive coronary artery disease (obstructive CAD) using **only** routine
pre-procedural demographic, clinical and laboratory variables. Developed for
pre-angiographic triage in an angiography-referred cohort.

- **Design:** Single-centre, retrospective development and internal validation.
- **Analytic sample:** N = 1187 patients referred for invasive coronary angiography.
- **Outcome:** Obstructive CAD = ≥50% luminal diameter stenosis in ≥1 major
  epicardial coronary artery (or ≥50% left-main stenosis), binary.
- **Model:** Stacked ensemble of four base learners — TabPFN, LightGBM,
  CatBoost, and a regularized clinical logistic-regression model — combined by
  an age-conditional meta-learner, with stratified probability calibration and
  split-conformal prediction (90% target coverage).
- **Validation:** Repeated nested cross-validation (2 × 5 folds) with
  fold-internal preprocessing; bootstrap 95% CIs; reported in accordance with
  the TRIPOD statement.

## Key results

| Metric | Value (95% CI) |
| --- | --- |
| AUC | 0.866 (0.850–0.891) |
| Sensitivity (threshold 0.73) | 74.0% (70.8–77.0) |
| Specificity (threshold 0.73) | 81.5% (77.6–85.2) |
| Positive predictive value | 88.5% (86.0–91.0) |
| Negative predictive value | 62.0% (58.0–66.0) |
| Accuracy | 76.6% (74.1–79.0) |
| Matthews correlation coefficient | 0.53 |
| Calibration slope / E-O ratio | 0.91 / 1.02 |
| Incremental AUC vs logistic | +0.077 (p<0.001) |
| Conformal gray-zone (target/empirical coverage) | 90% / 90.1% |

## Repository contents

- `outputs/` — generated figures (ROC, calibration, decision-curve, subgroup,
  conformal gray-zone, pipeline schematic) and model artifacts.
- `CardioPredict_Lancet_manuscript.tex` — manuscript source (LaTeX/pandoc).
- `CardioPredict_Lancet_manuscript.html` — compiled manuscript.
- `outputs/manuscript_stats.json`, `outputs/train_prod_report.json`,
  `outputs/predictions.npz`, `outputs/results.txt` — analysis outputs.

## Reproducibility

- Fixed analysis seed: 42
- Development cohort N = 1187; data hash (SHA-256, 16 hex): `fb3af1d8645920f3`
- Software: Python 3.12 · NumPy 1.26.4 · scikit-learn 1.8.0 · LightGBM 4.6.0 ·
  CatBoost 1.2.10 · TabPFN 7.1.1
- Model bundle: `outputs/model_bundle.joblib`

## Data & ethics

De-identified data and full analysis code are available from the corresponding
author on reasonable request, subject to institutional and ethics-committee
approval. **No patient-identifiable data are included in this repository.**

## License

See manuscript for funding and declarations. Correspondence on request.