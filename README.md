# Crypto Analysis

Short project description

A lightweight project for analyzing cryptocurrency market metrics (price changes, market capitalization, and momentum scoring) and producing Power BI dashboards and cleaned datasets for visual analysis.

## Table of Contents
- [Introduction](#introduction)
- [Dataset / Inputs](#dataset--inputs)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Analysis / Features](#analysis--features)
- [Results / Outputs](#results--outputs)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Introduction

This repository contains raw captures, cleaned outputs, and documentation used to build Power BI dashboards that analyze cryptocurrency market behavior. The focus is on reproducible ingestion of CoinGecko market data, consistent cleaning, and storing DAX measures and documentation alongside visual artifacts.

## Dataset / Inputs

- Primary data source: CoinGecko Markets API (example):

  `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&price_change_percentage=24h,7d`

- Conventions:
  - Raw API captures should be saved under `raw_data/` as timestamped JSON files (e.g., `raw_data/coins-20260106-153000.json`).
  - Cleaned datasets, DAX measure descriptions and formulas live under `clean_data/` (see `clean_data/desc.md`).
  - Use snake_case for filenames and column names (e.g., `price_change_percentage_24h`).

## Tech Stack

- Power BI Desktop (reports / dashboards)
- Python (recommended for ingestion and cleaning scripts)
- JSON, CSV for dataset interchange

## Installation

1. Install Power BI Desktop to view/edit reports.
2. If you add or use ingestion scripts:
   - Python 3.8+ recommended
   - Create a virtual environment and install dependencies from `requirements.txt` (if present):

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

## Usage

- To collect raw data, use the CoinGecko API and save responses to `raw_data/` with timestamped filenames.

Python (minimal example):

```py
import requests, time, json
url = "https://api.coingecko.com/api/v3/coins/markets"
params = {"vs_currency":"usd","order":"market_cap_desc","per_page":100,"price_change_percentage":"24h,7d","page":1}
resp = requests.get(url, params=params)
if resp.ok:
    filename = f"raw_data/coins-{int(time.time())}.json"
    with open(filename, 'w', encoding='utf-8') as f:
        json.dump(resp.json(), f, ensure_ascii=False, indent=2)
```

- When adding scripts, include tests (pytest) and a small sample `raw_data/sample.json` fixture for CI tests.

## Analysis / Features

- Momentum scoring and ranking
- Price change percentage analysis (24h, 7d)
- Market capitalization trends and ranking
- DAX measures and calculations documented in `clean_data/desc.md`

## Results / Outputs

- Primary outputs are Power BI `.pbix` reports (add them under `reports/` if included) and cleaned CSV/JSON datasets in `clean_data/`.
- If repository size is a concern, prefer adding a `reports/manifest.md` and attach `.pbix` files as release assets.

## Project Structure

- `raw_data/` — raw API captures and images
- `clean_data/` — cleaned outputs and `desc.md` with measure documentation
- `.github/` — repo and agent instructions (includes `copilot-instructions.md`)
- `README.md`, `LICENSE`

## Contributing

- Follow existing conventions (timestamped raw captures, snake_case, store DAX in `clean_data/desc.md`).
- PRs should have a short title with a prefix: `[data]`, `[report]`, `[docs]` and include a brief description of data source/parameters used.
- Include tests for any transformation logic and a small sample fixture under `raw_data/`.

## License

See the `LICENSE` file for license details.

## Contact

Open an issue or submit a PR with questions or fixes. If you'd like, include a short note describing the change and the data used for testing.

Email: vermaadarsh666@gamil.com
