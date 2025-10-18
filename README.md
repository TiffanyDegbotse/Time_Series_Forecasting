# Hourly Temperature Forecasting at RDU Airport

This project develops and evaluates machine learning models to forecast hourly temperature at Raleigh-Durham (RDU) Airport for the period September 17–30, 2025. The notebook provides a full pipeline covering data preprocessing, feature engineering, model training, and evaluation.

The target variable is temperature (`tmpf`) derived from timestamped weather data in `data/RDU.csv`. Forecasting is performed over the two-week window using two models: **Linear Regression** and **Random Forest Regressor**. Model performance is assessed with RMSE (Root Mean Squared Error), MAE (Mean Absolute Error), and MSE (Mean Squared Error).

## Repository Contents
- `project.ipynb` — main notebook for preprocessing, modeling, and evaluation  
- `data/RDU.csv` — input dataset of weather observations at RDU Airport  
- `requirements.txt` — list of dependencies  

## Setup
Clone the repository:  
```bash
git clone https://github.com/TiffanyDegbotse/Time_Series_Forecasting.git
cd Time_Series_Forecasting
```

Create a virtual environment and install requirements:  
```bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Run the notebook:  
```bash
jupyter notebook project.ipynb
```

## Methodology
- **Preprocessing**: converted timestamps to datetime, aggregated minute-level readings into hourly means, and handled missing values  
- **Feature Engineering**: included hour of day, day of week, lag features (1, 24, 48, 72 hours), and rolling statistics (24-hour moving mean and standard deviation)  
- **Modeling**: trained both Linear Regression (baseline) and Random Forest (nonlinear, tuned hyperparameters)  
- **Evaluation**: compared metrics (MAE, RMSE, MSE) and plotted predicted vs. actual temperatures  

## Results
- Linear Regression: MAE = 5.818, RMSE = 7.349, MSE = 54.009  
- Random Forest: MAE = 5.665, RMSE = 7.060, MSE = 49.845  

Random Forest outperformed Linear Regression across all metrics, providing more accurate forecasts and better capturing temperature variability. Visualizations confirm stronger alignment of Random Forest predictions with actual temperature values.

## Future Work
- Incorporate exogenous variables (humidity, windspeed, pressure) for richer features  
- Explore deep learning methods (LSTMs, Transformers) for sequence modeling  
- Deploy as an API or lightweight web app for real-time predictions  

## Requirements
- Python 3.9+  
- pandas, numpy, matplotlib  
- scikit-learn  
- jupyter  

Install all dependencies via:  
```bash
pip install -r requirements.txt
```
