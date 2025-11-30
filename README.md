# Ex.No: 01A PLOT A TIME SERIES DATA
###  Date: 19/08/2025
### Name: Visalan H
### Registration Number: 212223240183

# AIM:
To Develop a python program to Plot a time series data (population/ market price of a commodity
/temperature.
# ALGORITHM:
1. Import the required packages like pandas and matplot
2. Read the dataset using the pandas
3. Calculate the mean for the respective column.
4. Plot the data according to need and can be altered monthly, or yearly.
5. Display the graph.
# PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("C:\DL\dataSets\GoldPrice(2013-2023).csv")

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['Price'] = data['Price'].str.replace(',', '').astype(float)
data['price_diff'] = data['Price'] - data['Price'].shift(1)

result = seasonal_decompose(data['Price'], model='additive', period=12)
data['price_sea_diff'] = result.resid

data['price_log'] = np.log(data['Price'])
data['price_log_diff'] = data['price_log'] - data['price_log'].shift(1)

result = seasonal_decompose(data['price_log_diff'].dropna(), model='additive', period=12)
data['price_log_seasonal_diff'] = result.resid

plt.figure(figsize=(10, 5))
plt.plot(data['Price'], label='Original Price')
plt.title('Original Gold Price Data')
plt.xlabel('Year')
plt.ylabel('Price')
plt.legend()
plt.show()

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 2)
plt.plot(data['price_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Price')
plt.show()

plt.subplot(6, 1, 3)
plt.plot(data['price_sea_diff'], label='Seasonal Decomposition Residual')
plt.legend(loc='best')
plt.title('Seasonal Residuals')
plt.xlabel('Date')
plt.ylabel('Residuals')
plt.show()

plt.subplot(6, 1, 4)
plt.plot(data['price_log'], label='Log Transform')
plt.legend(loc='best')
plt.title('Log Transformed Gold Price')
plt.xlabel('Date')
plt.ylabel('Log Price')
plt.show()

plt.subplot(6, 1, 5)
plt.plot(data['price_log_diff'], label='Log Differencing')
plt.legend(loc='best')
plt.title('Log Differencing')
plt.xlabel('Date')
plt.ylabel('Log Price Diff')
plt.show()

plt.subplot(6, 1, 6)
plt.plot(data['price_log_seasonal_diff'], label='Log Seasonal Residual')
plt.legend(loc='best')
plt.title('Seasonal Residuals (Log Differenced)')
plt.xlabel('Date')
plt.ylabel('Residuals')

plt.tight_layout()
plt.show()

```
# OUTPUT:

<img width="1070" height="581" alt="image" src="https://github.com/user-attachments/assets/7aca035e-acf5-4ff8-9e8c-45e35c929c90" />

<img width="735" height="176" alt="image" src="https://github.com/user-attachments/assets/cfcb304c-1879-4a61-ba86-ebaa9e31a65e" />

<img width="728" height="161" alt="image" src="https://github.com/user-attachments/assets/7a924bd2-4470-4893-962b-c90169e957be" />

<img width="708" height="169" alt="image" src="https://github.com/user-attachments/assets/2d2ed31b-4d0b-44eb-b50e-ee3783065b26" />

<img width="705" height="165" alt="image" src="https://github.com/user-attachments/assets/b6849c3a-fbd5-4aa9-9511-899292243f8a" />

<img width="789" height="145" alt="image" src="https://github.com/user-attachments/assets/1187cb34-8093-4501-855a-824bbdcad9b0" />

# RESULT:
Thus we have created the python code for plotting the time series of given data.
