# BTC Macro Dashboard

An interactive projection model visualizing Bitcoin's ecosystem from 2022 to 2029 — combining network hashrate, global M2 liquidity, BTC price, and Strategy Inc (MSTR) stock — built as a single self-contained HTML file with no dependencies beyond a CDN-loaded charting library.

![Dashboard Preview](https://img.shields.io/badge/status-live-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue) ![Built with](https://img.shields.io/badge/built%20with-HTML%2FJS%2FChart.js-orange)

---

## What it does

The dashboard lets you explore how four macro variables relate to each other historically and project forward three years using adjustable assumptions:

| Variable | Source basis | Color |
|---|---|---|
| **MSTR stock price** | NAV model: BTC holdings × BTC price × mNAV ÷ shares | Purple |
| **Bitcoin price** | Exponential trend + M2 coupling factor | Amber |
| **Network hashrate** | Historical growth extrapolation | Blue |
| **Global M2 supply** | US + China + Eurozone + Japan in USD | Green |

---

## Model methodology

### Projection engine

All four variables are projected using **exponential trend extrapolation with lognormal confidence intervals**:

```
Base projection:  V(t) = V₀ × (1 + r_quarterly)^t
±1σ band:         V(t) × exp(±σ√t)
±2σ band:         V(t) × exp(±2σ√t)
```

Where `t` is measured in quarters. This gives wider bands at longer horizons, correctly representing compounding uncertainty.

### MSTR stock model

The MSTR price is derived from a **modified Net Asset Value (mNAV)** framework:

```
MSTR price = (BTC holdings × BTC price × mNAV multiple) ÷ shares outstanding
```

Key parameters:
- **Starting point (Mar 2026):** 762,099 BTC, ~340M shares, mNAV ~1.2×, price ~$135
- **BTC accumulation:** New BTC acquired each year via ATM equity and preferred share issuances
- **Share dilution:** Annual dilution rate from ongoing capital raises
- **mNAV trajectory:** Linear interpolation from current ~1.2× to your target by 2029

### M2 → BTC coupling

Bitcoin price is modeled as:

```
Effective BTC growth rate = Base rate + (M2 growth × coupling factor)
```

A coupling factor of 0 means BTC moves independently of liquidity. A factor of 1 means BTC absorbs all M2 growth as additional return. Research suggests a ~60–70 day lag between M2 changes and BTC price movements.

---

## Interactive controls

| Slider | Default | What it models |
|---|---|---|
| BTC annual growth, base | 30% | Structural BTC appreciation trend |
| BTC volatility 1σ | 55% | Width of the uncertainty band |
| Hashrate annual growth | 35% | Mining expansion rate |
| M2 annual growth | 4% | Central bank monetary expansion |
| M2 → BTC coupling | 0.40 | How strongly liquidity drives BTC |
| BTC accumulation / year | 80,000 BTC | Strategy's ongoing buying rate |
| mNAV multiple 2029 | 1.5× | Premium over NAV at end of projection |
| MSTR volatility 1σ | 70% | Width of MSTR uncertainty band |
| Share dilution / year | 12% | Annual equity issuance dilution |

---

## Key data points (March 2026)

- **Strategy BTC holdings:** 762,099 BTC (~3.6% of total supply)
- **Average purchase price:** $75,694 / BTC
- **MSTR current price:** ~$135 (ATH: $543, Nov 2024)
- **Current mNAV:** ~1.2× (peak: ~4× in late 2024)
- **Bitcoin price:** ~$70,000
- **Network hashrate:** ~800–1,082 EH/s
- **Global M2 (US+China+EU+Japan):** ~$100T

---

## Historical context

| Event | Impact |
|---|---|
| May 2020 Bitcoin halving | Block reward: 12.5 → 6.25 BTC |
| China mining ban (Jul 2021) | Hashrate dropped ~50%, recovered within months |
| FTX collapse (Nov 2022) | BTC fell to ~$16K |
| Bitcoin ETF approval (Jan 2024) | Institutional capital inflows accelerated |
| April 2024 halving | Block reward: 6.25 → 3.125 BTC |
| BTC ATH ~$126K (Oct 2025) | MSTR ATH ~$543 (Nov 2024) |

---

## How to use

1. Open `btc_macro_dashboard.html` in any modern browser
2. Select a variable tab (MSTR / BTC / Hashrate / M2 / All)
3. Adjust sliders to match your assumptions
4. Metric cards update in real time showing 2029 base projections and ±1σ ranges

**No internet connection required** after the initial Chart.js CDN load. All logic runs client-side in JavaScript.

---

## Hosting on GitHub Pages

1. Push this repository to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, root folder
4. Your dashboard will be live at `https://yourusername.github.io/btc-macro-dashboard`

---

## Data sources

| Data | Source |
|---|---|
| Bitcoin hashrate | CoinWarz, JPMorgan research |
| Bitcoin price | Bankrate, Fortune, CoinDesk |
| Global M2 | StreetStats (Fed, ECB, PBoC, BoJ) |
| MSTR / Strategy data | CoinDesk, MacroTrends, SEC filings, TradingView |
| mNAV framework | Strategy.com, Tekedia, CCN |

---

## Disclaimer

This dashboard is for **educational and informational purposes only**. It is not financial advice. Projections are illustrative scenarios based on historical trends — not forecasts. Bitcoin and MSTR are highly volatile assets. Past performance does not guarantee future results.

---

## License

MIT — free to use, modify, and distribute.
