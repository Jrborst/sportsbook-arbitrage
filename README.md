# Sportsbook Arbitrage & Market Inefficiency Trading System

Real-time arbitrage detection and positive expected value (EV) betting system across 8 sportsbooks. Deployed with live capital, achieving 50% cumulative ROI before accounts were stake-limited due to sustained profitability.

## Overview

This system identifies and exploits two types of pricing inefficiencies in sports betting markets:

1. **Arbitrage opportunities** — cases where odds across different sportsbooks imply a total probability below 100%, guaranteeing a risk-free profit regardless of outcome
2. **Positive EV bets** — cases where a single sportsbook's odds underestimate the true probability of an outcome, offering positive expected value over a large sample

The core insight is that sportsbooks price independently and update at different speeds, creating temporary mispricings that can be systematically detected and exploited before they close.

## System Components

### Real-Time Odds Scraper
- Scrapes live odds across 8 major sportsbooks simultaneously
- Monitors multiple sports and bet types in real time
- Flags opportunities the moment a mispricing appears

### Arbitrage Detection Engine
- Calculates implied probabilities from odds across all books
- Identifies cross-platform discrepancies where total implied probability is below 100%
- Computes guaranteed profit margin and optimal stake allocation across books

### EV Detection Engine
- Estimates true probabilities using a consensus model derived from the sharpest books
- Flags bets where a soft book's odds imply a higher payout than the true probability warrants
- Ranks opportunities by edge size for prioritized execution

### Position Sizing
- Kelly Criterion optimal sizing to maximize long-run bankroll growth
- Fractional Kelly applied to manage variance and drawdown risk
- Separate sizing logic for arbitrage (risk-free) vs. EV bets (probabilistic edge)

### Backtesting Framework
- Monte Carlo simulation across historical opportunities to model profit distributions and drawdowns
- Stress tests position sizing under adverse variance scenarios
- Validates edge persistence across different sports, bet types, and time periods

## Results

| Metric | Arbitrage | Positive EV |
|---|---|---|
| Total bets backtested | 2,250 | 4,100 |
| Average return per bet | 2.63% | 3.26% edge |
| Deployment | Live capital | Live capital |
| Cumulative ROI | 50% across both strategies combined |
| Outcome | Accounts stake-limited due to sustained profitability |

The stake-limiting outcome is itself a signal. Sportsbooks restrict accounts that win consistently, which validates that the edge being captured is real and non-random.

## Technical Stack

- **Python** — core system
- **pandas, NumPy** — data processing and probability calculations
- **scipy** — statistical modeling and Monte Carlo simulation
- **matplotlib** — visualization of profit distributions and drawdown curves
- **Odds API** — commercial odds API for real-time data ingestion across sportsbooks

## Key Concepts

**Arbitrage in betting markets vs. financial markets:** The mechanics are structurally similar to cross-venue arbitrage in equity markets. Different market makers (sportsbooks) price the same underlying event independently, creating temporary discrepancies that close as odds converge. Execution speed and account longevity are the primary constraints, analogous to latency and capital constraints in financial arbitrage.

**Positive EV as a systematic edge:** EV betting is analogous to a market maker fading an informed trader. The edge comes from identifying books that are slower to update their lines relative to the consensus, and systematically betting against their stale prices.

**Kelly Criterion:** Position sizing follows the Kelly Criterion to maximize the geometric growth rate of the bankroll. Fractional Kelly (half-Kelly) is applied in practice to reduce variance while preserving most of the theoretical growth rate advantage.

## Status

System was actively deployed from January 2025 to August 2025. Accounts were subsequently stake-limited by sportsbooks. Code is not publicly shared to protect methodology.
