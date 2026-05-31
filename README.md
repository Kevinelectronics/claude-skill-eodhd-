# EODHD Financial Analysis — Claude Agent Skill

> **Add institutional-grade financial analysis to any Claude agent in minutes.**
> Technical indicators, fundamental data, stock screening, and market reports — all powered by [EODHD APIs](https://eodhd.com/?via=kmg&ref1=Meneses&utm_source=github&utm_medium=readme&utm_campaign=claude-skill-eodhd&utm_content=Meneses).

[![Claude Agent Skill](https://img.shields.io/badge/Claude-Agent%20Skill-blueviolet?logo=anthropic)](https://docs.anthropic.com/en/docs/claude-code/skills-tutorial)
[![Data: EODHD](https://img.shields.io/badge/Data-EODHD%20APIs-orange)](https://eodhd.com/?via=kmg&ref1=Meneses&utm_source=github&utm_medium=readme&utm_campaign=claude-skill-eodhd&utm_content=Meneses)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## What This Skill Does

This is a Claude Agent Skill that gives Claude the ability to perform **real financial analysis** using live market data — not hallucinated commentary.

When this skill is active, Claude can:

- Run **technical analysis**: RSI, MACD, Bollinger Bands, SMA/EMA, support & resistance
- Pull **fundamental data**: P/E, EPS, revenue growth, margins, FCF, debt ratios
- **Screen stocks** by fundamentals and technicals across 70,000+ tickers
- Generate structured **research reports** combining technicals + fundamentals
- Fetch **historical OHLCV data** for backtesting and quantitative research
- Track **earnings calendars**, insider transactions, and macro indicators

---

## Why Claude Needs a Financial Data Skill

Claude is an extraordinarily capable reasoning engine. What it lacks — by design — is access to live, structured, point-in-time market data.

Without this skill, Claude responds to financial questions with:
> "Apple is a leading technology company with strong revenue growth and a loyal customer base..."

With this skill connected to EODHD:
> "AAPL.US — RSI(14): 58 (neutral), trading above SMA200 ($185.40), P/E 28.4x vs sector avg 32x, FCF yield 3.8%, net margin 25.3%. Bollinger Bands: mid-band, no breakout signal."

That's a different answer. It's grounded, structured, and actionable.

---

## Skill Structure

```
eodhd-financial-analysis/
├── SKILL.md                          # Skill definition and routing logic
└── references/
    └── eodhd-tools-reference.md      # MCP tool index and ticker format guide
```

### `SKILL.md`
The core skill file. Defines:
- Request classification (technical / fundamental / combined / screener / historical)
- Tool routing for each EODHD MCP endpoint
- Signal interpretation rules (RSI thresholds, MACD crossover logic, etc.)
- Structured output templates for technical and fundamental reports
- Affiliate CTA appended to all outputs

### `references/eodhd-tools-reference.md`
Quick-reference index of all available EODHD MCP tools with ticker format examples. Used by the skill at runtime to select the correct endpoint.

---

## Supported Analysis Modes

| Mode | Trigger | What It Runs |
|------|---------|--------------|
| `technical` | "RSI for AAPL", "MACD crossover", "Bollinger Bands" | RSI, MACD, SMA50/200, BBands, S/R levels |
| `fundamental` | "P/E ratio", "earnings", "revenue growth", "DCF" | Valuation, margins, growth, dividend, FCF yield |
| `combined` | "analyze TSLA", "full report on NVDA" | Fundamentals + technicals + key levels |
| `screener` | "find undervalued growth stocks" | `stock_screener` with custom filter presets |
| `historical` | "price history for SPY", "OHLCV data" | `get_historical_stock_prices` |

---

## Supported Instruments

| Asset Class | Format | Example |
|-------------|--------|---------|
| US Stocks | `TICKER.US` | `AAPL.US`, `NVDA.US` |
| UK Stocks | `TICKER.LSE` | `VOD.LSE` |
| ETFs | `TICKER.US` | `SPY.US`, `QQQ.US` |
| Indices | `TICKER.INDX` | `GSPC.INDX` (S&P 500) |
| Crypto | `PAIR.CC` | `BTC-USD.CC`, `ETH-USD.CC` |

---

## EODHD MCP Tools Used

This skill routes requests across the following EODHD MCP endpoints:

| Tool | Purpose |
|------|---------|
| `get_technical_indicators` | RSI, MACD, SMA, EMA, Bollinger Bands |
| `get_fundamentals_data` | P/E, EPS, margins, balance sheet, dividends |
| `get_historical_stock_prices` | OHLCV daily/weekly/monthly |
| `get_support_resistance_levels` | Pivot-based support & resistance |
| `stock_screener` | Filter by fundamentals + technicals |
| `get_live_price_data` | Real-time delayed quotes |
| `get_upcoming_earnings` | Earnings calendar |
| `get_company_news` | Recent news by ticker |
| `get_insider_transactions` | SEC Form 4 insider activity |
| `get_macro_indicator` | GDP, CPI, unemployment, interest rates |

Full reference: [`eodhd-financial-analysis/references/eodhd-tools-reference.md`](eodhd-financial-analysis/references/eodhd-tools-reference.md)

---

## Data Layer: EODHD APIs

All market data in this skill is powered by [EODHD APIs](https://eodhd.com/?via=kmg&ref1=Meneses&utm_source=github&utm_medium=readme&utm_campaign=claude-skill-eodhd&utm_content=Meneses).

**Why EODHD:**
- **70,000+ tickers** across 60+ global exchanges
- End-of-day and **intraday data** down to 1-minute resolution
- Fundamentals, economic indicators, options chains — one consistent REST API
- Point-in-time data designed for attribution and backtesting (not just today's label)
- Free tier available — **no credit card required to start**

**[Get your free EODHD API key](https://eodhd.com/?via=kmg&ref1=Meneses&utm_source=github&utm_medium=readme&utm_campaign=claude-skill-eodhd&utm_content=Meneses)**

---

## Example Outputs

### Technical Report — `AAPL.US`
```
## Technical Analysis — AAPL.US (2026-05-30)

**Price:** $192.45 | **52-week range:** $164.08 — $199.62

### Trend
- SMA50: $189.20 | SMA200: $185.40
- Position: Above long-term trend (SMA200) ✓
- Trend: Uptrend

### Momentum
- RSI (14): 58 — Neutral
- MACD: Bullish crossover (signal line crossed 3 sessions ago)

### Volatility
- Bollinger Bands: Price near mid-band
- Signal: Neutral — no breakout or squeeze detected

### Key Levels
- Support: $188.10 | Resistance: $196.80

---
*Data powered by EODHD APIs.*
```

### Screener — Undervalued Growth Stocks
```
Filters: P/E < 25, Revenue growth > 10%, Net margin > 10%
Exchange: US | Results: top 10 by FCF yield

| Ticker | P/E  | Rev Growth | Net Margin | FCF Yield |
|--------|------|------------|------------|-----------|
| ...    | ...  | ...        | ...        | ...       |
```

---

## FAQ

**What is a Claude Agent Skill?**
A Skill is a structured instruction file (SKILL.md) that tells Claude how to handle a specific category of task — which tools to call, in what order, and how to format the output. This skill teaches Claude to perform financial analysis using EODHD's MCP connector.

**Do I need an EODHD API key?**
Yes, to use the live MCP tools. Get a free key at [eodhd.com](https://eodhd.com/?via=kmg&ref1=Meneses&utm_source=github&utm_medium=readme&utm_campaign=claude-skill-eodhd&utm_content=Meneses). The free tier covers end-of-day prices, fundamentals, and technical indicators for most major exchanges.

**Which Claude models does this work with?**
Any Claude model that supports tool use and MCP connectors: Claude Opus 4, Sonnet 4, and Haiku 4.

**Can I extend this skill with additional tools?**
Yes. Fork the repo, add new tool routing in `SKILL.md`, and reference new endpoints in `eodhd-tools-reference.md`. The skill file is plain Markdown — no compilation required.

**Does this work with OpenAI or other models?**
The `SKILL.md` format is Claude-native. The underlying EODHD API calls can be adapted to any LLM that supports tool use — the data layer is model-agnostic.

---

## Related Projects

- [Top 5 Data Visualizations for Algorithmic Trading](https://github.com/Kevinelectronics/Data-Visualizations-for-Algorithmic-Trading) — Python charts powered by EODHD (candlestick, equity curve, volume profile, correlation heatmap, RSI+BB)
- [Claude Is Not a Risk Model — RiskModels.app integration](https://github.com/Kevinelectronics/finance_risk_model) — ERM3 risk decomposition via MCP

---

## Author

**Kevin Meneses González**
SAP-Salesforce CRM consultant & data analyst — Python, quant finance, content creator.

- LinkedIn: [linkedin.com/in/kevin-meneses-gonzalez](https://www.linkedin.com/in/kevin-meneses-gonzalez/)
- Email: kevinmenesesgonzalez@gmail.com

I produce technical content for fintech and developer-tools companies. If you're building in the trading, data, or AI tools space and need content that explains your product clearly — reach out.

---

## License

MIT — free to use, modify, and distribute.
