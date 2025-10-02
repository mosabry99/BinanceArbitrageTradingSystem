# AGENTS.md

## Binance-Internal-Arbitrage-Trading-System Bot

### Overview
This agent implements a **Binance Internal Arbitrage Trading System** in Python.  
It is designed to detect and execute profitable arbitrage opportunities across Binance markets (spot and futures).  
It prioritizes **safety, backtesting, and compliance with Binance API rate limits**.

---

### Capabilities
- Triangular arbitrage detection (A → B → C → A).
- Cross-pair arbitrage opportunities detection.
- Live order execution on Binance Testnet and Mainnet (after manual approval).
- WebSocket-based orderbook streaming for real-time opportunities.
- Configurable thresholds for minimum profit, maximum trade size, slippage, and fees.
- Backtesting engine for historical data replay and strategy validation.

---

### Modes
- **Backtest**: Replay historical orderbook data and measure profitability.
- **Paper (Testnet)**: Use Binance Testnet for safe live simulations.
- **Live**: Real execution on Binance (disabled by default, requires manual approval).

---

### Risk Controls
- Per-trade maximum notional limit.
- Circuit breaker for consecutive failed trades or high drawdown.
- Daily/hourly max loss thresholds.
- Manual kill switch to immediately stop trading.
- Two-step confirmation required for live trading.

---

### Architecture
```
binance_arbitrage/
├─ src/
│  ├─ bot/
│  │  ├─ main.py          # CLI entry point
│  │  ├─ config.py        # Config loader (pydantic)
│  │  ├─ market_data.py   # WebSocket + REST handlers
│  │  ├─ strategy.py      # Arbitrage strategy logic
│  │  ├─ execution.py     # Trade execution + order handling
│  │  ├─ risk.py          # Risk checks & circuit breakers
│  │  ├─ backtest.py      # Historical data backtesting
│  │  └─ utils.py         # Shared helpers
├─ tests/                 # Unit & integration tests
├─ docker/                # Containerization setup
└─ README.md              # Project documentation
```

---

### Configuration
The bot is configured via a `.yaml` or `.env` file.  
Example config:

```yaml
mode: paper
symbols: [BTCUSDT, ETHUSDT]
max_trade_size: 50
min_profit_pct: 0.2
fee_pct: 0.1
slippage_estimate: 0.05
concurrency: 2
```

Environment variables for Binance API keys:

```bash
BINANCE_API_KEY=your_key_here
BINANCE_API_SECRET=your_secret_here
```

---

### Safety
- API keys stored securely (never committed).
- Logging excludes sensitive information.
- Testnet strongly recommended before enabling live trading.
- Withdrawals disabled on API keys for security.

---

### Deliverables
- Full Python repo scaffold.
- Unit tests for strategy math and backtesting.
- Integration tests with Binance Testnet.
- Dockerfile and docker-compose for containerized runs.
- README with setup instructions and usage examples.
- Prometheus-compatible metrics and structured logs.

---

### Example Commands
Run in testnet mode:

```bash
python -m bot.main --mode paper --symbols BTCUSDT,ETHUSDT
```

Run backtest:

```bash
python -m bot.backtest --symbols BTCUSDT,ETHUSDT --data ./data/history.json
```

---

### References
- [Binance API Documentation](https://developers.binance.com)
- [Binance Connector Python](https://github.com/binance/binance-connector-python)
- [Binance Testnet](https://testnet.binance.vision/)
