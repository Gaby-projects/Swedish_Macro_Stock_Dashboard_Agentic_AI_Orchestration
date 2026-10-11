# 📈 Swedish Macroeconomic Indicators & Stock Market Dashboard 🏛️

![API](https://img.shields.io/badge/API-6A1B9A?style=for-the-badge)
![Live Dashboard - STREAMLIT](https://img.shields.io/badge/Live_Dashboard-STREAMLIT-1F4E79?labelColor=1F4E79&style=for-the-badge)
![Agent AI Orchestration](https://img.shields.io/badge/Agent_Orchestration-2E7D32?style=for-the-badge)

A Streamlit dashboard that puts Sweden's main economic indicators (Riksbank API) next to selected Stockholm stocks (Yahoo Finance API). I built it with a team of seven Claude Code subagents. Ideal for anyone who wants a quick overview of how the Swedish economy is doing and how the stock market is trending.

## 🔗 Live dashboard

https://macro-micro-indicators.streamlit.app/

*The first load can take a few seconds while the latest data downloads, or up to a minute if the app has been asleep.*

## ✨ Features

- 7 macroeconomic indicators from the Riksbank (Sweden's central bank), such as GDP, inflation and the policy rate, with latest value, history sparkline and optional forecasts.
- 19 Stockholm stocks in 8 sectors, with returns, rebased price charts and sector indices.
- Macro × Market view: any macro indicator against any stock or sector on one chart, to see how an industry moves with the economy.
- Reliable data: retries, schema validation and snapshot fallback, with a freshness badge per source.
- Fixtures mode: runs offline with sample data.

## 🤖 How it was built

Seven specialised [Claude Code subagents](https://code.claude.com/docs/en/sub-agents), defined in [`.claude/agents/`](.claude/agents/), each owning its own files. [`CLAUDE.md`](CLAUDE.md) is the shared ground truth they all read.

| Subagent | Role |
|---|---|
| `pm-plan` | Product manager: spec and task list |
| `riksbank-data-expert` | Riksbank API client and macro transforms |
| `yahoo-data-expert` | Yahoo Finance API client and market transforms |
| `viz-ux-designer` | UX and chart design |
| `macro-market-expert` | Aligns monthly/quarterly macro data with daily prices |
| `streamlit-builder` | Builds the app |
| `verifier` | QA gate: tests and app boot after every step |

## 🛠️ Tech stack

- [Python](https://www.python.org/) & [pandas](https://pandas.pydata.org/) – data analysis
- [Streamlit](https://streamlit.io/) – interactive dashboard
- [Plotly](https://plotly.com/python/) – interactive charts
- [Riksbank API](https://developer.api.riksbank.se/) – Swedish macroeconomic data
- [Yahoo Finance](https://finance.yahoo.com/) – Stockholm stock prices
- [Claude Code subagents](https://code.claude.com/docs/en/sub-agents) – team of AI agents that built the app


## 📁 Project structure

- `app.py` — Streamlit entry point
- `src/swedish_macro_dashboard/data/` — API clients, schema, sample data
- `src/swedish_macro_dashboard/transforms/` — macro, market and overlay transforms
- `src/swedish_macro_dashboard/tabs/` — dashboard tabs
- `tests/` — pytest suite
- `docs/` — spec, UI plan and chart specs
- `.claude/agents/` — subagent definitions

## ⚡ Run locally

Requirements: [uv](https://docs.astral.sh/uv/) (installs Python and all dependencies).

```bash
uv sync
uv run python -m streamlit run app.py
```

No API keys needed. To run without internet, turn on **Fixtures mode** in the sidebar.
