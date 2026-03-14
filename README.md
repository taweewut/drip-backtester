# DRIP Backtester — Dividend vs Growth

A lightweight single-page web app for comparing two assets using a simplified **DRIP (Dividend Reinvestment Plan)** backtest.

It is designed for side-by-side analysis of:

- **Dividend ETFs** and **Dividend Growth ETFs**
- **Growth ETFs** and **Growth Stocks**
- **Dividend Stocks** vs **Growth Stocks**
- **Lump sum + monthly DCA** investing scenarios

The app runs entirely in the browser and can be published easily with **GitHub Pages**.

---

## Features

- Compare **two tickers** side by side
- Simulate:
  - **Initial lump sum investment**
  - **Monthly DCA contributions**
  - **Annual dividend reinvestment (DRIP-style)**
- View results as:
  - **Final real portfolio value**
  - **Inflation-adjusted annualized summary**
  - **Annual gain / loss chart**
  - **Year-by-year breakdown table**
- Built-in ticker library for:
  - Dividend ETFs
  - Dividend Growth ETFs
  - Growth ETFs
  - REIT ETFs
  - Dividend Stocks
  - Growth Stocks
- Add your own custom tickers from the UI
- Save custom tickers in browser `localStorage`
- Import / export custom ticker libraries as JSON
- Includes a built-in guide for manually extending ticker data in code

---

## Demo use case

This project is especially useful for exploring questions like:

- How does **SCHD** compare with **QQQ** over the last 10 years?
- Does **dividend growth** outperform pure **growth** after inflation?
- What happens when you combine **lump sum investing** with **monthly DCA**?
- How much does **dividend reinvestment** contribute to long-term compounding?

---

## Project structure

```text
.
├── index.html    # Main app (HTML + CSS + JavaScript in one file)
└── README.md
```

This project is intentionally simple and self-contained, so it can be hosted as a static site without any build step.

---

## How it works

The backtester uses annual data for each ticker:

- `p` = annual **price return** as decimal
- `d` = annual **dividend yield** as decimal

Example:

```js
"VTI": {
  name: "Vanguard Total Market",
  cat: "Blend ETF",
  data: {
    2020: { p: 0.212, d: 0.016 },
    2021: { p: 0.255, d: 0.013 }
  }
}
```

### Simulation assumptions

For each year, the model:

1. Adds half of the yearly DCA contributions
2. Applies annual price return
3. Applies annual dividend yield
4. Adds the remaining half of yearly DCA contributions
5. Adjusts portfolio values using CPI inflation data

This makes the app useful for **high-level comparison**, especially between dividend-oriented and growth-oriented assets.

---

## Important limitations

This is a **simplified educational backtester**, not a professional portfolio accounting engine.

### What it does well

- Style comparison: **Dividend vs Growth**
- Long-term compounding intuition
- Inflation-aware comparison
- Relative comparison between two assets

### What it does not model precisely

- Exact dividend payment dates
- Share-level tracking
- Tax effects
- Fund expense ratios
- Transaction fees / slippage
- Monthly or daily total return path
- IRR / XIRR cash-flow analysis

### Note on annualized return

The app shows an annualized growth figure, but because the simulation includes ongoing monthly contributions, that figure should be treated as a **simple reference metric**, not a strict money-weighted return.

---

## Run locally

Because this is a static HTML app, you can open it directly in a browser.

### Option 1: Open file directly

Open `index.html` in your browser.

### Option 2: Use a local server

Useful if you want a cleaner dev workflow.

Python:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

---

## Publish with GitHub Pages

### 1. Create a GitHub repository

Example repository name:

```text
drip-backtester
```

### 2. Push the project files

At minimum:

- `index.html`
- `README.md`

### 3. Enable GitHub Pages

In your repository:

- Go to **Settings**
- Open **Pages**
- Under **Build and deployment**, choose:
  - **Source** → `Deploy from a branch`
  - **Branch** → `main` (or `master`)
  - **Folder** → `/ (root)`

### 4. Save and wait for deployment

GitHub will generate a public URL such as:

```text
https://your-username.github.io/drip-backtester/
```

---

## Adding custom tickers

You can add custom tickers in two ways.

### Method 1: From the app UI

Use the **Manage Tickers** tab to:

- Enter ticker symbol
- Enter full name
- Select category
- Fill in annual price return and dividend yield data
- Save to browser storage

### Method 2: Edit the code directly

Inside `index.html`, update the `BASE_TICKERS` object.

Format:

```js
"SYMBOL": {
  name: "Asset Name",
  cat: "Category",
  data: {
    2020: { p: 0.10, d: 0.03 },
    2021: { p: -0.05, d: 0.032 },
    2022: { p: 0.12, d: 0.031 }
  }
}
```

### Data entry rules

- Use **decimals**, not percent strings
- `12.5%` → `0.125`
- `3.2%` → `0.032`
- `-4.5%` → `-0.045`
- For non-dividend assets, use `d: 0`

---

## Suggested data sources

The app currently assumes manually verified annual data.

Examples mentioned in the app:

- Macrotrends annual return history
- Macrotrends dividend yield history

Before entering data, make sure you are consistent about whether the value is:

- **price return**, or
- **total return**

To avoid double counting dividends, the `p` field should represent **price return**, while `d` should represent **dividend yield**.

---

## Built with

- HTML5
- CSS3
- Vanilla JavaScript
- Chart.js for chart rendering
- Google Fonts (`Syne`, `DM Mono`)

---

## Roadmap ideas

Possible future improvements:

- Share-level DRIP tracking
- Monthly total return simulation
- IRR / XIRR calculation
- Risk metrics:
  - Max drawdown
  - Volatility
  - Best / worst year
- Benchmark comparison mode
- CSV import for ticker data
- More complete historical database
- Dark / light theme toggle

---

## License

You can choose your preferred license for this repository.

Common options:

- MIT License
- Apache-2.0
- GPL-3.0

If you want a simple permissive choice for GitHub, **MIT** is a common option.

---

## Disclaimer

This project is for **educational and research purposes only**.
It does not constitute investment advice, financial advice, tax advice, or a recommendation to buy or sell any security.

Always verify historical data independently before relying on results.
