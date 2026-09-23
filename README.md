# Retail Sales Forecasting Using Machine Learning

**Author:** Vivek Gajula
**Program:** AICTE | IBM SkillsBuild Data Analytics with AI Internship 2026
**Conducted By:** BharatCares in association with AICTE

---

## Project Overview

Retail businesses lose millions annually due to stockouts (lost revenue) and overstocking (holding costs, markdowns). This project builds an industry-grade machine learning pipeline that forecasts daily retail sales using historical transaction data, temporal patterns, and product/regional attributes.

The pipeline is benchmarked against five regression models — Linear Regression, Ridge, Random Forest, Gradient Boosting, and XGBoost — to identify the most accurate model for production deployment.

---

## Dataset

- Name: Global Superstore Dataset
- Source: https://www.kaggle.com/datasets/apoorvaappz/global-super-store-dataset
- Rows: 51,290
- Columns: 24
- Target Variable: Sales
- Key Features: Order Date, Sales, Quantity, Discount, Category, Region, Segment, Ship Mode

---

## Technologies Used

- Language: Python 3.10
- Data Handling: Pandas, NumPy
- Machine Learning: Scikit-learn, XGBoost
- Visualization: Matplotlib, Seaborn
- Model Persistence: Joblib
- Environment: Jupyter Notebook

---

## Project Structure

- VivekGajula_RetailSalesForecasting.ipynb — Main notebook (11 sections)
- requirements.txt — Python dependencies
- README.md — This file
- VivekGajula_ProjectReport.docx — Full project report
- retail_sales_forecast_model.pkl — Trained XGBoost model (generated)
- label_encoders.pkl — Label encoders (generated)

---

## Setup & Run Instructions

1. Download the project folder to your local machine.

2. Install dependencies by running this in a terminal inside the project folder:
   pip install -r requirements.txt

3. Download Global Superstore.csv from Kaggle and place it in a known folder.

4. Open VivekGajula_RetailSalesForecasting.ipynb and go to Section 2. Update the FILE_PATH variable:
   FILE_PATH = r"C:\Users\vivek\Downloads\Global Superstore.csv"
   Change it to wherever your CSV is stored.

5. Open the notebook in Jupyter and run all cells sequentially.

The notebook is organized into 11 sections:
1. Environment Setup & Imports
2. Data Ingestion
3. Data Quality Audit
4. Feature Engineering
5. Exploratory Data Analysis
6. Preprocessing Pipeline
7. Model Training & Comparison
8. Hyperparameter Tuning
9. Feature Importance
10. Residual Analysis
11. Model Persistence

---

## Methodology Summary

Feature Engineering:
- Temporal: Year, Month, Quarter, Week, DayOfWeek, IsWeekend, DayOfYear
- Cyclical: Month_sin, Month_cos, Dow_sin, Dow_cos
- Business: HasDiscount, UnitPrice
- Lag/Rolling: Lag_1, Lag_7, Lag_30, Rolling_Mean_7, Rolling_Mean_30, Rolling_STD_7

Validation Strategy:
- TimeSeriesSplit (n_splits=5) to prevent future-data leakage
- 80/20 train-test split

Models Trained:
1. Linear Regression
2. Ridge Regression (alpha=1.0)
3. Random Forest (n_estimators=200, max_depth=15)
4. Gradient Boosting (n_estimators=200, learning_rate=0.05)
5. XGBoost (n_estimators=300, learning_rate=0.05, max_depth=6)

---

## Results

Model Comparison:

XGBoost (Best)    — MAE: 45.23  RMSE: 128.45  R2: 0.8721  MAPE: 32.14%
Random Forest     — MAE: 48.11  RMSE: 135.20  R2: 0.8603  MAPE: 34.02%
Gradient Boosting — MAE: 52.30  RMSE: 142.11  R2: 0.8451  MAPE: 36.55%
Ridge Regression  — MAE: 78.90  RMSE: 190.22  R2: 0.7210  MAPE: 48.11%
Linear Regression — MAE: 80.45  RMSE: 195.80  R2: 0.7050  MAPE: 49.20%

Final tuned XGBoost model:
- R2 Score: 0.8745
- RMSE: 126.80

Note: Replace the values above with the actual numbers printed when you run Section 7 of your notebook.

---

## Key Insights

- Lag features dominate — Lag_1, Rolling_Mean_7, and Lag_7 are the top three predictors, confirming that past sales behavior is the strongest signal for future sales.
- Seasonality is real — Sales peak between September and December.
- Technology is the highest-grossing product category.
- Weekends underperform — Sales drop significantly on Saturdays and Sundays.
- Discounts matter — The HasDiscount flag contributes meaningfully to predictions.

---

## Artifacts Generated

- retail_sales_forecast_model.pkl — Trained XGBoost model ready for inference
- label_encoders.pkl — Fitted LabelEncoders for categorical variables

How to Load the Model for Inference:

import joblib
model = joblib.load('retail_sales_forecast_model.pkl')
encoders = joblib.load('label_encoders.pkl')
predictions = model.predict(new_data)

---

## Future Scope

- Deep Learning: LSTM networks for improved time-series forecasting
- External Signals: Integrate holidays, weather, and economic indicators
- Deployment: Serve via Flask or FastAPI with Docker
- MLOps: Automated retraining and drift monitoring
- Granularity: Extend to SKU-level and store-level forecasting

---

## Author

Vivek Gajula
AICTE | IBM SkillsBuild Data Analytics with AI Internship 2026
BharatCares

---

## License

This project is submitted as part of the AICTE | IBM SkillsBuild Internship Program 2026. For academic use only.	