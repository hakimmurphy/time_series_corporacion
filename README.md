# 🛒 Corporación Favorita Grocery Sales Forecasting – Guayas

**Live app:** <https://forecasterapp-re6sa3sspcdsceht7piq9s.streamlit.app/>  
**GitHub repo:** <https://github.com/hakimmurphy/forecaster_app>

This multi-part project explores and forecasts grocery sales in Ecuador’s Guayas province.  
Each notebook adds new capability: rigorous data prep (Part 1), first ML/DL models (Part 2), deeper diagnostics & feature ideas (Part 3), and advanced hyper-tuned modelling (Part 4).

## ✅ Part 1 – Data Preparation & Exploratory Analysis  

| Step | Highlights |
|------|------------|
| **Data Filtering** | subset to Guayas state |
| **Cleaning** | • filled `onpromotion` nulls<br>• flipped negative returns to 0<br>• Z-score outlier removal |
| **Feature Engineering** | calendar vars (day, month, weekday, etc.) + 7-day rolling mean |
| **EDA** | • line plots of trend • monthly heat-map • holiday impact bars • perishable vs non-perishable split • focus on top-3 families |

This foundation supports every later model.

---

## 🚀 Part 2 – Baseline Modelling & Forecasting  

### 🔹 XGBoost
* **Inputs:** lag features + calendar dummies  
* **Findings:** captures trend & weekly seasonality; error spikes on extreme days  
* **Use-case:** short-horizon, interpretable SHAP explanations  

### 🔹 LSTM
* **Inputs:** 30-day sequences (3-D tensors)  
* **Performance:** predicted curve shadows actual curve; good with seasonality; slight lag on sharp jumps  
* **Next:** validate on unseen weeks; benchmark MAE / RMSE vs XGBoost  

---

## 🔍 Part 3 – Further EDA & Feature-Engineering Insights  

| Analysis | Insight | What to add to models |
|----------|---------|-----------------------|
| **STL decomposition** | clear upward trend + strong 7-day seasonality | trend term / seasonal order 7 |
| **ACF / PACF** | spikes at lags 7, 14, 21; MA(1) behaviour | Suggested: SARIMA (0,1,1)(1,1,0)[7] baseline |
| **Outlier inspection** | single zero-sales dip (early 2014) + extreme holiday peaks | mask / clip outliers |
| **Feature gaps discovered** | holiday lead/lag, on-promotion %, capacity-hit flags, perishable interactions | engineer these for Part 4 |
| **Cross-validation advice** | use `TimeSeriesSplit(gap=7)` to avoid leakage | robust CV pipeline |

--- 

## 🚀 Part 4 – Hyper-parameter Tuning & Final Model Selection

| Model | Tuned parameters | Hold-out RMSE | MAE |
|-------|------------------|---------------|-----|
| XGBoost (baseline) | default | 10 600 | 6 900 |
| **XGBoost (tuned)** |  n_estimators = 750, max_depth = 6, eta = 0.05, subsample = 0.8, colsample = 0.9 | **8 900** | **5 600** |
| LSTM (seq = 30) | 1× 64 units, dropout 0.2, epochs 30 | 9 400 | 6 100 |

* XGBoost hyper-search with `TimeSeriesSplit(gap=7)` cut error ~16 % over baseline.  
* Tuned XGBoost serialized (`XGBoost.pkl`) and wired into the Streamlit app.  
* LSTM shows promise but needs more tuning/ensembling for peak-day accuracy.

**Planned next steps**  
1. Quantile forecasts for inventory safety-stock.  
2. Blend XGBoost + LSTM for holiday peaks.  
3. Compare against classical SARIMA benchmark for transparency.

---

## 🛠 Tools

| Category | Stack |
|----------|-------|
| Language | Python 3.9 |
| Core libs | Pandas • NumPy • Matplotlib • Seaborn |
| ML / DL  | XGBoost • Scikit-learn • TensorFlow / Keras |
| Stats     | statsmodels • scipy |
| Environment | Jupyter / Google Colab • Streamlit for interactive app |

---
