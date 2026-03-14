# Heart Disease Prediction Using Machine Learning

Classification models to predict heart disease presence using clinical patient data.

## Overview

This project compares multiple machine learning algorithms to predict the presence of heart disease in patients based on 11 clinical features. The goal is to identify which classification approach provides the most accurate and robust predictions for early disease detection.

## Problem Statement

Heart disease is the leading cause of death in Australia, with 18,590 deaths in 2017. Early detection significantly improves patient outcomes. This project evaluates whether common clinical measurements can accurately predict heart disease presence using machine learning techniques.

## Dataset

- **Source:** IEEE Dataport (curated from 5 public datasets)
- **Size:** 1,190 patient observations
- **Features:** 11 clinical variables (mix of categorical and numeric)
  - Age, sex, chest pain type
  - Resting blood pressure, cholesterol, fasting blood sugar
  - Resting ECG, maximum heart rate, exercise-induced angina
  - Oldpeak (ST depression), ST slope
- **Target:** Binary classification (0 = no heart disease, 1 = heart disease present)

## Methodology

### Models Evaluated

1. **Naive Bayes Classifier** (baseline model)
2. **Logistic Regression (GLM)**
3. **K-Nearest Neighbors (KNN)**

Each model was tested using:
- All features
- Significant features only (p < 0.05)
- Principal Component Analysis (2 components)

### Approach

- 80/20 train-test split
- Feature selection based on statistical significance
- Dimensionality reduction via PCA (Kaiser Rule & Horn's Parallel Analysis)
- K-means clustering analysis for pattern discovery

## Key Results

### Model Performance (Test Data Accuracy)

| Model | Features | Accuracy | Kappa |
|-------|----------|----------|-------|
| **Logistic Regression** | All features | **84.4%** | 0.686 |
| **Logistic Regression** | Significant features | **83.5%** | 0.669 |
| Naive Bayes | All features | 77.6% | 0.551 |
| KNN | Significant features | 73.0% | 0.456 |
| Logistic Regression | PCA (2 components) | 70.5% | 0.405 |
| KNN | PCA (2 components) | 72.2% | 0.439 |

### Most Significant Predictors
- Sex
- Chest pain type (especially asymptomatic)
- Cholesterol levels
- Fasting blood sugar
- Exercise-induced angina
- Oldpeak (ST depression)

### Key Findings

- **Best model:** Logistic regression with all features achieved 84.4% accuracy
- All models exceeded the industry standard threshold (70% accuracy)
- Feature selection maintained high accuracy while reducing dimensionality
- K-means clustering did not effectively separate heart disease status (36.5% variance explained)

## Technologies Used

- **Language:** R (4.x)
- **Key Packages:** 
  - `caret` - model training and evaluation
  - `e1071` - Naive Bayes implementation
  - `tidyverse` - data manipulation
  - `FactoMineR`, `factoextra` - PCA and visualization
  - `cluster` - clustering analysis

## Files

- `heart_disease_analysis.Rmd` - Full R Markdown analysis with code and explanations
- `heart_disease_report.pdf` - Comprehensive report with methodology, results, and discussion

## Running the Analysis
```R
# Install required packages
install.packages(c("tidyverse", "caret", "e1071", "FactoMineR", 
                   "factoextra", "cluster", "psych", "ggcorrplot"))

# Open and knit the RMarkdown file
rmarkdown::render("heart_disease_analysis.Rmd")
```

## Model Interpretation

The logistic regression models demonstrated the best performance, with statistical significance (p < 0.05) for:
- **Sex** (males higher risk)
- **Asymptomatic chest pain** (strongest predictor)
- **Lower cholesterol** (associated with disease presence in this dataset)
- **Elevated fasting blood sugar**
- **Exercise-induced angina**
- **Oldpeak elevation**

## Limitations & Future Work

### Current Limitations
- Small dataset (1,190 observations)
- Model performance varies with different train-test splits
- K-means clustering did not reveal meaningful subtypes

### Suggested Improvements
- Validate on external datasets
- Test ensemble methods (Random Forest, XGBoost)
- Explore deep learning approaches
- Investigate feature interactions
- Conduct more extensive hyperparameter tuning

## Clinical Relevance

With 84% accuracy, the logistic regression model shows promise for:
- Clinical decision support tools
- Early screening programs
- Risk stratification in preventive cardiology
- Identifying high-risk patients for further testing

## Note

This project was completed as part of my Master of Data Science program (2023).  
README documentation was drafted with AI assistance.
