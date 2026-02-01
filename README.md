# End-to-End Data Science Pipeline: Analyzing Delhi's Air Quality Index (AQI)

---

### Data Source

**Original Dataset:** [Delhi Pollution AQI Dataset](https://www.kaggle.com/datasets/vishardmehta/delhi-pollution-aqi-dataset) by [Vishard Mehta](https://www.kaggle.com/vishardmehta) on Kaggle

[![Kaggle Dataset](https://img.shields.io/badge/Kaggle-Dataset-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/vishardmehta/delhi-pollution-aqi-dataset)

- **Period**: 2020-2024
- **Frequency**: Hourly measurements
- **Records**: 35,000+ observations
- **License**: [Check Kaggle Dataset License](https://www.kaggle.com/datasets/vishardmehta/delhi-pollution-aqi-dataset)

---

## Project Overview
Delhi is known for having one of the most complex air pollution profiles in the world, often driven by seasonal factors, traffic, and industrial activities. This project focuses on analyzing historical Air Quality Index (AQI) data retrieved from a database. The goal is to process raw data into actionable insights and potentially build a predictive model for future air quality trends.

Below is the comprehensive Data Science workflow applied in this project, covering everything from data extraction to model evaluation.

---

## 1. Business Understanding & Domain Knowledge
Before diving into the code, it is crucial to understand the context of Delhi's pollution:
*   **Objective:** To analyze historical trends, identify critical pollution periods, and forecast AQI levels.
*   **Key Factors:** Delhi's AQI is heavily influenced by seasonal changes (especially winter), stubble burning in neighboring states, and festivals like Diwali.
*   **Metrics:** We focus on pollutants such as PM2.5, PM10, NO2, CO, SO2, and O3.

## 2. Data Collection & Extraction
The data resides in a relational database.
*   **Action:** Establish a connection using SQL connectors (e.g., `SQLAlchemy` or `psycopg2`).
*   **Querying:** Fetch relevant features and ensure the data granularity (hourly/daily) matches the analytical goals.

## 3. Data Cleaning & Preprocessing
Real-world sensor data is rarely clean. This phase handles the "noise":
*   **Missing Values:** Sensors often fail or undergo maintenance. We handle nulls using interpolation (linear/time-based) rather than simple dropping to maintain time-series continuity.
*   **Outlier Detection:** Distinguishing between sensor errors (e.g., negative values) and extreme pollution events (e.g., AQI > 500 during smog episodes).
*   **Type Conversion:** Converting timestamp strings into proper Python `datetime` objects for time-based indexing.

## 4. Exploratory Data Analysis (EDA)
Uncovering patterns and trends through visualization:
*   **Time Series Analysis:** Visualizing long-term trends to identify the annual "smog season" (typically October to January).
*   **Correlation Analysis:** Using Heatmaps to see how different pollutants correlate (e.g., PM2.5 vs. PM10).
*   **Distribution Check:** Understanding the spread of AQI values (Skewness/Kurtosis).

## 5. Feature Engineering
Transforming raw data into meaningful features for modeling:
*   **Temporal Features:** Extracting Hour, Day, Month, and Weekend indicators to capture rush-hour and seasonal effects.
*   **Lag Features:** Creating "Lag 1" or "Lag 24" features (past values) since current air quality is highly dependent on the state of the air in previous hours.
*   **Rolling Statistics:** Calculating rolling means (moving averages) to smooth out short-term fluctuations.

## 6. Modeling (Forecasting)
*   **Model Selection:** Applying time-series compatible models such as ARIMA, SARIMA, or Machine Learning regressors like XGBoost/Random Forest.
*   **Training:** Splitting data into Training and Testing sets chronologically (to avoid data leakage in time series).

## 7. Evaluation
Measuring the success of the analysis/model:
*   **Metrics:** Using RMSE (Root Mean Squared Error) or MAE (Mean Absolute Error) to quantify the deviation between predicted and actual AQI values.
