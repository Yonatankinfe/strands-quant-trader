# 📈 Strands-Quant-Trader

An advanced, modular algorithmic trading and research engine designed for **tokenized stocks** (via Bybit) and **US Equities** (via `yfinance` fallback). It bridges quantitative analysis, Machine Learning (Gradient Boosting), and Large Language Models (LLMs) to generate trading signals, all wrapped in an institutional-grade risk management and event-driven backtesting framework.

---

## ✨ Key Features

- **Dual Data Providers**: Seamlessly switches between Bybit's tokenized stocks and `yfinance` (real US stock candles as a price proxy) with automatic fallback and geo-block workarounds.
- **Pluggable Decision Engines**:
  - 🧠 **ML Model**: HistGradientBoosting with triple-barrier labeling, purged chronological cross-validation, and probability calibration.
  - 🤖 **LLM Agent**: Local HuggingFace integration (e.g., `Qwen2.5-1.5B-Instruct`) or remote API endpoints.
  - 📏 **Rule-Based**: Deterministic technical indicator scoring.
  - 🎲 **Random Baseline**: For statistical benchmarking and placebo testing.
- **Institutional Risk Management**:
  - ATR-based dynamic Stop-Loss and Take-Profit.
  - Per-symbol and account-level circuit breakers (consecutive losses, daily drawdown limits).
  - Overextension gates (prevents buying tops/selling bottoms).
  - US Regular Session filters and minimum Risk-Reward (R:R) cost hurdles to overcome fees/slippage.
- **Rigorous ML Pipeline**: Chronological purged splits to prevent data leakage, placebo tests, and permutation feature importances.
- **Live Paper Trading**: Event-driven live simulator that triggers on candle closes, manages positions, and persists state to JSON/CSV for seamless resuming.

---

## 📂 Project Structure (Notebook Cells)

The project is designed to run sequentially in a Jupyter Notebook or Google Colab environment:

| Cell(s) | Module | Description |
| :--- | :--- | :--- |
| **1 - 4** | Setup & Config | Installs dependencies, loads API keys from Colab Secrets, and initializes core configurations. |
| **5 - 6** | Data Ingestion | Connects to Bybit or yfinance, validates symbols, and builds the tradable universe. |
| **7 - 8** | Market State | Computes causal technical indicators and builds normalized JSON market snapshots. |
| **9** | Decision Models | Implements the LLM, Rule-Based, and Random deciders. |
| **9b - 9d** | ML Pipeline | Generates triple-barrier labels, trains regularized GBDT models, and evaluates calibration. |
| **10 - 12** | Risk & Engine | Core risk manager, order builder, and event-driven portfolio accounting engine. |
| **13 - 15** | Backtesting | Chronological backtester, performance metrics, and equity curve visualizations. |
| **16 - 17** | Live Trading | Live paper-trading loop with state persistence and result exporting. |
| **18 - 20** | Execution | Runs the universe selection, backtests, ML experiments, and live paper trading. |

---

## 🚀 Installation & Setup

This project is highly optimized for **Google Colab** due to its reliance on Colab Secrets for API keys and optional GPU acceleration for LLM inference.

### 1. Install Dependencies
Run the first cell to install required packages:
```python
!pip install -q -U transformers accelerate yfinance scikit-learn joblib
# Optional: !pip install -q pysocks (if using a SOCKS5 proxy for Bybit)
