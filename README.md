## CIND820 - Big Data Analytics Capstone Project

# Modeling the Impact of Economic, Lifestyle, and Demographic Factors on Health Outcomes Using Regression and Time Series Techniques

## Project Overview
This is the repository for my Capstone project for the final course towrad the Certificate in Data Analytics, Big Data, and Predictive Analytics from Toronto Metropolitan University, exploring the relationship between socioeconomic factors and the prevalence of non-communicable diseases (NCDs), such as diabetes, cardiovascular diseases, and life expectancy trends.
The objective of the project is to identify significant predictors of health outcomes using robust time-series analysis, feature engineering, and machine learning models, with appropriate preprocessing, validation, and diagnostics.

## Objectives
1. Identify the key socioeconomic, demographic, and behavioral predictors of non-communicable diseases (NCDs).
2. Evaluate and compare ARIMA, Prophet, and Random Forest for health forecasting.
3. Provide long-term projections (2024–2074) to support evidence-based policymaking in public health.

## Health Indicators:
* Life Expectancy
* Diabetes Prevalence
* Cardiovascular Disease Rates

## Predictors:
* Economics Predictors: GDP, CPI, inflation, income, Unemployment, Gini Coefficient
* Demographic Predictors: Median age, Sex ratio, Education 
* LIfestyle Predictors: Cost healthy diet, BMI 

## Abstract
This project analyzes the impact of economic, lifestyle, and demographic factors on global public health outcomes, focusing specifically on the prevalence of non-communicable disease (NCDs) such as heart disease and diabetes, as well as life expectancy. Using a consolidated dataset of 21,514 global observations across 18 variables from 16 sources compiled by Our World in Data, covering the period 1950 to 2023, this study applies multiple linear regression and time series forecasting techniques to explore historical patterns and predict future health trends.
The three research questions are designed to help explain how various determinants affect health outcomes: (1) What are the key socioeconomic, demographic, and lifestyle factors most strongly associated with the prevalence of non-communicable diseases (heart disease and diabetes) across countries from 1950 to 2023? (e.g., diabetes and heart disease); (2) To what extent do modifiable lifestyle and economic factors (e.g., BMI, cost of healthy diet, income, and CPI) explain variations in life expectancy and population health outcomes across countries?; and (3) How will health outcomes (life expectancy, disease rates) evolve over the next 50 years (2023–2073), based on historical trends and key predictors identified in the period from 1950 to 2023?
While most prior studies are limited to specific regions or shorter timeframes, this project provides a globally scoped, long-term perspective on the determinants of health. Analytical tools in Python, such as pandas, scikit-learn, and time series models, are used to conduct regression analysis and forecast future health outcomes.
By identifying influential predictors and modeling long-term trends, this research provides evidence-based insights that can support global health policy, inform preventive strategies, and improve population health outcomes over time.

## Problem Statement
This project investigates the extent to which socioeconomic, demographic, and lifestyle factors are associated with the global prevalence of non-communicable diseases (specifically heart disease and diabetes) and variations in life expectancy. Using a large-scale dataset from Our World In Data which covers the period from 1950 to 2023, this study applies multiple linear regression and time series forecasting techniques to identify the most influential predictors and project future health outcomes up to the year 2073. The goal is to provide a robust, data-driven foundation for understanding the drivers of population health and for anticipating long-term trends.

## Research Questions
1.	What are the key socioeconomic, demographic, and lifestyle predictors most strongly associated with the prevalence of non-communicable diseases (heart disease and diabetes) across countries from 1950 to 2023?
2. To what extent do modifiable lifestyle and economic factors (e.g., BMI, cost of healthy diet, income, and CPI) explain variations in life expectancy and population health outcomes across countries?
3.	How will long-term health outcomes evolve over the next 50 years (2024–2074), based on historical trends and key predictors identified between 1950 and 2023, and which forecasting approaches (ARIMA, Prophet, Random Forest) provide the most accurate projections by country and health indicator?

