# Corporación Favorita Grocery Sales Forecasting - Guayas

This project focuses on preparing and exploring grocery sales data for the Guayas state, as part of a larger sales forecasting project.

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

*A full markdown summary with next-step checklist is appended to the notebook `Corporación_Favorita_Grocery_Guayas_Further_EDA.ipynb`.*

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

### Next (Part 4 → XGBoost / LSTM Hypertuning)

* Retrain XGBoost + new features  
* Train LSTM with log-scaled target & weekly differencing   
* Push best model into `streamlit` app, add forecast summary table + interactive chart.

---

This multi-part project explores and forecasts grocery sales in Ecuador’s Guayas province.  
Each notebook adds new capability: rigorous data prep (Part 1), first ML/DL models (Part 2), deeper diagnostics & feature ideas (Part 3), and advanced modelling (Part 4).
