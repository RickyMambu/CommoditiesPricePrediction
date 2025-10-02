# CommoditiesPricePrediction
This repository contains the code and experiments for predicting daily commodity prices using **Long Short-Term Memory (LSTM)** models.   The objective is to minimize prediction error (MSE, MAE, RMSE) and provide a reliable tool for short-term forecasting of commodity prices in Indonesia.


---

## 🚀 Objective
To build a **time-series forecasting model** for commodity prices that can:
- Predict the **next day’s price** with minimal error.
- Leverage historical data (lags, rolling averages) and external factors (currency exchange rate, CPI, weather).
- Be deployable into a production system (with Firebase integration).

---

## 📊 Dataset
The dataset combines:
- **Prices**: Daily commodity prices (scraped from BI / manual input).  
- **Exogenous features**:  
  - Currency exchange rate (USD/IDR) — Yahoo Finance.  
  - CPI (Consumer Price Index) — FRED.  
  - Weather data (temperature, rainfall, humidity) — NASA POWER API.  
- **Engineered features**: Lag variables, rolling means, percentage change, calendar features.

➡️ Final features:  
`prices, rolling_mean_7, rolling_mean_30, lag_1, lag_7, lag_30, pct_change_1, pct_change_7, day_of_week, day_in_month, cpi, usd_idr, Temperature, Curah Hujan, Kelembapan`

---

## 🏗️ Model Architecture
**LSTM_v2_Imputed** (current best model):

- LSTM(128, return_sequences=True)  
- Dropout(0.3)  
- LSTM(64)  
- Dropout(0.3)  
- Dense(64, ReLU)  
- Dense(1)  

**Optimizer**: Adam  
**Loss function**: Mean Squared Error  

---

## ⚙️ Training Setup
- Epochs: 150  
- Batch size: 32  
- Validation split: 20%  
- Callbacks:  
  - EarlyStopping (patience=10)  
  - ReduceLROnPlateau  
  - ModelCheckpoint  

---

## ✅ Evaluation Results
Test set performance (LSTM_v2_Imputed):  
- **MSE**: 1,293,069.60  
- **MAE**: 916.23  
- **RMSE**: 1,137.13  

👉 Average daily prediction error: **~Rp 916 (≈2–3%)**

---

## 📈 Visualizations
- Actual vs Predicted Prices  
- Error Distribution  
- Training & Validation Loss Curves  

---

## 📜 License
Released under **CC BY 4.0** with attribution to original data sources (NASA POWER, Yahoo Finance, FRED, BI).  

---

