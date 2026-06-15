# Patient Comorbidity Risk Assessment Dataset

## Overview

This is a synthetic but clinically-informed dataset simulating a hospital-style patient risk assessment registry. It contains **10,000 unique patient records** across **20 columns**, covering demographics, lifestyle factors, chronic disease status, vital signs, lab values, and two computed risk scores.

Unlike purely random synthetic data, every field here is generated using realistic medical relationships — older age, higher BMI, smoking, poor lab values, and multiple comorbidities all interact to influence disease prevalence and the final risk scores. The dataset also includes natural class imbalance (severe multi-disease cases are rarer than healthy/moderate cases) and realistic missingness (5–8% blanks in selected clinical fields), making it well-suited for:

- Exploratory Data Analysis (EDA)
- Missing value handling / imputation practice
- Feature engineering
- Binary classification (e.g., predicting Diabetes, Hypertension, CKD)
- Regression / risk scoring (Heart Attack Risk %, Mortality Risk %)
- General healthcare AI / ML model benchmarking

---

## Column-by-Column Description

### 1. `Patient_ID`
**Type:** String (unique identifier)
Unique patient identifier in the format `PT100001`–`PT110000`. Used purely for record identification — not a predictive feature.

### 2. `Age`
**Type:** Integer (18–95)
Patient's age in years. Follows a roughly normal distribution centered around 58, reflecting a hospital population skewed toward middle-aged and older adults. Age is the single strongest driver of disease prevalence and risk scores in this dataset.

### 3. `Gender`
**Type:** Categorical — `Male`, `Female`
Roughly balanced split (~49% Male / ~51% Female).

### 4. `BMI`
**Type:** Float (15.0–50.0)
Body Mass Index (kg/m²). Centered around ~27.5 (overweight range), with a spread covering underweight to severely obese patients. Higher BMI increases the likelihood of diabetes, hypertension, liver disease, and elevated risk scores.
*~6–7% missing values.*

### 5. `Smoking_Status`
**Type:** Categorical — `Never`, `Former`, `Current`
Smoking history. Older patients are slightly more likely to fall into the "Former" category. Current smokers carry the highest weight in both the Heart Attack Risk and Mortality Risk calculations.
*~6% missing values.*

### 6. `Alcohol_Consumption`
**Type:** Categorical — `None`, `Low`, `Moderate`, `High`
Self-reported alcohol consumption level. "High" and "Moderate" consumption increase the probability of liver disease.
*~7% missing values.* ⚠️ Note: the category value `None` is a **literal text label** ("non-drinker"), not a missing cell — true missing values appear as empty cells. Use `keep_default_na=False` in pandas to avoid pandas auto-converting the text "None" to NaN.

### 7. `Physical_Activity_Level`
**Type:** Categorical — `Low`, `Moderate`, `High`
Patient's typical physical activity level. "High" activity acts as a protective factor, reducing both Heart Attack Risk and Mortality Risk; "Low" activity slightly increases resting heart rate.
*~7% missing values.*

### 8. `Diabetes`
**Type:** Binary (0 = No, 1 = Yes)
Diabetes diagnosis flag. Probability increases with age and BMI (~8.3% overall prevalence). Strongly linked to elevated `HbA1c`, and increases the likelihood of Chronic Kidney Disease.

### 9. `Hypertension`
**Type:** Binary (0 = No, 1 = Yes)
Hypertension diagnosis flag. Probability increases with age and BMI (~20.3% overall prevalence). Directly drives up `Systolic_BP` and `Diastolic_BP`, and is one of the strongest contributors to both risk scores.

### 10. `Chronic_Kidney_Disease`
**Type:** Binary (0 = No, 1 = Yes)
CKD diagnosis flag (~5.2% overall prevalence). Probability rises sharply with age and is significantly more common in patients who already have diabetes and/or hypertension — patients with *both* conditions show roughly a 5–7x higher CKD rate than patients with neither.

### 11. `Liver_Disease`
**Type:** Binary (0 = No, 1 = Yes)
Liver disease flag (~6.1% overall prevalence). Driven primarily by alcohol consumption (High/Moderate) and elevated BMI (NAFLD-style pattern), with a smaller age contribution.

