# GitHub Copilot / AI agent instructions for this repo ✅

## Quick facts
- Purpose: Crypto analysis dashboards and datasets (Power BI-focused). Key outputs are reports, DAX measures, and cleaned CSVs.
- Main folders: `raw_data/` (raw API pulls + images), `clean_data/` (DAX/measures + processed data), top-level `README.md` documents project goals.
- Primary data source: CoinGecko API. Example URL in `raw_data/api.md`:
  `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&price_change_percentage=24h,7d`

---

## What matters for automation or code suggestions 🔧
- This repo currently contains documentation, API reference, and dashboard images — **no build, test, or CI scripts exist**. When adding code, also add simple test/validation and a README describing the script.
- Data workflow conventions (follow these exactly):
  - Raw API captures go into `raw_data/` as timestamped files (JSON preferred): e.g. `raw_data/coins-20260106-153000.json`. Add a `raw_data/README.md` describing capture time and parameters.
  - Cleaned outputs and DAX docs go into `clean_data/` (example: `clean_data/desc.md` contains measure names and DAX snippets).
  - Keep filenames and columns in snake_case (e.g., `price_change_percentage_24h`).

## Ingestion pattern (example)
- Use the CoinGecko API parameters shown in `raw_data/api.md`. Handle pagination (increment `page=`) and respect rate limits (sleep between requests).
- Minimal Python snippet (example to follow when generating code):

```py
# use requests, handle pagination, save raw JSON with timestamp
url = "https://api.coingecko.com/api/v3/coins/markets"
params = {"vs_currency":"usd","order":"market_cap_desc","per_page":100,"price_change_percentage":"24h,7d","page":1}
# loop pages, sleep between calls, save `raw_data/coins-<timestamp>.json`
```

## Data/column expectations (use these names exactly if possible)
- `current_price`, `market_cap`, `total_volume`, `price_change_percentage_24h`, `price_change_percentage_7d`, `id`, `symbol`, `name`, `last_updated`.
- Keep DAX measure names and explanations in `clean_data/desc.md` when adding or modifying measures.

## Reports & artifacts
- Power BI reports are referenced in `README.md` but not present; prefer adding `.pbix` files under a `reports/` or `Reports/` directory and include a short `reports/README.md` describing which PBIX version produced which exported images.
- If repo size is a concern, check in a `reports/manifest.md` and upload `.pbix` as release assets instead.

## Testing, validation & PR guidance ✅
- If adding scripts: include a `tests/` folder with pytest-based unit tests for transformation logic and a small sample fixture in `raw_data/sample.json`.
- PRs should include: short title with prefix (`[data]`, `[report]`, `[docs]`), description of data sources/parameters used, and screenshots when dashboards change.

## AI-agent specific rules (short, actionable) 🤖
- Always cite the exact API URL and parameters from `raw_data/api.md` when creating ingestion code.
- Do not invent DAX measures—refer to `clean_data/desc.md` for naming and intent. If a new measure is needed, add it to `clean_data/desc.md` and include an example formula.
- If you propose a structural change (new folder, new naming convention), add a short migration note in `README.md` and include a script to migrate or rename files.
- Avoid editing images in `raw_data/` in-place; instead add new exports and keep the original files for traceability.

## Known gaps / suggestions (documented)
- No existing tests or automation scripts — prioritize adding a small `scripts/` ingestion script and basic tests.
- `Reports/` and `result/` are described in `README.md` but not present — add these if you introduce report files or final outputs.

---

If any of these conventions are unclear or you'd like examples for a specific task (e.g., ingestion script, a DAX measure, or a unit test), tell me which and I'll add a short example or a starter script. ✨