## Dataset
This project analyzes a consolidated dataset sourced from 16 datasets from Our World In Data, covering the period 1950 – 2023 for over 300 countries. The dataset contains data related to demographic, economic, and lifestyle indicators, and health outcome variables, including GDP, income levels, inflation, CPI, unemployment rate, cost of a healthy diet, BMI, sex ratio, medium age, disease prevalence, life expectancy, and mortality. 
The link available at
[Download the dataset (CSV)](https://github.com/jenniferyik/CIND820_Capstone-Project/blob/main/Health%20Dataset.csv)

## Methodology - Techniques and Tools
* Modeling Techniques: Multiple Linear Regression, ARIMA, Prophet, Random Forest
* Tools: Python (Pandas, NumPy, scikit-learn, Matplotlib/Seaborn, prophet)

## Literature Review

## Project Stages
### Data Collection & Integration

Merged 16 CSV datasets from Our World in Data

Standardized column names and formats (e.g., renamed “Entity” to “Country”)

Joined on Country and Year with outer joins to maximize coverage

### Data Cleaning & Preprocessing

Addressed missing values using tailored imputation (mean, median, mode)

Detected and treated outliers using Winsorization (5th–95th percentile)

Performed variable transformation using Yeo-Johnson to correct skewness and support non-positive values

### Exploratory Data Analysis (EDA)

Assessed variable distributions (histograms, Q-Q plots)

Performed normality checks (Shapiro-Wilk, ADF tests)

Generated correlation matrices and Spearman heatmaps
<img width="1117" height="1003" alt="image" src="https://github.com/user-attachments/assets/5c642f09-bcfc-4fc9-9ad1-0e147b77e1da" />


Investigated multicollinearity using correlation and VIF scores

### Feature Engineering

Created lag features to capture temporal dependencies (e.g., Income_lag1 to lag3)

Standardized all continuous features using StandardScaler

Conducted ACF & PACF analysis to assess autocorrelation structure
<img width="989" height="765" alt="image" src="https://github.com/user-attachments/assets/3d1d408c-8e56-401d-aa45-29ce80c6f5af" />
<img width="989" height="765" alt="image" src="https://github.com/user-attachments/assets/196ece19-df8f-4783-bb27-f92fbf7871c8" />

### Feature Selection

Compared methods: LASSO, RFE, Random Forest, and Forward Selection
<img width="855" height="547" alt="image" src="https://github.com/user-attachments/assets/8acfe6eb-39b8-455c-94d3-c720c8aa3836" />
<img width="863" height="547" alt="image" src="https://github.com/user-attachments/assets/78838b1a-7a07-40ab-baaa-2c10b53aa713" />
<img width="846" height="547" alt="image" src="https://github.com/user-attachments/assets/311cd7ad-2768-40e2-862c-f399f8e61b5a" />


Selected best-performing method per target variable using TimeSeriesSplit + RMSE

Ranked feature importance to identify key predictors

### Model Building

Built models for each of the 3 health outcomes:

 * Life Expectancy

 * Diabetes Prevalence

 * Cardiovascular Diseases

Applied multiple models: Random Forest, ARIMA, Prophet, and Linear Regression

Incorporated HAC standard errors for robust inference in linear models

### Validation Strategy

Used walk-forward (rolling forecast) validation across 10 countries with varying income levels

Ensured no lookahead bias and improved generalizability over time and region

### Model Evaluation & Residual Diagnostics

Used evaluation metrics: RMSE, MAPE, and R²

Conducted residual diagnostics:

ADF Test – stationarity

Breusch–Pagan Test – heteroscedasticity

Ljung–Box Test – autocorrelation

### Forecasting & Interpretation

Generated forecasts and compared predicted vs. actual values

Forecast Comparison of ARIMA, Prophet, and Random Forest Across Three Targets – Life Expectancy, Diabetes and Cardiovascular Disease between 1950–2074
<img width="1389" height="590" alt="image" src="https://github.com/user-attachments/assets/21171501-4615-45a2-8941-bf9c68caa297" />
<img width="1389" height="590" alt="image" src="https://github.com/user-attachments/assets/76d7966f-28b9-4e17-a953-1402be8fee20" />
<img width="1389" height="590" alt="image" src="https://github.com/user-attachments/assets/9634ce8d-9257-4e0b-a2ac-87341510e60d" />


Interpreted model results to extract key health and policy insights




## Contents
 Jupyter Notebooks: Documentation of data preparation, modeling, and evaluation

 Technical Reports: HTML formats summarizing methods, results, and diagnostics

 Dataset: Merged CSV file or download link 

 Figures: Correlation heatmaps, Residual plots, ACF & PACF Plot, Forecast charts.

 Python Scripts: Functions for cleaning, transformation, and preprocessing

 Comments & Documentation: All code includes explanatory comments and markdown cells





