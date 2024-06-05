# Stock Price Prediction

## Features in the Data

### Next Day Adjusted Close Price:
- **Definition**: The closing price of the stock adjusted for corporate actions like dividends, stock splits, etc., for the next trading day. This is our target variable for predictive modeling. The goal is to predict this value using other features in the dataset.

### Open:
- **Definition**: The price at which the stock opened for trading on a particular day. Used to understand the day's price movement and can be a feature in predictive models.

### LogRange (Stock Daily High - Low):
- **Definition**: The logarithm of the range between the highest and lowest prices of the day. It's a Risk Indicator.
  - Indicates the volatility or risk of the stock on that particular day. Higher values suggest higher risk.

### Log_Volume (Log Value of Daily Traded Volume):
- **Definition**: The logarithm of the total volume of shares traded on a particular day.
  - Reflects the trading activity and liquidity of the stock. Higher values indicate higher trading activity.

### Return_Percentage:
- **Definition**: The percentage change in the adjusted close price from the previous day to the current day. Calculated as \[((Today Adj Close - Prior Day Adj Close) / Prior Day Adj Close) * 100%\]
  - Indicates the profitability of holding the stock. Positive values indicate a gain, while negative values indicate a loss.

### 3_Day_Avg_AdjClose (Market Price Level Assessment Indicator, Delay=3):
- **Definition**: The average of the adjusted close prices over the past three days.
  - Provides a short-term trend indicator and smooths out daily fluctuations.

### PriorDay_AdjClose:
- **Definition**: The adjusted close price of the prior trading day.
  - Helps in calculating returns and can be a feature in predictive models.

## Data Pre-processing
- **Converted Data Types**: The data is converted to desired datatypes.
- **Dropped Missing Dates**: Dropped the rows where the date is not present since it accounted for 3% of the data.
- **Inferred Frequency and Filled Missing Values**: Frequency is inferred for the datetime index, and missing dates are filled along with other columns with the mean.

## Data Analysis
- **Correlation Plot**:
  - **Open, Range, and PriorDay_AdjClose**: These variables show a higher correlation with the Adj Close price.
  - **Volume, Log_Volume, and Return_Percentage**: These variables show some correlation with each other and with other features but not strongly with Adj Close.
  - **3_Day_Avg_AdjClose (Delay)**: Shows a strong positive correlation with the Adj Close price, indicating it could be a significant predictor.

- **Trend Analysis**: The Adjusted Close price shows an overall upward trend from January 2023 to May 2024.
  - There are noticeable periods of increased volatility, especially towards the end of the period.

- **Feature Selection**: Focus on features that have a higher correlation with the target variable (Adj Close), such as Open, Range, PriorDay_AdjClose, and 3_Day_Avg_AdjClose (Delay).

## Models Used
1. **Linear Regression**:
2. **ARIMA**:
   - First used without differencing, it produced bad results.
   - Performed Adfuller test to check if data is stationary or not; it came out to be non-stationary.
3. **ARIMA with First Order Differencing**:
   - Differencing was performed.
   - Checked seasonality by plotting, and seasonality was observed.
4. **Differenced SARIMA (diff=5)**:
5. **Differenced SARIMA (diff=1)**:
6. **AUTO-ARIMA**:
7. **Exponential Smoothing**:
   - Used with and without differencing, performed better than ARIMA.
8. **SARIMAX (SARIMA with Exogenous Variables)**:
   - Produced the best results with:
     - **Mean Absolute Error (MAE)**: 14.959487511807463
     - **Mean Squared Error (MSE)**: 438.8020128153929
     - **Root Mean Squared Error (RMSE)**: 20.94760160055067

