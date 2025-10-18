# Hourly Temperature Forecasting at RDU Airport

This project builds and evaluates machine learning models to predict hourly temperature at Raleigh-Durham (RDU) airport for the period September 17, 2025 – September 30, 2025. The notebook demonstrates a complete workflow from data preprocessing to feature engineering, model training, and evaluation.

The goal of this project is to forecast hourly temperature (`tmpf`) at RDU Airport using historical weather data. The dataset `data/RDU.csv` contains timestamped weather observations. Forecasting is performed for the window 2025-09-17 00:00 to 2025-09-30 23:00. Two models are implemented: Linear Regression and Random Forest Regressor. The models are evaluated using RMSE (Root Mean Squared Error), MAE (Mean Absolute Error), and MSE (Mean Squared Error).

The repository contains `project.ipynb` which holds the notebook with preprocessing, feature engineering, modeling, and evaluation; `data/RDU.csv` which is the input dataset of hourly weather at RDU Airport; and `requirements.txt` listing dependencies.

To set up, clone the repository with  
git clone https://github.com/TiffanyDegbotse/Time_Series_Forecasting.git
cd Time_Series_Forecasting

Then create a virtual environment and install dependencies with  
python -m venv venv  
source venv/bin/activate   (or venv\Scripts\activate on Windows)  
pip install -r requirements.txt  

Run the notebook with  
jupyter notebook project.ipynb  

Data preprocessing included converting timestamps to datetime format, reindexing minute-level readings into hourly means, and filling missing values for continuity in the time series. Feature engineering added time-based features such as hour of day and day of week, lag features for temperature (1, 24, 48, and 72 hours ago), and rolling statistics like the 24-hour moving mean and standard deviation. Modeling involved two approaches: a Linear Regression baseline and a Random Forest Regressor with tuned hyperparameters. Evaluation compared both models on RMSE, MAE, and MSE, along with visualizations of predicted versus actual hourly temperatures.

Linear Regression achieved MAE = 5.818, RMSE = 7.349, and MSE = 54.009. Random Forest achieved MAE = 5.665, RMSE = 7.060, and MSE = 49.845. Random Forest outperformed Linear Regression across all metrics, showing better ability to capture variability in temperature patterns. Forecast plots demonstrate that the Random Forest predictions align more closely with observed values over the forecast horizon.

Future extensions include incorporating additional exogenous variables such as humidity, windspeed, and pressure to enrich the feature set, experimenting with deep learning models like LSTMs or Transformers for sequence forecasting, and deploying the solution as a lightweight web app or API for real-time temperature predictions.

Requirements include Python 3.9+, pandas, numpy, matplotlib, scikit-learn, and jupyter. These can be installed via pip install -r requirements.txt.

Dataset source: RDU airport weather data (course dataset). Developed as part of coursework on time series forecasting.
