# Auto Finance Agent

## Project Summary

Auto Finance Agent is a multi-agent AI system for monitoring, explaining, and supporting a paper-traded equity income strategy.

The first strategy to implement is a quality-dividend and low-volatility equity income strategy. The system will use deterministic, tested Python tools for data collection, factor calculation, technical analysis, risk checks, portfolio construction, and paper-trading workflows. LangGraph agents will use those tools to monitor the portfolio, explain risks, review proposed rebalances, and produce human-readable reports.

The system is paper-trading only in v1.

## Strategy

The initial strategy is a quality-dividend and low-volatility equity income strategy.

This strategy stays close to a buy-and-hold investing mindset while still giving AI useful work to do. It focuses on companies or funds that appear to combine:

- Quality characteristics
- Durable dividends
- Lower volatility
- Reasonable diversification

The strategy is inspired by established methodologies, including:

- MSCI World Quality Index concepts, such as high return on equity, stable earnings growth, and low financial leverage.
- MSCI High Dividend Low Volatility concepts, such as high dividend yield, quality characteristics, and inverse-volatility weighting.
- S&P Dividend Aristocrats concepts, such as long histories of rising or maintained dividends.
- Low-risk investing research, including the idea that low-volatility or low-beta investing can improve risk-adjusted returns over long periods.

This is not intended to be a high-frequency trading system. It is a semi-passive strategy with periodic monitoring and review.

## Why This Strategy Fits An Agentic System

This strategy is suitable for a first agentic finance system because the analytics are explainable.

Agents can help by:

- Monitoring whether holdings still match the intended quality, dividend, and low-volatility traits.
- Flagging weakening dividend durability.
- Watching sector concentration and crowding.
- Reviewing high-yield securities that may be value traps.
- Comparing portfolio holdings against the written strategy rulebook.
- Explaining proposed rebalances in plain language.
- Producing recurring portfolio health reports.

The agents should not invent calculations or trade rules. Deterministic tools should calculate scores, indicators, risk checks, and portfolio weights. Agents should interpret those tool outputs and help the human user review decisions.

## V1 Scope

V1 will focus on a working paper-trading system.

Included in v1:

- Yahoo Finance data ingestion for prototype market and fundamentals data.
- Alpaca paper trading integration.
- A curated stock and/or ETF universe.
- Quality, dividend, volatility, and technical analysis calculations.
- Portfolio scoring and ranking.
- Basic portfolio construction.
- Risk guardrails.
- LangGraph-based multi-agent review workflow.
- Human-readable portfolio health reports.
- Human approval before any paper trade execution.

Excluded from v1:

- Live trading.
- Options, margin, leverage, short selling, or derivatives.
- High-frequency trading.
- Fully autonomous order placement without review.
- Research-grade point-in-time backtesting.
- Tax optimization.
- Multi-currency or international market support.

## Target Users

The first user is the project team.

The system should help beginner-to-intermediate developers and investors understand:

- Why a security is included or excluded.
- What risks exist in the current portfolio.
- Whether holdings still match the strategy.
- What changes a rebalance would make.
- Which decisions require human review.

## System Principles

- Deterministic tools perform calculations.
- Agents explain, monitor, compare, and review.
- Paper trading comes before any live-trading consideration.
- Human approval is required before execution.
- Strategy rules should be written before they are coded.
- New logic should have unit tests.
- Risk guardrails should be enforced in code, not only in prompts.
- The system should prefer clear explanations over unnecessary complexity.

## Data Sources

Initial prototype data source:

- Yahoo Finance

Execution and paper trading:

- Alpaca paper trading through `alpaca-py`

Known data limitation:

Yahoo Finance is acceptable for early prototyping, but it may have missing, delayed, revised, or inconsistent data. The architecture should isolate Yahoo Finance inside the data source layer so that another provider can replace it later without rewriting the full system.

## Agent Architecture

The project will use LangGraph for multi-agent workflows.

Initial planned agents:

- Supervisor Agent: coordinates the workflow and routes tasks.
- Portfolio Monitor Agent: reviews whether holdings still match the strategy.
- Technical Analyst Agent: interprets technical indicators from tested tools.
- Dividend Analyst Agent: reviews dividend durability and income quality.
- Risk Reviewer Agent: checks guardrails, concentration, and drawdown risks.
- Rebalance Reviewer Agent: explains proposed portfolio changes before approval.

Agents may call approved tools, but they should not directly perform raw calculations, fetch unvalidated data, or place trades without human approval.

## Risk Policy

The system must respect these v1 risk rules:

- Paper trading only.
- No live orders.
- No trade execution without human approval.
- No derivatives.
- No short selling.
- No leverage.
- Maximum position size must be enforced.
- Sector concentration limits must be enforced.
- The system must support dry-run mode.
- Execution logic must be separated from analysis and explanation logic.

## Definition Of Done For V1

V1 is complete when the system can:

- Ingest required prototype data.
- Calculate quality, dividend, volatility, and technical indicators.
- Score and rank the investment universe.
- Build a target portfolio using written constraints.
- Compare the target portfolio to the current Alpaca paper portfolio.
- Produce a proposed rebalance.
- Run risk guardrail checks.
- Generate a LangGraph agent review of the portfolio and proposed rebalance.
- Produce a weekly portfolio health report.
- Execute approved paper trades through Alpaca.
- Pass unit tests for core strategy, analytics, tools, and risk logic.

## Open Questions

- Will the first universe be ETF-only, stock-only, or mixed?
- How many securities should be in the starting universe?
- Which Yahoo Finance fields are reliable enough for prototype fundamentals?
- Which technical indicators should be used for v1?
- Should v1 include a lightweight historical sanity check?
- What rebalance cadence should be used: weekly, monthly, or quarterly?
- What maximum position and sector limits should be used?