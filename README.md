# Catalyst

**A social platform for stock theses with competitive performance tracking.** Post your thesis, an
AI stress-tests it against the news, and every thesis is scored on its real return vs. the S&P,
ranked by who actually beats the market.

## What it is

A *catalyst* is an investment thesis published as a structured argument, not a hot take:
- a **title** and your written **argument**,
- a **basket** of tickers with weights,
- the **pressures** you believe will move it (supply, demand, geopolitical, macro, contract),
- the **news and sources** that bear on those pressures.

For each pressure the system generates *boom* and *invalidation* scenarios, and as real news lands, a
pressure can be confirmed or invalidated, which automatically re-grades every thesis that cites it.

## How it's scored

Two numbers, kept separate on purpose.

**AI Sentiment (0 to 1)** is a reasoned opinion, not a vibe. A **red team** argues the most plausible
ways the thesis breaks; a **green team** the most plausible ways it pays off. Each scenario is
reasoned out first, then assigned an *impact* (how much it moves the basket) and a *likelihood*; those
net into an expected-value score, adjusted by how well trusted, independent news corroborates the
thesis. Every input is tagged by source (user, AI, or news) so the model knows what to trust. The math
is model-agnostic, so a stronger model sharpens the scores with zero rework.

**Φ (phi)** is the real scoreboard: your basket's return vs. the same dollars in the S&P 500 over the
same dates. Φ = 1.00 matched the market; above 1.00 beat it. Users are ranked by their average Φ
across ELO tiers (Bronze to Masters), so the leaderboard shows who is actually beating the market, not
who is loudest.

Connect a broker (Alpaca / IBKR) to deploy a basket for real; positions reconcile back into your Φ.

## The vision

A paid ETF-builder and brokerage passthrough on top of a free, public, S&P-beating leaderboard.
Anyone can post a thesis and prove it with results.

## Tech

Python + Flask, PostgreSQL with `pgvector`. Local-first AI via [Ollama](https://ollama.com)
(`qwen2.5:14b`), with a hosted backend selectable by config. A news pipeline that clusters and
trust-tiers stories, links them to pressures by embedding similarity, and re-grades affected theses on
confirmation or invalidation. Real price data with FX handling for overseas tickers; Φ and ELO computed
from actual basket returns vs. SPY.

---
*Product overview. Code, deployment, and configuration are maintained privately.*
