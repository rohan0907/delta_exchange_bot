# Ultimate Crypto Trading Bot for Delta Exchange

A fully automated trading system designed to execute profitable trades efficiently on Delta Exchange. This bot integrates seamlessly with Delta Exchange's API, leveraging advanced trading strategies, risk management, and real-time market analysis to maximize returns.

## Features

### 1. Smart Trading Strategies
- **Scalping & Swing Trading** – Capitalizes on short-term price movements
- **Moving Average Crossover** – Uses SMA/EMA for trend-based trades
- **Breakout Trading** – Detects price breakouts and executes trades accordingly
- **Mean Reversion** – Buys when assets are oversold, sells when overbought
- **RSI & MACD Indicators** – Filters high-probability trades for better accuracy

### 2. Risk Management & Stop-Loss Protection
- **1:1 Risk-Reward Ratio** – Maintains a 10% take-profit (TP) & 10% stop-loss (SL) per trade
- **Leverage Support** – Trades with up to 10x leverage to maximize gains
- **Lot Size Control** – Limits each trade to 1 lot per position for steady risk management
- **Trailing Stop-Loss** – Protects profits by adjusting SL as price moves favorably

### 3. Automated & Real-Time Execution
- **High-Speed API Integration** – Executes trades in milliseconds with Delta Exchange
- **Auto-Rebalancing** – Adjusts positions based on market conditions
- **Real-Time Market Data** – Fetches live prices and trends instantly
- **Low Latency** – Ensures minimal lag between signal detection and execution

### 4. Multi-Coin & Altcoin Trading
- **Works with All Cryptocurrencies** – BTC, ETH, SOL, XRP, and more
- **Customizable Trading Pairs** – Select multiple assets for diversified trading
- **Market & Limit Orders** – Executes orders based on trader preference

### 5. Secure API & Fund Safety
- **HMAC-SHA256 API Security** – Encrypted requests ensure safe trading
- **No Withdrawal Access** – The bot only trades and cannot withdraw funds
- **Failsafe Mechanism** – Auto-pauses on extreme market conditions

### 6. User-Friendly Interface & Alerts
- **Web & Mobile Compatibility** – Runs on desktop & cloud-based servers
- **Telegram & Email Alerts** – Sends trade updates and market signals
- **Performance Dashboard** – Displays live profit/loss, trade history & analytics

## Installation

### Prerequisites
- Python 3.8+
- Delta Exchange API credentials

### Setup
1. Clone this repository:
   ```
   git clone https://github.com/yourusername/delta-exchange-bot.git
   cd delta-exchange-bot
   ```

2. Install required packages:
   ```
   pip install -r requirements.txt
   ```

3. Create a configuration file with your API credentials:
   ```python
   # config.py
   DELTA_API_KEY = "your_api_key"
   DELTA_API_SECRET = "your_api_secret"
   
   # Optional notification settings
   TELEGRAM_TOKEN = "your_telegram_bot_token"  # Optional
   TELEGRAM_CHAT_ID = "your_telegram_chat_id"  # Optional
   EMAIL = "your_email@example.com"  # Optional
   EMAIL_PASSWORD = "your_email_password"  # Optional
   ```

## Usage

### Backtesting
Before running the bot with real funds, you can backtest its performance:

```python
from delta_bot import DeltaExchangeBot

# Initialize the bot
bot = DeltaExchangeBot(
    api_key="your_api_key",
    api_secret="your_api_secret"
)

# Run backtest
results = bot.backtest_strategy(
    symbol="BTC/USDT",
    start_date="2023-01-01",
    end_date="2023-12-31",
    interval="1h",
    leverage=5.0
)

print(f"Backtest completed. Final capital: ${results['capital']:.2f}")
print(f"Win rate: {results['metrics']['win_rate']:.2f}%")
print(f"Profit factor: {results['metrics']['profit_factor']:.2f}")
```

### Live Trading
To start live trading:

```python
from delta_bot import DeltaExchangeBot

# Initialize the bot
bot = DeltaExchangeBot(
    api_key="your_api_key",
    api_secret="your_api_secret",
    telegram_token="your_telegram_bot_token",  # Optional
    telegram_chat_id="your_telegram_chat_id",  # Optional
    email="your_email@example.com",  # Optional
    email_password="your_email_password"  # Optional
)

# Define trading parameters
trading_symbols = ["BTC/USDT", "ETH/USDT", "SOL/USDT", "XRP/USDT"]
trading_interval = "1h"
trading_leverage = 5.0  # 5x leverage

# Start the bot
bot_thread = bot.run_bot(
    symbols=trading_symbols,
    interval=trading_interval,
    leverage=trading_leverage,
    check_interval_seconds=300  # Check every 5 minutes
)

# To stop the bot
bot.stop_bot()
```

### Customizing Trading Strategies
You can customize the bot's trading strategy:

```python
# Create a custom strategy
def my_custom_strategy(df):
    signals = pd.Series(0, index=df.index)
    
    # Define your strategy logic
    # Example: Buy when RSI < 30, Sell when RSI > 70
    signals[df['rsi'] < 30] = 1  # Buy signal
    signals[df['rsi'] > 70] = -1  # Sell signal
    
    return signals

# Run bot with custom strategy
bot_thread = bot.run_bot(
    symbols=["BTC/USDT"],
    strategy_func=my_custom_strategy,
    interval="1h",
    leverage=3.0
)
```

## Risk Warning
Trading cryptocurrencies involves substantial risk and may not be suitable for all investors. Make sure you understand the risks involved and never trade with capital you cannot afford to lose.

## Security Notes
- Never share your API keys
- Use API keys with trade-only permissions (no withdrawal access)
- Monitor the bot regularly
- Start with small trading amounts until you're confident in its performance

## License
This project is licensed under the MIT License - see the LICENSE file for details.
