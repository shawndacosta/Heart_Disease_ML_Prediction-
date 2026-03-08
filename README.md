# ❤️ Heart Disease Prediction – Machine Learning Classification Project

# Project Overview

This project focuses on predicting the presence of **heart disease** using structured **clinical data**.

Multiple **classification models** were implemented and compared through a rigorous evaluation pipeline including **cross-validation** and **hyperparameter tuning**.

The objective was to identify the most reliable model based on **generalization performance** and apply it to unseen **test data** for final prediction.

The final selected model achieved strong and consistent performance across multiple **evaluation metrics**.

# 📑 Table of Contents

1. [I. Introduction 🩺](#i-introduction-)
2. [II. Dataset & Exploratory Data Analysis 🔍](#ii-dataset--exploratory-data-analysis-)
3. [III. Data Preprocessing 🛠️](#iii-data-preprocessing-%EF%B8%8F)
4. [IV. Model Selection & Hyperparameter Optimization 📈](#iv-model-selection--hyperparameter-optimization-)
5. [V. Models Evaluation 📊](#v-models-evaluation-)
6. [VI. Final Model Application on Test Data 📥](#vi-final-model-application-on-test-data-)
7. [VII. Conclusion ✔️](#vii-conclusion-%EF%B8%8F)


# I. Introduction 🩺

Cardiovascular diseases are among the leading causes of mortality worldwide. Early detection based on measurable clinical indicators can significantly improve patient outcomes.

The goal of this project is to build a **supervised machine learning model** capable of predicting **heart disease presence** using demographic and medical features such as **age**, **blood pressure**, **cholesterol level**, **ECG results**, and **exercise-induced symptoms**.

To ensure a robust and reproducible methodology, the project follows a structured workflow:

- Data validation and exploration  
- Feature preparation  
- Train-validation split  
- Model comparison using cross-validation  
- Hyperparameter tuning  
- Performance analysis using multiple evaluation metrics  

# II. Dataset & Exploratory Data Analysis 🔍 

The dataset is divided into two files:

- `train.csv` 
- `test.csv`  

Both datasets were loaded using Pandas and inspected for structural consistency.

The training dataset contains **630,000 rows** and **15 columns**, including the target variable `Heart Disease`.  
The test dataset contains the same feature structure without the target column.

## Data Structure Validation

Using `.info()` and `.isnull().sum()`, the dataset was examined for consistency:

- No missing values were detected  
- All numerical features were correctly assigned as integer or float types  
- The target variable was initially stored as categorical values (`Presence`, `Absence`)

## Feature Description

The dataset includes several variables:

- `Age` — Patient age  
- `Sex` — Gender indicator  
- `Chest pain type` — Category of chest pain  
- `BP` — Resting blood pressure  
- `Cholesterol` — Cholesterol level  
- `FBS over 120` — Fasting blood sugar indicator  
- `EKG results` — Electrocardiographic results  
- `Max HR` — Maximum heart rate achieved  
- `Exercise angina` — Exercise-induced angina  
- `ST depression` — ST segment depression value  
- `Slope of ST` — Slope of the peak exercise ST segment  
- `Number of vessels fluro` — Number of major vessels colored by fluoroscopy  
- `Thallium` — Thallium stress test result

All these variables represent clinical measurements available prior to diagnosis.  
This ensures that no feature introduces **data leakage**, as the model only relies on information that would realistically be available before confirming heart disease.

## Target Distribution

The `Heart Disease` variable distribution is as follows:

- Absence: 347,546  
- Presence: 282,454  

The dataset is relatively balanced, meaning that class imbalance is not a major concern.  
Therefore, ***accuracy*** was considered a reliable primary evaluation metric, alongside ***precision***, ***recall***, ***F1-score***, and the ***confusion matrix***.

# III. Data Preprocessing 🛠️

## Imputation 

Since the dataset contains no missing values, no imputation was required.  

## Encoding

The only categorical variable in the dataset was the target column `Heart Disease`. 

A simple mapping was applied:

- `Absence` → 0  
- `Presence` → 1  

This binary encoding was sufficient because the task is a **binary classification** problem. 

No One-Hot Encoding or Ordinal Encoding was required, as all feature columns were already numerical.

## Data Leakage Consideration

Since only the target variable was encoded, no data leakage was introduced.

All predictive features remain independent from the label encoding process.

## Feature and Target Separation

The dataset was then divided into:

- **X** — all feature columns  
- **y** — the encoded `Heart Disease` target  

A train-validation split was applied to ensure proper evaluation of model generalization performance before testing on unseen data.

# IV. Model Selection & Hyperparameter Optimization 📈

To determine the most suitable algorithm for heart disease prediction, multiple classification models were evaluated. Each model was associated with a predefined hyperparameter grid in order to test different configurations systematically.

Hyperparameter tuning was performed using **GridSearchCV**, combined with a **5-fold cross-validation** strategy. This approach evaluates performance across multiple training splits, improving model stability.

For each model, the best hyperparameter configuration was selected and evaluated using cross-validation metrics.

# V. Models Evaluation 📊

## Accuracy Comparison

The first comparison was conducted using ***accuracy***, as the dataset is balanced.

|       | Model        | Accuracy |
|-------|--------------|----------|
| 2     | XGBoost      | 0.887333 |
| 1     | RandomForest | 0.884405 |
| 0     | DecisionTree | 0.880913 |

All models achieve very similar ***accuracy*** scores.  
Since the differences are small, additional metrics were used for a more detailed comparison.

## Detailed Performance Comparison

| Model         | Accuracy | Confusion Matrix                     | Precision | Recall   | F1 score |
|---------------|----------|--------------------------------------|-----------|----------|----------|
| XGBoost       | 0.887333 | [[62903, 6661], [7535, 48901]]       | 0.880116  | 0.866486 | 0.873248 |
| RandomForest  | 0.884405 | [[62855, 6709], [7856, 48580]]       | 0.878656  | 0.860798 | 0.869635 |
| DecisionTree  | 0.880913 | [[62667, 6897], [8108, 48328]]       | 0.875111  | 0.856333 | 0.865620 |

By observing the additional metrics, we can see that **XGBoost produces fewer overall classification errors**.

Based on this comprehensive evaluation, **XGBoost** was selected as the final model**.


## Optimal Hyperparameters

The selected model achieved its performance based on the following hyperparameters:

| Parameter     | Value |
|--------------|--------|
| max_depth     | 3      |
| n_estimators  | 200    |
| learning_rate | 0.2    |

# VI. Final Model Application on Test Data 📥

## Generating Predictions

Once **XGBoost** was selected as the final model, it was retrained on the full training dataset using the optimal hyperparameters.

Predictions were generated on the test set and exported as a CSV file.

Here are the first 10 lines of the file:

| Disease Prediction |
|--------|
| 1 |
| 0 |
| 1 |
|0  |
| 0 |
| 1 |
| 0 |
| 1 |
| 1 |

# VII. Conclusion ✔️

This project demonstrates a complete **machine learning workflow**, from data exploration to model selection and final prediction.

After comparing multiple algorithms, **XGBoost** achieved the strongest overall performance across all evaluation metrics. 

The final model demonstrates strong predictive performance with balanced classification behavior.

## Possible Improvements

Although the results are robust, several enhancements could be explored:

- More advanced hyperparameter tuning (e.g., RandomizedSearch or Bayesian optimization)
- Feature engineering to capture more complex patterns
- Ensemble blending between top-performing models
- Threshold optimization depending on the application objective

Overall, the modeling pipeline is structured, reproducible, and suitable for further optimization.
