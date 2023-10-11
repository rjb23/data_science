# data_science #datafinance #python
pip install yfinance pandas matplotlib

import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt

# Define the S&P 500 ticker symbol and date range
ticker_symbol = "^GSPC"
start_date = "2003-01-01"
end_date = "2023-01-01"

# Fetch S&P 500 historical data from Yahoo Finance
sp500_data = yf.download(ticker_symbol, start=start_date, end=end_date)

# Create a new figure for the plots
plt.figure(figsize=(12, 6))

# Plot the S&P 500 Closing Price
plt.subplot(2, 2, 1)
plt.plot(sp500_data['Close'], label='S&P 500 Close Price', color='blue')
plt.title('S&P 500 Closing Price')
plt.xlabel('Year')
plt.ylabel('Price')
plt.grid()
plt.legend()

# Plot S&P 500 Daily Returns
plt.subplot(2, 2, 2)
sp500_data['Return'] = sp500_data['Close'].pct_change() * 100
plt.plot(sp500_data['Return'], label='S&P 500 Daily Returns', color='green')
plt.title('S&P 500 Daily Returns')
plt.xlabel('Year')
plt.ylabel('Percentage Return')
plt.grid()
plt.legend()

# Plot S&P 500 Moving Average
plt.subplot(2, 2, 3)
sp500_data['50_MA'] = sp500_data['Close'].rolling(window=50).mean()
sp500_data['200_MA'] = sp500_data['Close'].rolling(window=200).mean()
plt.plot(sp500_data['Close'], label='S&P 500 Close Price', color='blue')
plt.plot(sp500_data['50_MA'], label='50-day Moving Average', color='red')
plt.plot(sp500_data['200_MA'], label='200-day Moving Average', color='orange')
plt.title('S&P 500 Moving Averages')
plt.xlabel('Year')
plt.ylabel('Price')
plt.grid()
plt.legend()

# Plot S&P 500 Volume
plt.subplot(2, 2, 4)
plt.bar(sp500_data.index, sp500_data['Volume'], color='purple', label='S&P 500 Volume')
plt.title('S&P 500 Trading Volume')
plt.xlabel('Year')
plt.ylabel('Volume')
plt.grid()
plt.legend()

# Adjust layout and display the plots
plt.tight_layout()
plt.show()
