# Advanced Intraday Stock Signal Dashboard + Kite Connect Live Trading

A Streamlit app for Indian intraday trading research, paper trading, and optional live execution through Kite Connect.

## What this app does

- Downloads historical OHLCV data with `yfinance` for training and backtesting
- Uses a Streamlit UI for live monitoring
- Connects to Kite Connect for authentication, market data streaming, and order placement
- Builds technical, volume, volatility, session, and regime features
- Trains models with time-ordered validation
- Tunes the trading threshold using validation performance
- Supports PAPER mode and LIVE mode
- Logs orders and signals locally

## Important

This app is not a guarantee of profit.

Start in PAPER mode and validate everything before enabling live orders.

## Kite Connect setup

You need:

- `KITE_API_KEY`
- `KITE_API_SECRET`
- `KITE_ACCESS_TOKEN` after session generation

The session flow is:

1. Open the login URL
2. Log in to Kite
3. Capture the `request_token` from the redirect URL
4. Exchange `request_token + api_secret` for an `access_token`
5. Store the `access_token` in secrets or session state

## Recommended Streamlit secrets

Create `.streamlit/secrets.toml`:

```toml
KITE_API_KEY = "your_api_key"
KITE_API_SECRET = "your_api_secret"
KITE_ACCESS_TOKEN = "your_access_token_if_already_generated"
```

## Folder structure

```text
stock-intraday-live/
├── app.py
├── requirements.txt
├── README.md
└── .streamlit/
    └── secrets.toml
```

## Installation

```bash
pip install -r requirements.txt
```

If you want LightGBM locally:

```bash
pip install lightgbm
```

## Run locally

```bash
streamlit run app.py
```

## Live usage flow

1. Put your Kite API key and secret in Streamlit secrets.
2. Open the app.
3. Generate an access token using the request token from the Kite redirect URL.
4. Start the live feed.
5. Keep the app in PAPER mode first.
6. Only then switch to LIVE and enable auto-execution.

## Notes

- PAPER mode simulates fills locally.
- LIVE mode sends real orders through Kite Connect.
- The app uses a persistent live stream when enabled.
- The order log is written to `trading_logs/orders.jsonl`.

## Suggested safe defaults

- Mode: PAPER
- Candle interval: 5m or 15m
- Future move threshold: 0.35%
- Min confidence: 0.60
- Max quantity: 1
- Auto-execute: OFF
