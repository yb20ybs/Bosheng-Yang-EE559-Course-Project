# EE559 Heart Disease Risk Prediction

This project is the final course project for EE559. The goal of this project is to predict heart disease risk using supervised machine learning methods on the UCI Heart Disease dataset.

The project includes data preprocessing, exploratory data analysis, LASSO-based feature selection, model training, model evaluation, and SHAP-based interpretability analysis.

## Project Overview

Cardiovascular disease is one of the major public health problems worldwide. Early risk prediction can help support clinical decision-making and improve patient outcomes. In this project, we build a machine learning framework to predict whether a patient has heart disease based on clinical features.

This is formulated as a binary classification problem:

- `0`: No heart disease
- `1`: Presence of heart disease

## Dataset

The dataset used in this project is the UCI Heart Disease dataset. After preprocessing, the dataset contains 297 patient records and 13 clinical features.

The features include demographic information, physiological measurements, and exercise-related clinical indicators, such as:

- age
- sex
- resting blood pressure
- serum cholesterol
- maximum heart rate
- exercise-induced angina
- ST depression
- number of major vessels
- thalassemia type

The class distribution is relatively balanced:

- Negative class: 160 samples, 53.9%
- Positive class: 137 samples, 46.1%

Because the two classes are relatively balanced, no additional over-sampling or under-sampling method is applied.

## Methods

This project follows a complete supervised machine learning pipeline:

1. Data preprocessing
2. Exploratory data analysis
3. LASSO feature selection
4. Model training
5. Hyperparameter tuning
6. Model evaluation
7. SHAP-based interpretability analysis

## Data Preprocessing

The preprocessing steps include:

- Converting missing values represented by `?` into missing values
- Removing samples with missing values
- Converting all variables into numerical format
- Transforming the original target variable into a binary classification label
- Applying feature scaling when required by the model

## Exploratory Data Analysis

Exploratory data analysis is performed to understand the relationship between clinical features and the target variable.

The analysis shows that several variables are significantly different between the negative and positive classes, including:

- age
- maximum heart rate (`thalach`)
- ST depression (`oldpeak`)
- chest pain type (`cp`)
- exercise-induced angina (`exang`)
- number of major vessels (`ca`)
- thalassemia type (`thal`)

These observations provide useful evidence for feature selection and model development.

## Feature Selection

LASSO regression is applied for feature selection. By using L1 regularization, less important feature coefficients are shrunk toward zero. This helps reduce model complexity, improve generalization ability, and increase interpretability.

Using the 1-SE criterion, the final selected key features are:

- `thal`
- `ca`
- `exang`
- `oldpeak`
- `thalach`

These features are used as important predictors in the following modeling and interpretation steps.

## Models

Three supervised learning models are implemented and compared:

### Logistic Regression

Logistic Regression is used as the baseline model. It is simple, interpretable, and suitable for binary classification tasks.

### Random Forest

Random Forest is an ensemble learning method based on multiple decision trees. It can capture nonlinear relationships and feature interactions while reducing overfitting through bagging.

### XGBoost

XGBoost is a gradient boosting method that usually performs well on structured tabular data. It is used to capture complex feature interactions and improve predictive performance.

## Hyperparameter Tuning

Bayesian optimization is used to tune model hyperparameters. Cross-validation is applied during the tuning process to improve model stability and reduce the risk of overfitting.

## Evaluation Metrics

The models are evaluated using the following metrics:

- Accuracy
- Precision
- Recall
- F1-score
- AUC
- Confusion Matrix
- ROC Curve

These metrics provide a comprehensive evaluation of both overall classification performance and class-specific prediction behavior.

## Results

The experimental results show that all three models achieve reasonable classification performance.

The AUC results are summarized as follows:

| Model | Train AUC | Test AUC |
|---|---:|---:|
| Logistic Regression | 0.898 | 0.904 |
| Random Forest | 0.924 | 0.900 |
| XGBoost | 0.919 | 0.899 |

Random Forest achieves the best overall balance between predictive performance, stability, and generalization ability. Although Logistic Regression has a slightly higher test AUC, Random Forest shows more balanced behavior across different evaluation metrics and confusion matrix results.

XGBoost also performs well, but it shows slight signs of overfitting on this relatively small dataset.

## Interpretability Analysis

SHAP is used to interpret the Random Forest model. SHAP values quantify the contribution of each feature to the model prediction.

The SHAP analysis shows that the most important features are:

- `thal`
- `ca`
- `thalach`
- `oldpeak`
- `exang`

The interpretation results suggest that higher values of `thal` and `ca` tend to increase the predicted risk of heart disease, while higher `thalach` is generally associated with lower predicted risk. The SHAP dependence analysis also shows nonlinear relationships between several clinical features and the model output.
