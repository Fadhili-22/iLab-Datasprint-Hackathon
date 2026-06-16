# Financial Health Classification using Machine Learning

##  Project Overview

This project aims to predict an individual's financial health status using machine learning techniques. The dataset contains demographic, socioeconomic, and financial resilience indicators, and multiple classification models were developed and evaluated to determine the most effective approach.

The project was developed as part of a Data Science / Machine Learning coursework challenge.

---

##  Objective

To build a classification model capable of identifying financial health levels based on various indicators and engineered features.

---

## Repository Structure

```
├── index.ipynb                 # Main notebook containing the entire workflow
├── DataSprint2026_Visualisations   # Exported visualizations
├── README.md                   # Project documentation
└──finaccess2024_datasprint     # Dataset (if publicly shareable)
```

---

## Workflow

### 1. Data Cleaning
- Handling missing values
- Data inspection and validation
- Encoding categorical variables

### 2. Exploratory Data Analysis (EDA)
- Distribution analysis
- Correlation analysis
- Class imbalance examination
- Feature visualization

### 3. Feature Engineering
Several features were created to improve predictive performance, including:

- Financial Health Score
- Composite resilience indicators
- Encoded demographic variables
- Derived socioeconomic features

### 4. Model Development

Three machine learning models were trained and evaluated:

| Model | F1 Score |
|---------|---------|
| Logistic Regression | 0.514 |
| Random Forest | 0.546 |


Random Forest achieved the best performance and was selected as the final model.

---

## ⚙️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn

---

## 📊 Evaluation Metric

The models were evaluated primarily using:

- Weighted Score
- Classification Report
- Confusion Matrix

F1 Score was chosen because it balances precision and recall, making it suitable for imbalanced classification problems.

---

## 🚀 Running the Project

### Clone the Repository

```bash
git clone https://github.com/your-username/your-repository.git
cd your-repository
```

### Install Dependencies

```bash
pip install -r requirements.txt
```


Open:

index.ipynb
```

---

## 📈 Results

Among the models tested:

- Logistic Regression provided a baseline performance.
- Random Forest significantly improved prediction accuracy and delivered the highest F1 score and overall best classification performance.

---

## 👥 Team Members

- Member 1: Munyua Njenga Fadhili
- Member 2: Vanessa Njoki Gikebe
- Member 3: Brandon Mecker Musyoka

---

## 📜 License

This repository is intended for academic and educational purposes.
