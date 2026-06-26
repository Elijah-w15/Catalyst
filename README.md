 <div align="center">

# Catalyst

 </div>
  
  <div align="center">

  ### link: [Rankedcatalyst.com](https://rankedcatalyst.com) *not publicly hosted yet*

  </div>

  ---

Summery: **A social platform for stock theses with competitive performance tracking.** Post your thesis, an
AI stress-tests it against the news, and every thesis is scored on its real return vs. the S&P, with a 
ranked ladder by who actually beats the market.

## What  is a "Catalyst"

A *catalyst* is an investment thesis published as a structured argument:
- a **title** and your written **argument**,
- a **basket** of tickers impacted with weights,
- taged **pressures** you believe will move the selected stocks (supply, demand, geopolitical, macro, contract),
- supporting **news/sources** added by author.

For each pressure the system generates *boom* and *invalidation* scenarios, and as real news lands, a
pressure can be confirmed or invalidated, which automatically re-grades every thesis that cites it.

## How it's scored

Two numbers, kept separate on purpose.

**Φ (phi)** is the real scoreboard: your basket's return vs. the same dollars in the S&P 500 over the
same dates. Φ = 1.00 matched the market; above 1.00 beat it. Users are ranked by their average Φ
across ELO tiers (Bronze to Masters), so the leaderboard shows who is actually beating the market, not
who is loudest.

**AI Sentiment (0 to 1)** is an expected-value function over generated scenarios. A **red team** works
through the ways the thesis could break; a **green team** the ways it could pay off. For each scenario
the model reasons from the thesis and the news to an *impact* (how much it would move the basket) and a
*likelihood*: an evidence-grounded estimate, not a claim to know the future. The score is the net
expected value across those scenarios (green minus red), squashed to 0 to 1, then weighted by how well
trusted, independent news corroborates the thesis.

## The vision

A paid SaaS ETF-builder and brokerage passthrough on top of a free, public, competitive S&P-beating leaderboard.
Anyone can post a thesis and have it tracked against the S&P for a spot on the ranked ladder.

Premium unlocks the rest: connect a partner broker (Alpaca or IBKR) and deploy a catalyst for real, turning any thesis 
into a useable, custom ETF.
  
## Tech

Python + Flask, PostgreSQL with `pgvector`. Local-first AI via [Ollama](https://ollama.com)
(`qwen2.5:14b`), with a hosted backend selectable by config. A news pipeline that clusters and
trust-tiers stories, links them to pressures by embedding similarity, and re-grades affected theses on
confirmation or invalidation. Real price data with FX handling for overseas tickers; Φ and ELO computed
from actual basket returns vs. SPY.

---
*Product overview. Code, deployment, and configuration are maintained privately.*
