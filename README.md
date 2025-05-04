# Corporación Favorita Grocery Sales Forecasting - Guayas

This project focuses on preparing and exploring grocery sales data for the Guayas state, as part of a larger sales forecasting project.

## Completed in Part 1: Data Preparation & EDA

* **Data Filtering:** Filtered the dataset to focus on Guayas state.
* **Data Cleaning:** 
    * Handled missing values in the `onpromotion` column.
    * Replaced negative sales with 0 to reflect returns as non-sales.
    * Identified and handled outliers using Z-score analysis.
* **Feature Engineering:**
    * Created time-based variables (day, month, year, weekday, etc.).
    * Calculated a 7-day rolling average of unit sales.
* **Exploratory Data Analysis (EDA):**
    * Visualized sales trends over time using line plots.
    * Analyzed monthly sales patterns with a heatmap.
    * Explored the impact of holidays on sales using bar plots.
    * Visualized sales of perishable vs. non-perishable items.
    * Focused analysis on the top 3 product families.

This sets the foundation for modeling and forecasting in future parts.

## Part 2: Modeling & Forecasting
* **XGBoost Model**
   * Built a gradient-boosted tree model using lag features and time-based variables.
   * Trained on historical sales to predict future values.
* **Performance Analysis:**
   * Actual vs. Predicted plots show that XGBoost captures overall trends but shows variability during high or low sales days.
   * Model is interpretable and performs well for short-horizon predictions.
 * **LSTM Model**
   * A recurrent neural network (LSTM) was used to learn temporal dependencies and patterns in sales data.
 * **Model Performance:**
    * Predicted sales (dashed line) closely follow actual sales, showing strong temporal learning.
    * Handles seasonality and periodicity well.
 * **Pattern Recognition:**
    * Effectively tracks fluctuations and cyclical patterns in sales.
    * Slight prediction lag during abrupt changes.
 * **Recommendations:**
    * Evaluate using MAE/RMSE for numeric accuracy.
    * Test on unseen data to ensure robustness.
    * Promising for mid- to long-term forecasting scenarios.    

## Tools Used

* **Programming Language:** Python
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, XGBoost, Scikit-learn, TensorFlow/Keras
* **Environment:** Jupyter Notebook (Google Colab)

* 
