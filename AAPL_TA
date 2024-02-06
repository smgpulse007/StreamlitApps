import streamlit as st
import yfinance as yf
import pandas as pd
import plotly.graph_objects as go

# Title of the web app
st.title('Stock Data Visualization')

# Sidebar inputs for user interaction
ticker = st.sidebar.text_input('Stock Ticker', value='AAPL', max_chars=5)
start_date = st.sidebar.date_input('Start Date', value=pd.to_datetime('2023-07-01'))
end_date = st.sidebar.date_input('End Date', value=pd.to_datetime('2024-01-31'))
window = st.sidebar.slider('SMA/EMA Window', min_value=5, max_value=50, value=20)

# Fetch historical stock data from Yahoo Finance
data = yf.download(ticker, start=start_date, end=end_date)

# Calculate SMA and EMA
sma = data['Close'].rolling(window=window).mean()
ema = data['Close'].ewm(span=window, adjust=False).mean()

# Plotting
fig = go.Figure()
fig.add_trace(go.Scatter(x=data.index, y=data['Close'], name='Stock Prices', mode='lines'))
fig.add_trace(go.Scatter(x=data.index, y=sma, name='SMA', mode='lines'))
fig.add_trace(go.Scatter(x=data.index, y=ema, name='EMA', mode='lines'))

# Use Streamlit to display the plotly figure
st.plotly_chart(fig)
