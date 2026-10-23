# Financial Health Classification using Machine Learning

## Project Overview

DataSprint 2026 - predicting whether a Kenyan adult's financial situation **Improved**, **Stayed the same** or **Worsened**, using the 2024 FinAccess Household Survey (20,871 respondents, 28 columns). Five classification models are compared, and the drivers behind the predictions are analysed.

The project was developed as part of a Data Science / Machine Learning coursework challenge (SDC x iLab Africa, Strathmore University).

---

## Objective

To build a classification model capable of identifying financial health levels based on demographic, socioeconomic and financial resilience indicators and engineered features. The evaluation metric is **weighted F1-score**, because the classes are imbalanced (52.6% Worsened, 26.9% Stayed the same, 20.5% Improved).

---

## Repository Structure

```
├── index.ipynb                          # Main notebook containing the entire workflow
├── DataSprint2026_Presentation.pptx     # Slide deck (numbers match the notebook)
├── DataSprint2026_Visualisations.pdf    # All 20 figures from the notebook, with captions
├── finaccess2024_datasprint.xlsx        # Dataset
├── requirements.txt                     # Pinned packages used by the notebook
└── README.md                            # Project documentation
```

---

## Workflow

### 1. Data Cleaning
- Remove 5 duplicate rows
- `barriers_bank` / `barriers_mobile_money`: missing or `0` means "No barrier"
- Tidy text labels and merge "Don't know" / "Refused" marital-status answers

### 2. Exploratory Data Analysis (EDA)
- Class imbalance and target distribution
- Shocks, emergency-fund access, product usage, loan default, education and income against the outcome
- County and rural/urban views

### 3. Feature Engineering
- `financial_health_score` (0-4 sum of four resilience indicators)
- `has_any_savings`, `shock_no_savings`, `fully_excluded`

### 4. Model Development
Encoding, scaling and SMOTENC sit inside an `imblearn` pipeline, so they are fitted on training folds only. Models are compared with stratified 5-fold cross-validation, and the model is selected on CV score. Per-class decision weights are tuned on out-of-fold predictions and the 20% test set is used once.

| Model | CV weighted F1 | Test weighted F1 |
|---|---|---|
| Logistic Regression | 0.517 | 0.515 |
| Random Forest | 0.535 | 0.538 |
| Random Forest + SMOTENC | 0.529 | 0.531 |
| LightGBM | 0.537 | 0.527 |
| **LightGBM + SMOTENC** | **0.548** | **0.541** (0.542 with tuned class weights) |

LightGBM + SMOTENC was selected as the final model. The gain over the Random Forest is clear in cross-validation but small on the test set. Test macro-F1 is 0.486 and accuracy 0.554. Without the self-reported resilience items, test weighted F1 is 0.520.

---

## Technologies Used

- Python
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-Learn
- imbalanced-learn (SMOTENC)
- LightGBM

---

## Evaluation Metric

- Weighted F1-score (primary), macro-F1 and accuracy
- Per-class precision / recall / F1 and confusion matrices
- Permutation importance for the drivers

---

## Running the Project

### Clone the Repository

```bash
git clone https://github.com/Fadhili-22/iLab-Datasprint-Hackathon.git
cd iLab-Datasprint-Hackathon
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run

Open `index.ipynb` and run all cells, or execute it from the command line:

```bash
jupyter nbconvert --to notebook --execute --inplace index.ipynb
```

All randomness uses `SEED = 42`. Set `FAST = True` in the first code cell for a quick smoke test (about 3 minutes instead of about 15).

---

## Results

- Logistic Regression is the baseline (test weighted F1 0.515).
- Tree models do better; LightGBM + SMOTENC with tuned class weights is best (0.542), strongest on "Worsened" and weakest on "Stayed the same".
- Top drivers by permutation importance: county, age group, monthly income, financial health score and emergency-fund access.

Caveat: the survey is cross-sectional, so findings are associations, and the file has no survey weights, so rates describe the sample (n = 20,866), not national totals.

---

## Team Members

- Member 1: Munyua Njenga Fadhili
- Member 2: Vanessa Njoki Gikebe
- Member 3: Brandon Mecker Musyoka

---

## License

This repository is intended for academic and educational purposes.
