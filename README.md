# Stock Market Analysis and Prediction Engine

This project is a sophisticated Python-based engine for stock market analysis and prediction. It leverages financial data from Alpha Vantage and news sentiment from Bloomberg (via a local terminal) to generate insights, predictions, and trading recommendations. The system employs a variety of quantitative finance techniques, including technical analysis, machine learning models (LSTM, DQN), and statistical modeling.

## Functionality

The core functionality of this project revolves around the `main123.py` script, which performs the following key operations:

*   **Data Ingestion:**
    *   Fetches historical stock data (daily time series, company overview, global quotes) using the Alpha Vantage API (via `alpha_vantge_client.py`).
    *   Retrieves normalized news sentiment for specified stock tickers using the Bloomberg API (via `bloomberg.py` and a local Bloomberg Terminal connection).
*   **Quantitative Analysis:**
    *   Calculates a proprietary "Sigma" score, a key metric driving trading recommendations.
    *   Computes a wide array of technical indicators, including RSI, MACD, SMAs, Bollinger Bands, and more.
    *   Determines market characteristics such as Hurst exponent (for trend vs. mean reversion), mean reversion half-life, volatility regimes, and overall market regimes.
    *   Performs drawdown analysis to assess risk.
*   **Machine Learning & Prediction:**
    *   Utilizes LSTM (Long Short-Term Memory) neural networks for tasks like volatility prediction.
    *   Employs DQN (Deep Q-Network) agents for generating trading recommendations.
    *   Generates price predictions for 30-day and 60-day horizons, complete with confidence bands derived from Monte Carlo simulations.
*   **Output & Visualization:**
    *   Saves detailed analysis reports for each stock to `STOCK_ANALYSIS_RESULTS.txt`.
    *   Generates and saves prediction charts as PNG images (e.g., `AAPL_prediction_20250324_222133.png`) in the root directory (or a `prediction_plots` directory, though some plotting code might be configured for the root). These charts visualize historical prices along with forecasted trends and confidence intervals.

The `advanced_quant_functions_backup.py` file contains a comprehensive suite of advanced quantitative tools, suggesting capabilities or past explorations in areas like:
*   Statistical Arbitrage and Pair Trading
*   Time Series Decomposition (SSA, EMD, HHT)
*   Advanced Momentum Indicators (Adaptive RSI, FRAMA)
*   Alternative Machine Learning Models (XGBoost, Random Forest, Gaussian Processes)
*   Sentiment Analysis from various (mocked) alternative data sources
*   Market Microstructure Analysis (simulated)
*   Multi-Fractal Analysis, Tail Risk (Extreme Value Theory), Wavelet Analysis, and Bayesian Regime Detection.
*   Option pricing via Black-Scholes.

## Repository Structure

*   `main123.py`: The main executable script that drives the analysis and prediction.
*   `alpha_vantge_client.py`: Client script for interacting with the Alpha Vantage API.
*   `bloomberg.py`: Script for fetching news sentiment from a Bloomberg Terminal.
*   `advanced_quant_functions_backup.py`: A backup file containing a wide array of advanced quantitative finance functions.
*   `config.yml`: Appears to be a Cloudflare Tunnel configuration file, possibly for exposing a web interface (e.g., `www.quantpulse.org` mentioned in the file).
*   `STOCK_ANALYSIS_RESULTS.txt`: Text file where detailed analysis outputs for each processed stock are stored.
*   `*.png`: Image files (e.g., `AAPL_prediction_20250324_222133.png`) representing stock prediction charts. These typically show historical prices, forecasted mean paths, and confidence bands.
*   `prediction_plots/`: (Potentially) A directory where prediction plots are saved.

## How to Use

1.  **Prerequisites:**
    *   Ensure all dependencies listed below are installed.
    *   A valid Alpha Vantage API key is required. The script `main123.py` currently has a hardcoded key. You should replace it with your own:
        ```python
        ALPHA_VANTAGE_API_KEY = "YOUR_API_KEY"
        ```
    *   For news sentiment analysis, a Bloomberg Terminal must be running locally and accessible via the Bloomberg API. If not available, sentiment fetching will be skipped or default values will be used.

2.  **Running the Analysis:**
    *   The script `main123.py` can be run directly.
    *   **Interactive Mode:** If run without command-line arguments, it enters an interactive mode:
        ```bash
        python main123.py
        ```
        You will be prompted to:
        *   Analyze a specific stock by entering its ticker symbol.
        *   Search for stock symbols by keywords.
    *   **Direct Analysis Mode:** To analyze a specific stock directly, pass its symbol as a command-line argument:
        ```bash
        python main123.py YOUR_STOCK_SYMBOL
        ```
        For example:
        ```bash
        python main123.py AAPL
        ```

3.  **Output:**
    *   Analysis results will be appended to `STOCK_ANALYSIS_RESULTS.txt`.
    *   Prediction charts (PNG images) will be saved in the root directory or a `prediction_plots` subdirectory.

## Dependencies

The project relies on several Python libraries. You can typically install them using `pip`:

*   `requests`
*   `pandas`
*   `numpy`
*   `matplotlib`
*   `scikit-learn`
*   `hmmlearn`
*   `scipy`
*   `tensorflow` (includes `keras`)
*   `blpapi` (Bloomberg API - requires separate installation and Bloomberg Terminal access)
*   `certifi`
*   `urllib3`

The `advanced_quant_functions_backup.py` file suggests potential use of these additional libraries. If you intend to use functions from this backup file, you might need:

*   `talib-binary` (for TA-Lib)
*   `EMD-signal` (for PyEMD)
*   `PyWavelets`
*   `statsmodels`
*   `xgboost`
*   `pykalman`
*   `prophet`
*   `arch`
*   `empyrical`
*   `joblib`

Installation command for common dependencies:
```bash
pip install requests pandas numpy matplotlib scikit-learn hmmlearn scipy tensorflow blpapi certifi urllib3
```
For TA-Lib, installation can be more complex. Refer to the official TA-Lib documentation. One common way is:
```bash
pip install talib-binary
```

## Disclaimer
Stock market trading involves significant risk. This project is for educational and informational purposes only and should not be considered financial advice. Any predictions or recommendations generated by this tool are not guaranteed to be accurate, and you should consult with a qualified financial advisor before making any investment decisions.