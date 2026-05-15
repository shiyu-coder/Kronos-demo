# Kronos Demo

A demo webpage for **Kronos: A Foundation Model for the Language of Financial Markets**. This repository turns the Kronos forecasting pipeline into a lightweight BTC/USDT dashboard with live probability metrics, a 24-hour forecast chart, and a static site you can publish directly with GitHub Pages or any simple web host.

## Table of Contents
- [What this repo shows](#what-this-repo-shows)
- [Project structure](#project-structure)
- [How it works](#how-it-works)
- [Run locally](#run-locally)
- [Refresh predictions](#refresh-predictions)
- [Assets](#assets)
- [Related project](#related-project)

## What this repo shows
- A browser-based dashboard for **BTC/USDT live probabilistic forecasting**
- A simple presentation layer for the upstream [Kronos](https://github.com/shiyu-coder/Kronos) model
- Model outputs such as **upside probability**, **volatility amplification**, and a **24-hour forecast range**
- A repo structure that is easy to host, inspect, and extend

## Project structure
```text
.
├── index.html              # Dashboard layout and explanatory copy
├── style.css               # Visual styles for cards, sections, and charts
├── update_predictions.py   # Fetches Binance data, runs Kronos, renders outputs
├── prediction_chart.png    # Latest generated forecast chart
├── img/                    # Static images and branding assets
└── model/                  # Local model helpers imported by the update script
```

## How it works
1. `update_predictions.py` downloads recent Binance market data for `BTCUSDT` on the 1-hour interval.
2. It loads the Kronos tokenizer and model weights, then runs multiple sampled forecasts.
3. The script computes summary metrics, renders `prediction_chart.png`, and updates the static dashboard content.
4. `index.html` displays the latest chart, timestamp, and forecast explanation for visitors.

## Run locally
### 1) Serve the dashboard
Because this project is a static site, you can preview it with any local HTTP server:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

### 2) Install Python dependencies for forecast refresh
Create a virtual environment and install the packages used by `update_predictions.py`.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install matplotlib numpy pandas torch python-binance
```

You will also need the local Kronos model package referenced by:
- `NeoQuasar/Kronos-Tokenizer-2k`
- `NeoQuasar/Kronos-mini`
- the repository's `model/` helpers

## Refresh predictions
Run the update script from the repository root:

```bash
python3 update_predictions.py
```

The script is configured to:
- use `BTCUSDT`
- read 1-hour candles
- keep 360 historical points
- forecast 24 hours ahead
- generate 30 sampled predictions

After a successful run, the latest chart and dashboard values are written back into the repo files.

## Assets
- `prediction_chart.png` is the primary generated artifact for the live page
- `img/` contains branding and static assets used by the page UI

## Related project
This demo depends on the main Kronos research implementation:
- Upstream model repo: https://github.com/shiyu-coder/Kronos

## Contributing
If you plan to grow this demo, helpful next sections could be deployment notes, scheduled refresh automation, and a small troubleshooting section for model downloads and Binance connectivity.
