# Binance-Internal-Arbitrage-Trading-System Bot (Python Only)

## 📌 Overview

This agent implements a **Binance Internal Arbitrage Trading System** in pure Python.
It detects and executes arbitrage opportunities within Binance’s ecosystem (spot and futures markets).
It is designed with **safety-first principles**, testnet-first development, and strict Binance API compliance.

👉 No Docker or containerization required — runs as plain Python scripts.

---

## ⚡ Capabilities

* Detect **triangular arbitrage** (A → B → C → A).
* Detect **cross-pair inefficiencies** (spot vs futures spreads).
* Real-time **order book monitoring** via WebSocket (with REST fallback).
* Configurable **profit thresholds, fees, slippage estimates, trade size**.
* Execute trades on **Binance Testnet** (default) or **Mainnet** (requires explicit unlock).
* Historical **backtesting support**.

---

## 🛠️ Modes

* **Backtest** → Run historical data for profitability analysis.
* **Paper (Testnet)** → Risk-free simulation on Binance Testnet.
* **Live** → Real trades on Binance (locked by default, requires manual unlock).

---

## 🔒 Risk Controls

* Max trade size per order.
* Daily/Hourly loss caps.
* Circuit breaker after repeated failures.
* Manual **kill switch** (CLI or config).
* **Two-step unlock** for live trading.

---

## 📂 Architecture (Python-Only)

```
binance_arbitrage/
├─ main.py          # CLI entry point
├─ config.py        # Config loader (pydantic)
├─ market_data.py   # WebSocket + REST handlers
├─ strategy.py      # Arbitrage strategy logic
├─ execution.py     # Order placement + handling
├─ risk.py          # Risk checks & circuit breakers
├─ backtest.py      # Backtesting with historical data
├─ utils.py         # Helper functions
└─ tests/           # Unit + integration tests
```

---

## ⚙️ Configuration

The bot uses **YAML** for strategy settings and **environment variables** for credentials.

**Example config file (`config.yaml`):**

```yaml
mode: paper
symbols: [BTCUSDT, ETHUSDT, BNBUSDT]
max_trade_size: 100
min_profit_pct: 0.3
fee_pct: 0.1
slippage_estimate: 0.05
```

**Environment variables:**

```bash
export BINANCE_API_KEY="your_api_key_here"
export BINANCE_API_SECRET="your_secret_here"
```

---

## 🛡️ Safety

* API keys **never stored in code** (only environment variables).
* Withdrawals disabled on API keys.
* **Testnet-first**, Mainnet only after human confirmation.
* Logging avoids exposing secrets.

---

## 📦 Deliverables

* Full **Python source code** (no Docker).
* Strategy **unit tests**.
* Integration tests on Binance Testnet.
* Backtesting framework with sample data.
* Structured logs + error handling.
* Setup guide.

---

## 🚀 Example Commands

**Run in Testnet mode:**

```bash
python main.py --mode paper --symbols BTCUSDT,ETHUSDT
```

**Run a backtest:**

```bash
python backtest.py --symbols BTCUSDT,ETHUSDT --data ./data/history.json
```

---

## 📚 References

* [Binance API Docs](https://binance-docs.github.io/apidocs/)
* [Binance Connector Python](https://github.com/binance/binance-connector-python)
* [Binance Testnet](https://testnet.binance.vision/)
