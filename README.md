# DataSprint 2026 - Predicting Financial Wellbeing Among Kenyan Adults

Multiclass classification (Improved / Stayed the same / Worsened) on the 2024 FinAccess Household Survey.

| File | What it is |
|---|---|
| `finaccess2024_datasprint.xlsx` | Input data (20,871 rows x 28 columns) |
| `index.ipynb` | Full analysis: cleaning, EDA, feature engineering, five models, tuning, robustness check, permutation importance |
| `DataSprint2026_Presentation.pptx` | Slide deck (numbers match the notebook) |
| `DataSprint2026_Visualisations.pdf` | All 20 figures from the notebook, with captions |
| `requirements.txt` | Pinned packages used by the notebook |

## Reproduce
```
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace index.ipynb
```
All randomness uses `SEED = 42`. Set `FAST = True` in the first code cell for a quick smoke test (about 3 minutes instead of about 15).

## Method in brief
- 80/20 stratified split; encoding, scaling and SMOTENC live inside an `imblearn` pipeline so they are fitted on training folds only.
- Models: Logistic Regression, Random Forest, Random Forest + SMOTENC, LightGBM, LightGBM + SMOTENC (LightGBM tuned with a 24-iteration randomised search). Selection is by stratified 5-fold CV weighted F1, not by test score.
- Per-class decision weights are tuned on out-of-fold predictions; the test set is used once.

## Headline results (held-out test set)
| Model | CV weighted F1 | Test weighted F1 |
|---|---|---|
| Logistic Regression | 0.517 | 0.515 |
| Random Forest | 0.535 | 0.538 |
| Random Forest + SMOTENC | 0.529 | 0.531 |
| LightGBM | 0.537 | 0.527 |
| **LightGBM + SMOTENC** | **0.548** | **0.541** (0.542 with tuned class weights) |

Test macro-F1 0.486, accuracy 0.554. Without the self-reported resilience items test weighted F1 is 0.520.

## Caveats
Cross-sectional survey, so findings are associations. The file has no survey weights, so rates describe the sample (n = 20,866), not national totals.
