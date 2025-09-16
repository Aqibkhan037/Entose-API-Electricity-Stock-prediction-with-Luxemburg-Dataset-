<img width="1353" height="1530" alt="deepseek_mermaid_20250916_230b6c" src="https://github.com/user-attachments/assets/0d841a05-c466-4dbd-a276-54939368de11" />⚡ Electricity Price Forecasting Model
https://img.shields.io/badge/Python-3.8%252B-blue
https://img.shields.io/badge/XGBoost-1.7%252B-orange
https://img.shields.io/badge/ENTSO--E-API-green
https://img.shields.io/badge/Open--Meteo-API-lightgrey
https://img.shields.io/badge/License-MIT-yellow

A machine learning pipeline that forecasts electricity prices using historical price data from ENTSO-E and weather data from Open-Meteo. This model uses XGBoost to predict day-ahead electricity prices based on market and meteorological factors.
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

📋 Overview
This project implements a complete machine learning workflow for electricity price forecasting:

Data Acquisition: Fetches historical electricity prices from ENTSO-E API

Weather Integration: Retrieves complementary weather data from Open-Meteo

Feature Engineering: Creates temporal features and lag variables

Model Training: Uses XGBoost regression for price prediction

Performance Evaluation: Calculates Mean Absolute Error (MAE) metrics

_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

✨ Features
🔌 Real-time Data Fetching: Direct integration with ENTSO-E transparency platform

🌤️ Weather Integration: Incorporates temperature, cloud cover, radiation, and wind speed

⏰ Temporal Features: Hour-of-day, day-of-week, and month features

📊 Lag Variables: Includes price lag features (1h and 24h) for sequential patterns

🤖 XGBoost Model: High-performance gradient boosting for accurate forecasts

💾 Model Persistence: Save/load trained models for deployment
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

📦 Installation
Prerequisites
Python 3.8+

pip package manager

ENTSO-E API token (Get one here)

Install Dependencies
bash
pip install pandas numpy xgboost scikit-learn joblib requests entsoe-py
🔧 Configuration
Before running the model, ensure you have a valid ENTSO-E API token:

python
# Replace with your actual token
ENTSOE_TOKEN = "your_entsoe_api_token_here"  
COUNTRY_CODE = "FR"  # Country code (FR=France, DE=Germany, etc.)
LAT, LON = 49.8153, 6.1296  # Coordinates for weather data
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

🚀 Usage
Basic Training
bash
python fetch_and_train.py
Expected Output
text
⚡ Fetching electricity prices from ENTSO-E...
🌤️ Fetching weather data from Open-Meteo...
📥 Fetching data...
🧠 Training model...
📉 MAE: 12.3456 €/MWh
✅ Model saved to xgb_model_price.pkl
Integration in Your Code
python
# Load the trained model
model = joblib.load("xgb_model_price.pkl")
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

# Make predictions
predictions = model.predict(features_df)
📊 API Integrations
ENTSO-E API
Endpoint: Day-ahead electricity prices

Data: Historical price data in €/MWh

Frequency: Hourly resolution

Documentation: ENTSO-E Transparency Platform

Open-Meteo API
Endpoint: Historical weather data

Parameters: Temperature, cloud cover, solar radiation, wind speed

Documentation: Open-Meteo API
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

🔍 Model Features
The model uses the following input features:

Feature	Description	Type
temperature_2m	2-meter above ground temperature	Numerical
cloudcover	Cloud cover percentage	Numerical
shortwave_radiation	Solar radiation intensity	Numerical
wind_speed_10m	Wind speed at 10 meters height	Numerical
hour	Hour of day (0-23)	Categorical
dayofweek	Day of week (0-6)	Categorical
month	Month of year (1-12)	Categorical
lag1	Price 1 hour ago	Numerical
lag24	Price 24 hours ago	Numerical
📈 Performance Metrics
Mean Absolute Error (MAE): Typically between 5-15 €/MWh depending on market volatility

Training Period: 10 days of historical data (configurable)

Test Split: 20% of data for validation
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

🔄 Retraining Schedule
For production use, consider retraining the model:

Daily: For most accurate short-term predictions

Weekly: For general forecasting needs

After Market Events: Following significant price volatility
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

🌍 Geographic Coverage
Currently configured for France (COUNTRY_CODE = "FR"), but easily adaptable to other European countries:

Germany: DE

Spain: ES

Italy: IT

Netherlands: NL

Belgium: BE

And many more ENTSO-E member countries

🛠️ Customization
Adjust Training Period
python
# Change the number of training days
start_date = end_date - timedelta(days=30)  # 30 days of data
Add Additional Features
python
# Example: Add holiday information
df["is_holiday"] = df["time"].dt.date.isin(holiday_dates)
Modify Model Parameters
python
# Adjust XGBoost hyperparameters
model = xgb.XGBRegressor(
    n_estimators=200, 
    learning_rate=0.05, 
    max_depth=6,
    subsample=0.8,
    colsample_bytree=0.8
)
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

🤝 Contributing
We welcome contributions! Please feel free to submit pull requests or open issues for bugs and feature requests.

Fork the repository

Create your feature branch (git checkout -b feature/AmazingFeature)

Commit your changes (git commit -m 'Add some AmazingFeature')

Push to the branch (git push origin feature/AmazingFeature)

Open a Pull Request

📝 Learning Outcomes
This project demonstrates several important data science concepts:

API Integration: Working with REST APIs for data acquisition

Time Series Processing: Handling temporal data and feature engineering

Feature Engineering: Creating meaningful predictors from raw data

Machine Learning: Implementing and evaluating XGBoost models

Model Persistence: Saving and loading trained models

Error Handling: Robust API communication and data validation
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

⚠️ Limitations
Requires valid ENTSO-E API token

Limited to European electricity markets

Weather data accuracy depends on location coordinates

Model performance varies with market volatility
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🙏 Acknowledgments
ENTSO-E for providing electricity market data

Open-Meteo for free weather API access

XGBoost team for the powerful machine learning library

entsoe-py Python client for ENTSO-E API
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

📞 Support
For questions or support:

Check the issues page

Create a new issue with detailed information

Email: aqibkhan1528000@gmail.com
