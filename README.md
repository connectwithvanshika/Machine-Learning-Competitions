# House Price Prediction using Machine Learning

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Scikit--Learn-ML-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Random%20Forest-Regressor-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Kaggle-Competition-blueviolet?style=for-the-badge" />
</p>

---

## ▌Project Overview

This project focuses on predicting residential property prices using a **Random Forest Regression Model** trained on the Iowa Housing Dataset.

The model analyzes property characteristics such as:

✔ Lot Area
✔ Year Built
✔ Floor Space
✔ Number of Bedrooms
✔ Bathrooms
✔ Total Rooms

and predicts the final **Sale Price** of a house.

---

## ▌Problem Statement

Real estate valuation plays a crucial role in property investment and market analysis.

The goal of this project is to build a machine learning model capable of estimating house prices based on property features and generate predictions for unseen houses.

---

## ▌Dataset Information

Dataset Source:

• Iowa Housing Dataset
• Kaggle Machine Learning Competition

Target Variable:

```text
SalePrice
```

---

## ▌Features Used

| Feature      | Description              |
| ------------ | ------------------------ |
| LotArea      | Lot size in square feet  |
| YearBuilt    | Construction year        |
| 1stFlrSF     | First floor area         |
| 2ndFlrSF     | Second floor area        |
| FullBath     | Number of full bathrooms |
| BedroomAbvGr | Bedrooms above ground    |
| TotRmsAbvGrd | Total rooms above ground |

---

## ▌Technology Stack

```text
Python
Pandas
NumPy
Scikit-Learn
Jupyter Notebook
Kaggle
```

---

## ▌Machine Learning Workflow

```text
Dataset
   │
   ▼
Feature Selection
   │
   ▼
Train-Test Split
   │
   ▼
Random Forest Regressor
   │
   ▼
Model Evaluation
   │
   ▼
Price Prediction
   │
   ▼
Kaggle Submission
```

---

## ▌Model Training

```python
rf_model = RandomForestRegressor(random_state=1)

rf_model.fit(train_X, train_y)
```

---

## ▌Model Evaluation

Metric Used:

### Mean Absolute Error (MAE)

```text
Validation MAE: 21,857
```

A lower MAE indicates better prediction accuracy.

---

## ▌Prediction Generation

```python
test_preds = rf_model.predict(test_X)
```

Export predictions:

```python
output = pd.DataFrame({
    "Id": test_data.Id,
    "SalePrice": test_preds
})

output.to_csv("submission.csv", index=False)
```

---

## ▌Project Structure

```text
House-Price-Prediction/
│
├── train.csv
├── test.csv
├── notebook.ipynb
├── submission.csv
├── README.md
│
└── models/
```

---

## ▌Results

| Metric           | Value                   |
| ---------------- | ----------------------- |
| Model            | Random Forest Regressor |
| Validation MAE   | 21,857                  |
| Competition Type | Regression              |

---

## ▌Future Improvements

□ Hyperparameter Tuning

□ Feature Engineering

□ Missing Value Handling

□ Cross Validation

□ XGBoost

□ LightGBM

□ Ensemble Models

These improvements can significantly increase prediction accuracy.

---

## ▌Key Learnings

◆ Data Preprocessing

◆ Feature Selection

◆ Regression Analysis

◆ Random Forest Algorithms

◆ Model Evaluation

◆ Kaggle Competition Workflow

◆ End-to-End Machine Learning Pipeline

---

## ▌Author

### Vanshika Yadav

Machine Learning • Artificial Intelligence • Data Science

GitHub: https://github.com/connectwithvanshika

---

### If you found this project useful, consider giving it a star ⭐
