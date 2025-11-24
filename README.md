📦 Demand Forecasting Using Machine Learning
This project builds a full end-to-end Machine Learning pipeline for daily demand forecasting using historical sales data enhanced with pricing, promotions, competitor metrics, economic indicators, and weather effects. The goal is to generate accurate 30-day and 365-day forecasts to support inventory management, production planning, and supply chain optimization. All modeling, feature engineering, forecasting logic, and visualizations are implemented in Python using Jupyter Notebook.



📘 Project Highlights
Full time-series preprocessing and feature engineering
Lag and rolling-window features
Date-based decomposition
RandomForest & XGBoost regression models
Multi-step autoregressive forecasting function
Visualizations for accuracy, forecasts, and trends
Export of all plots and forecast outputs
This repository includes the complete reproducible workflow.



📁 Repository Structure
.
├── Demand Forecast.ipynb             
├── requirements.txt                  
├── README.md                         
├── plots/                        
   ├── actual_vs_rf_predicted.png
   ├── actual_vs_xgb_predicted.png
   ├── feature_importances_rf.png
   ├── forecast_30_day_comparison.png
   ├── historical_plus_30day_forecast.png




🧹 Data Preparation & Feature Engineering
1. Date Parsing
Converted date column to a datetime index
Sorted chronologically and dropped invalid rows

2. Time-based features
Extracted:
year
month
day
day_of_week
week_of_year

3. Lag Features
Lag windows applied to sales_units:
Lag 1
Lag 7
Lag 30

4. Rolling Window Features
Computed rolling averages:
Rolling 7-day mean
Rolling 30-day mean

5. Dropping Early NA Rows
Removed initial rows created by rolling windows.


🤖 Models Used
Random Forest Regressor 
300 trees
Parallel training (n_jobs=-1)
Low variance, robust baseline model
XGBoost Regressor
500 trees
Learning rate 0.05
Depth 6
Handles complex nonlinear patterns
Slightly smoother predictions (as expected)



📊 Results
Model Evaluation (Test Set)
Model	         MAE	RMSE
Random Forest	49.23	56.62
XGBoost	        50.34	58.85

Random Forest slightly outperformed XGBoost
Both models performed similarly and captured underlying demand patterns



Actual vs XGBoost Predicted
The XGBoost model:
Follows long-term structure
Smooths over high-frequency noise
Cannot replicate extreme fluctuations 
This reflects realistic business situations:
short-term noise is difficult to predict, but underlying demand trend is captured.



30-Day Forecast vs Recent Historical
The forecast for the next month is:
Much smoother than historical data
Stabilized around 90–110 units per day
XGBoost predicts slightly lower than RandomForest
This indicates stable upcoming demand without large shocks.



Historical + Forecast (Zoomed View)
This combined plot shows:
Extremely volatile historical daily demand
Smooth transition into predicted demand
Both models agree on the general direction
This is useful for inventory planning and capacity decisions.



🔮 Multi-Step Forecasting
Implemented a custom function:
forecast_future(model, df_history, days, feature_cols)
This function:
Predicts one day at a time
Rolls the forecast back into the dataset (autoregressive)
Recomputes lag & rolling window features
Supports any number of forecast days (e.g., 30, 365)

Generated outputs:
forecast_30_rf.csv
forecast_30_xgb.csv
forecast_365_rf.csv
forecast_365_xgb.csv



🖼️ Visualizations
Key plots saved in /plots/:
Actual vs RF Predicted
Actual vs XGB Predicted
Feature Importances (RF)
30-Day Forecast Comparison
Historical + Forecast (Zoomed)
All plots are exported as .png with high resolution (dpi=300).




▶️ How to Run the Project
1. Clone the repository
git clone https://github.com/YOUR_USERNAME/demand-forecasting.git
cd demand-forecasting


2. Install dependencies
pip install requirements.txt


3. Launch Jupyter Notebook
jupyter notebook


4. Open the notebook:
Demand Forecast.ipynb


5. Update the CSV path
Inside the notebook:
FILE_PATH = r"path/to/your/dataset.csv"



🏁 Conclusion
This project demonstrates a full machine learning workflow for demand forecasting:
Robust preprocessing
Feature engineering
Multiple ML models
Multi-step forecasting
Visualization and interpretability
Exportable outputs

The notebook is structured for readability, reproducibility, and clear end-to-end execution.


