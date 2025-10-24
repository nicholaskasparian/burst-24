# Burst-24 Trading Bot

An automated trading bot that executes trades on the Alpaca trading platform based on daily stock price movements. The bot analyzes percentage changes in stock prices and automatically places buy or sell orders proportional to the price movement and a configurable risk tolerance.

## Overview

Burst-24 is a Python-based algorithmic trading bot that:
- Monitors a predefined list of S&P 500 stocks
- Analyzes daily price changes (close vs. open)
- Automatically executes trades based on percentage movements
- Uses Alpaca's paper trading API for safe testing
- Implements a risk tolerance mechanism to control position sizing

## Features

- **Automated Trading**: Executes trades automatically based on daily price movements
- **Risk Management**: Configurable risk tolerance (default: $3000) to limit exposure
- **Bull & Bear Strategies**: Buys stocks that moved up, shorts stocks that moved down
- **Paper Trading**: Uses Alpaca's paper trading environment for risk-free testing
- **S&P 500 Coverage**: Monitors a comprehensive list of major US stocks
- **Error Handling**: Continues trading even if individual stock data is unavailable

## Prerequisites

- Python 3.x
- Alpaca trading account (paper trading recommended)
- Alpaca API credentials (API Key ID and Secret Key)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/nicholaskasparian/burst-24.git
cd burst-24
```

2. Install required dependencies:
```bash
pip install alpaca-py python-dotenv
```

## Configuration

1. Create a `.env` file in the project root directory:
```bash
touch .env
```

2. Add your Alpaca API credentials to the `.env` file:
```
APCA_API_KEY_ID=your_api_key_id_here
APCA_API_SECRET_KEY=your_api_secret_key_here
```

## Usage

Run the trading bot:
```bash
python script.py
```

The bot will:
1. Close all existing positions and cancel pending orders
2. Fetch yesterday's stock data for all monitored symbols
3. Calculate percentage changes between open and close prices
4. Execute trades proportional to the price movement and risk tolerance
5. Display a summary of all executed trades

## How It Works

### Trading Logic

1. **Data Collection**: The bot retrieves yesterday's stock data (open and close prices) for each symbol in the tradeable list.

2. **Percentage Calculation**: For each stock, it calculates the percentage change:
   ```
   Percentage Change = ((Close - Open) / Open) × 100
   ```

3. **Trade Execution**:
   - **Bullish Move** (positive change): Places a buy order
     - Amount = Percentage Change × Risk Tolerance
   - **Bearish Move** (negative change): Places a sell (short) order
     - Quantity = (Absolute Percentage Change × Risk Tolerance) / Current Price
   - **No Change**: No trade is executed

4. **Position Sizing**: The risk tolerance parameter controls the dollar amount at risk per percentage point of movement.

### Example

If a stock moves up 2.5% with a risk tolerance of $3000:
- Buy order amount = 3.5 × $3000 = $10500

If a stock moves down 1.8% with a risk tolerance of $3000 and current price of $100:
- Sell quantity = (1.8% × $3000) / $100 = 0.54 shares (rounded to integer)

## Risk Disclaimer

⚠️ **IMPORTANT**: This bot is for educational and research purposes only.

- **Always use paper trading** when testing automated trading strategies
- Algorithmic trading involves substantial risk of loss
- Past performance does not guarantee future results
- The bot uses a simplified strategy that may not account for market conditions, liquidity, or other important factors
- Never invest more than you can afford to lose
- Consult with a financial advisor before implementing any trading strategy with real money

## Technical Details

- **Language**: Python 3.x
- **Trading Platform**: Alpaca (https://alpaca.markets/)
- **API Client**: alpaca-py
- **Trading Mode**: Paper trading (by default)
- **Timeframe**: Daily bars
- **Order Type**: Market orders with Day time-in-force

## Monitored Stocks

The bot monitors a comprehensive list of S&P 500 stocks including major companies like:
- Tech: AAPL, MSFT, GOOGL, AMZN, NVDA, AMD, etc.
- Finance: JPM, BAC, GS, C, WFC, etc.
- Healthcare: JNJ, PFE, ABBV, UNH, etc.
- And many more...

(See `tradeable` list in `script.py` for the complete list)

## Limitations

- Only processes stocks from the predefined list
- Executes trades once per run (not continuous monitoring)
- Uses simple percentage-based strategy without technical indicators
- No stop-loss or take-profit mechanisms
- Requires manual execution (not scheduled)

## Future Enhancements

Potential improvements could include:
- Scheduled execution (e.g., daily at market open)
- More sophisticated trading signals (technical indicators, moving averages)
- Stop-loss and take-profit orders
- Performance tracking and reporting
- Real-time trade monitoring
- Portfolio rebalancing logic

## License

<a href="https://github.com/nicholaskasparian/burst-24">burst-24</a> © 2025 by <a href="https://github.com/nicholaskasparian">Nicholas Kasparian</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International</a><img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/nc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/sa.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;">

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page or submit a pull request.

## Disclaimer

This software is provided for educational and informational purposes only. It is not financial advice. Trading stocks involves risk, and you should never trade with money you cannot afford to lose. Always do your own research and consult with qualified financial professionals before making investment decisions.
