# 🌦️ Weather Data Time Series Forecasting

This project performs a complete **time series analysis and forecasting** of hourly temperature data from the RDU weather station. It walks through data cleaning, feature engineering, seasonal decomposition, and predictive modeling using both **Linear Regression** and **Random Forest Regressor**.

---

## 📘 Overview
The goal is to model and forecast hourly temperature (`tmpf`) using decades of historical data from RDU (Raleigh–Durham Airport).  
The workflow includes:
- Parsing and preprocessing raw weather logs  
- Handling missing values and duplicate timestamps  
- Creating an hourly continuous series  
- Exploring seasonality and trends  
- Building autoregressive forecasting models  

---

## ⚙️ Project Pipeline

### 1. Data Preparation
- Load and inspect the dataset (`data/RDU.csv`) using **Pandas** and **NumPy**.  
- Convert timestamps (`valid`) to `datetime`, extract time features (day, month, hour, weekday).  
- Convert temperature and other numeric fields using coercion (`pd.to_numeric(errors='coerce')`).  
- Identify and merge duplicate timestamps by averaging numeric values.  

### 2. Data Cleaning
- One-hot encode categorical features (`skyc`, `wxcodes`) for machine learning compatibility.  
- Resample data to a strict hourly grid.  
- Interpolate missing values for short gaps (≤ 3 hours) using **time-based interpolation** while keeping longer gaps as NaN.  
- Produce a fully continuous hourly temperature dataset covering multiple decades.  

### 3. Exploratory Analysis
- Apply **rolling mean smoothing** to visualize temperature trends and reduce noise.  
- Perform **seasonal decomposition** using `statsmodels` to identify daily, weekly, and annual cycles.  
- Visualize long-term variability and trend consistency.  

### 4. Feature Engineering
- Create autoregressive lag features:  
  - `lag1`: previous hour temperature  
  - `lag24`: same hour previous day  
- Add rolling features like `rolling24` (24-hour moving average).  
- Include cyclical time features (`hour`, `month`) to encode seasonality.  
- Drop rows with missing lag values to maintain data integrity.  

### 5. Predictive Modeling
- **Linear Regression**:  
  - Train on engineered features (`lag1`, `lag24`, `rolling24`, `hour`, `month`).  
  - Achieved **Train R² = 0.981**, **Test MAE = 9.50°F**, **Test MSE = 130.99**.  
- **Random Forest Regressor**:  
  - 200 trees, maximum depth of 20, trained with all CPU cores.  
  - Achieved **Train R² = 0.996**, **Test MAE = 4.40°F**, **Test MSE = 30.59**.  
- Both models used an **autoregressive loop**, updating forecasts sequentially for each hour in the test window (September 17–30, 2025).  

### 6. Evaluation
- Evaluation metrics computed using **scikit-learn**:
  - `mean_absolute_error` (MAE)  
  - `mean_squared_error` (MSE)  
- Random Forest significantly outperformed Linear Regression in predictive accuracy and stability.  

---

## 📊 Key Insights
- Temperature patterns show strong **daily and seasonal periodicity**.  
- Careful handling of missing and duplicate timestamps is critical for accurate modeling.  
- Time-based interpolation and lagged features improve continuity and predictive power.  
- Nonlinear ensemble methods (like Random Forests) capture weather variability better than linear models.  

---

## 🧩 Tools and Libraries
- **Python 3.10+**  
- **Pandas**, **NumPy**, **Matplotlib**, **Statsmodels**, **Scikit-learn**  

---

## 📈 Results Summary
| Model | Train R² | Test MAE (°F) | Test MSE |
|--------|-----------|----------------|-----------|
| Linear Regression | 0.981 | 9.50 | 130.99 |
| Random Forest | 0.996 | 4.40 | 30.59 |

Random Forest provided more accurate and stable forecasts, making it better suited for long-range temperature prediction tasks.

---

## 🧠 Summary
This project demonstrates an end-to-end **time series forecasting pipeline**—from raw data ingestion and cleaning to feature engineering, modeling, and evaluation.  
It highlights best practices for working with noisy meteorological data, handling missingness, and building reliable forecasting systems for real-world use.