### 12. `Cholesterol_Level`
**Type:** Integer (100–400 mg/dL)
Total cholesterol. Mean increases with age, BMI, and diabetes status. Elevated cholesterol is a key contributor to Heart Attack Risk.
*~5.8% missing values.*

### 13. `Systolic_BP`
**Type:** Integer (80–220 mmHg)
Systolic blood pressure. Strongly elevated in patients with `Hypertension = 1`, with smaller contributions from age and BMI.
*~5.7% missing values.*

### 14. `Diastolic_BP`
**Type:** Integer (50–140 mmHg)
Diastolic blood pressure. Also elevated by hypertension status, age, and BMI, and constrained to remain physiologically below the corresponding systolic value.
*~5.7% missing values.*

### 15. `Resting_Heart_Rate`
**Type:** Integer (40–140 bpm)
Resting heart rate. Increased by current/former smoking status and low physical activity; decreased by high physical activity.
*~7% missing values.*

### 16. `HbA1c`
**Type:** Float (4.0–14.0 %)
Glycated hemoglobin — a key diabetes marker. Non-diabetic patients cluster tightly around ~5.0–5.6%, while diabetic patients show a much higher mean (~7.6%+) with wider variance, reflecting real-world glycemic control differences.
*~5.4% missing values.*

### 17. `Family_History_CVD`
**Type:** Binary (0 = No, 1 = Yes)
Whether the patient has a family history of cardiovascular disease (~24.8% prevalence). Increases Heart Attack Risk but is not used in the Mortality Risk calculation, reflecting its more specific (CVD-focused) clinical relevance.

### 18. `Medication_Adherence_Percentage`
**Type:** Integer (0–100)
Self-reported / tracked medication adherence percentage. Tends to be lower in patients with more comorbidities (diabetes + hypertension + CKD + liver disease). Adherence above ~80% generally lowers both risk scores; lower adherence increases them.
*~7.7% missing values.*

### 19. `Heart_Attack_Risk_Percentage` 🎯 *(Target)*
**Type:** Float (0.0–100.0)
Composite, formula-driven heart attack risk score. Increases with age, smoking status, cholesterol, hypertension, diabetes, BMI, family history of CVD, and systolic blood pressure; decreases with high physical activity and strong medication adherence. The distribution is right-skewed (most patients fall in the low-risk range, with a smaller tail of high-risk patients), mimicking real-world class imbalance.

### 20. `Mortality_Risk_Percentage` 🎯 *(Target)*
**Type:** Float (0.0–100.0)
Composite, formula-driven overall mortality risk score. Increases with age, diabetes, hypertension, chronic kidney disease, smoking, BMI, cholesterol, and HbA1c; decreases with high physical activity and strong medication adherence. Like the heart attack score, it follows a right-skewed distribution with a long tail toward high-risk patients.

---

## Missing Data Pattern

Ten columns (`BMI`, `Smoking_Status`, `Alcohol_Consumption`, `Physical_Activity_Level`, `Cholesterol_Level`, `Systolic_BP`, `Diastolic_BP`, `Resting_Heart_Rate`, `HbA1c`, `Medication_Adherence_Percentage`) each have **~5–8% missing values**, represented as truly blank cells (not "NULL", "N/A", or "Unknown"). The two target columns and all binary disease flags / demographics are fully populated, keeping the prediction targets clean while still giving you realistic feature-level missingness to handle.

## Quick Summary Stats

| Metric | Value |
|---|---|
| Rows | 10,000 |
| Columns | 20 |
| Diabetes prevalence | ~8.3% |
| Hypertension prevalence | ~20.3% |
| CKD prevalence | ~5.2% |
| Liver disease prevalence | ~6.1% |
| Family history of CVD | ~24.8% |
| Mean Heart Attack Risk | ~18.3% |
| Mean Mortality Risk | ~12.0% |
| Correlation: Heart Attack Risk ↔ Mortality Risk | ~0.80 |
