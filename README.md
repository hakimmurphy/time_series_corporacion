# Corporación Favorita Grocery Sales Forecasting - Guayas

This project focuses on preparing and exploring grocery sales data for the Guayas state, as part of a larger sales forecasting project.

## Completed in Part 1

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

## Tools Used

* **Programming Language:** Python
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn
* **Environment:** Jupyter Notebook (Google Colab)
