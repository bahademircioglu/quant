# 📈 Quant Crypto Backtesting Framework

This project is a simple and extensible framework for **cryptocurrency trading strategy backtesting** using historical market data. It allows you to fetch minute-level data from Binance and test trading strategies with indicators like **RSI**, **MACD**, and **ATR**.

## 🚀 Features

- 📊 Fetch historical crypto data from Binance API
- ⚙️ Compute indicators: RSI, MACD, and ATR
- 🔁 Backtest long/short strategies with dynamic stop-loss and take-profit
- 💰 Simulate account balance, risk management per trade, and PnL tracking
- 🧩 Easily extendable for new symbols or strategies

---

## 📁 Project Structure

```
quant/
├── backtesting.ipynb       # Runs the backtesting engine
├── data_fetcher.ipynb      # Fetches historical Binance data and saves to CSV
├── crypto_data/            # Folder where fetched CSVs are saved
└── README.md               # Project description and usage instructions
```

---

## ⚙️ Setup

### 1. Clone the Repository

```bash
git clone https://github.com/bahademircioglu/quant.git
cd quant
```

### 2. Install Required Packages

> Requires Python 3.7+ and Jupyter environment (or JupyterLab)

You can install dependencies via pip:

```bash
pip install pandas numpy requests
```

Or use a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

*Optional: Jupyter Notebook support*

```bash
pip install notebook
```

---

## 🧠 Usage

### 📥 1. Fetch Historical Crypto Data

Run `data_fetcher.ipynb` to fetch historical minute-level OHLCV data for:

- BTCUSDT
- ETHUSDT
- SOLUSDT
- BNBUSDT

```python
fetcher = CryptoDataFetcher()
fetcher.fetch_and_save_data("2022-01-01", "2023-01-01")
```

This will generate one `.csv` file per symbol inside the `crypto_data/` folder.

> ⚠️ **Note:** You can adjust the date range (`start_date`, `end_date`) to widen or narrow the dataset. Also, you can modify the `trading_pairs` list inside `CryptoDataFetcher` to include more coins.

---

### 📈 2. Run the Backtest

Run the `backtesting.ipynb` notebook or script:

```python
backtest = TradingStrategyBacktest()
backtest.run_backtest()
```

This will:

- Load your fetched CSV data
- Calculate RSI, MACD, and ATR
- Simulate trades based on strategy logic
- Track entry/exit points, PnL, and update balance

> ✅ Strategy Logic:
>
> - Enter **long** when RSI > 70 and MACD crossover is bearish
> - Enter **short** when RSI < 30 and MACD crossover is bullish
> - Exit with dynamic **stop-loss (3%)** or **take-profit (10%)**

---

## 📊 Sample Output

```plaintext
Running backtest for BTCUSDT...
2022-01-10 13:25:00: Entered long position at 43200.5
2022-01-10 14:18:00: Closed long position at 47500.2 with 9.96% profit
Final balance: $1084.10
Trade summary:
  symbol   type   entry    exit     pnl   cost
0 BTCUSDT  long  43200.5  47500.2   9.96  84.10
...
```

---

## 🛠️ Customize

You can easily tweak:

- **Risk and profit settings** in `TradingStrategyBacktest`:
  ```python
  backtest = TradingStrategyBacktest(
      starting_balance=1000,
      risk_per_trade=0.01,
      take_profit=0.05
  )
  ```

- **Trading rules or entry/exit conditions** in `run_backtest()`

- **New indicators or strategies** by adding methods in `TradingStrategyBacktest`

---

## 📌 Future Improvements

- Strategy optimization (grid search or genetic algorithms)
- More technical indicators (Bollinger Bands, EMA crossover, etc.)
- Visualization of trades on candlestick charts
- Portfolio-level performance metrics (Sharpe, drawdown, etc.)

---

## 🤝 Contributing

Feel free to fork and PR your improvements, new strategies, or better visualizations!

---

## 📬 Author

Developed by [@bahademircioglu](https://github.com/bahademircioglu)  
Reach out for collaboration or feedback!
