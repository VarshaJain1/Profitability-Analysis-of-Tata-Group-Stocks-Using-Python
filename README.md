# Profitability-Analysis-of-Tata-Group-Stocks-Using-Python
This project aims to analyze the profitability of Tata Group stock(s) using Python. We'll use financial and stock market data to evaluate historical returns, volatility, and key profitability ratios.
. Import Libraries
python
Copy
Edit
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import yfinance as yf
from datetime import datetime
Data Collection
ticker = 'TCS.NS'  # NSE ticker for Tata Consultancy Services
start_date = '2015-01-01'
end_date = datetime.today().strftime('%Y-%m-%d')

tcs_data = yf.download(ticker, start=start_date, end=end_date)
tcs_data.head()
Data Cleaning & Exploration
print(tcs_data.isnull().sum())
tcs_data.describe()
tcs_data['Close'].plot(figsize=(12,6), title='TCS Stock Closing Price')
 Profitability Metrics
You can analyze:
 Daily & Cumulative Returns
tcs_data['Daily Return'] = tcs_data['Close'].pct_change()
tcs_data['Cumulative Return'] = (1 + tcs_data['Daily Return']).cumprod()
tcs_data[['Close', 'Cumulative Return']].plot(subplots=True, figsize=(12,8))
Annualized Return and Volatility
trading_days = 252
annual_return = tcs_data['Daily Return'].mean() * trading_days
annual_volatility = tcs_data['Daily Return'].std() * np.sqrt(trading_days)
print(f"Annual Return: {annual_return:.2%}")
print(f"Annual Volatility: {annual_volatility:.2%}")
Sharpe Ratio
risk_free_rate = 0.06  # you can change based on India 10Y bond yield
sharpe_ratio = (annual_return - risk_free_rate) / annual_volatility
print(f"Sharpe Ratio: {sharpe_ratio:.2f}")
Fundamental Profitability Ratios (Optional but valuable)
Net Profit Margin
ROE (Return on Equity)
ROA (Return on Assets)
Earnings Per Share (EPS)
EBITDA Margin
net_income = 39297  # Cr (INR)
revenue = 228907
net_profit_margin = net_income / revenue
print(f"Net Profit Margin: {net_profit_margin:.2%}")
tickers = ['TCS.NS', 'TATAMOTORS.NS', 'TATASTEEL.NS']
data = yf.download(tickers, start=start_date, end=end_date)['Adj Close']
returns = data.pct_change()
cumulative_returns = (1 + returns).cumprod()
cumulative_returns.plot(figsize=(12,6), title='Cumulative Returns of Tata Group Stocks')
Conclusion
Summarize findings:
Which stock is more profitable?
Historical performance vs. market benchmarks
Risk-adjusted performance
TCS has shown consistent returns with moderate volatility and a strong Sharpe ratio. The stock exhibits strong profitability metrics, making it a suitable long-term investment.
