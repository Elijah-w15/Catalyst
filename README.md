# Catalyst

**A social platform for stock theses with competitive performance tracking: post your thesis, an AI stress-tests it against the news, and every thesis is scored on its real return vs. the S&P, ranked by who actually beats the market.**

Catalyst is a platform for investment theses. Instead of a hot take, you publish a **catalyst**: a
written thesis, a basket of stocks, and the real-world **pressures** you believe will push that
basket one way or the other. An AI red-team / green-team stress-tests the thesis against the news,
and every thesis is **competitively tracked** on how its basket actually performs against the
S&P 500 over the same window. Conviction is settled by results, not volume: users are ranked on the
real performance of the theses they post.

---

## How it works

**A catalyst** is an investment thesis with four parts:
- a **title** and the author's written **argument**,
- a **basket** of tickers with weights,
- the **pressures** driving it: the forces (supply, demand, geopolitical, macro, contract) the
  author believes will move the basket,
- linked **evidence**: news and sources that bear on those pressures.

**Pressures** are the heart of the thesis. For each one the system generates **boom** and
**invalidation** scenarios (what would confirm it vs. what would break it), and as real news flows
in, a pressure can be confirmed or invalidated, which automatically re-grades every thesis that
cites it.

**The AI Sentiment score (0 to 1)** is a structured, reasoned opinion, not a vibe:
- a **red team** writes the most plausible ways the thesis *derails*, a **green team** the most
  plausible ways it *strengthens*. Each scenario is reasoned out first, then assigned an **impact**
  (how much it moves the basket) and a **likelihood** (how probable it is).
- those net into an **expected-value** score (`Σ green impact×likelihood − Σ red impact×likelihood`,
  squashed to 0 to 1),
- which is then modified by how well **trusted, independent news corroborates** the thesis.

Every input is tagged by provenance (*user-submitted*, *AI-generated*, or *news source*) so the
model knows what to trust. The scoring is **model-agnostic**: the math consumes whatever numbers the
model produces, so a stronger model yields sharper, better-calibrated scores with zero rework. It
makes no claim to predict tomorrow. It applies the same disciplined, evidence-grounded analysis to
every thesis, consistently, and updates when the news moves.

**Φ (phi), performance vs. the market.** Every basket is tracked against *the same dollars in the
S&P 500 over the same dates*. **Φ = 1.00 means you matched the market; greater than 1.00 means you
beat it.** This is the objective scoreboard, fully independent of the AI sentiment score.

**Ranking.** A user's standing is their **average catalyst Φ**, tiered into ELO bands
(Bronze, Silver, Gold, Platinum, Diamond, Masters). The leaderboard ranks who is actually beating
the market.

**Brokerage passthrough.** Connect a broker (Alpaca / IBKR) to deploy a basket for real; positions
and performance reconcile back into your Φ.

---

## The vision

A paid ETF-builder and brokerage passthrough on top of a **free, public, S&P-beating leaderboard**.
Anyone can post a thesis and prove it with real performance; the best ideas rise on results.

---

## Tech

- **Backend:** Python + Flask, PostgreSQL (with `pgvector` for embeddings).
- **AI:** local-first via [Ollama](https://ollama.com) (currently `qwen2.5:14b`), with a hosted
  backend (Anthropic) selectable by config. Deterministic, fully-traceable scoring math.
- **News pipeline:** ingests, clusters, and trust-tiers news; links stories to pressures by
  embedding similarity; re-grades affected theses when a pressure is confirmed or invalidated.
- **Performance:** real price data with FX handling for overseas tickers; Φ and ELO computed from
  actual basket returns vs. SPY.

## Status

v1, under active development. Local-first today; the scoring engine is intentionally model-agnostic
so it scales in quality as the model and the live-news corpus grow.

---

*This is a product-overview README. The codebase, deployment, and configuration are maintained
privately.*
