---
name: portfolio-review
description: "AI Berkshire skill: Portfolio Management: From 'Researching Companies' to 'Managing a Portfolio'. Source: skills/portfolio-review.md."
---

## Codex adapter note

This skill is generated from `skills/portfolio-review.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Portfolio Management: From "Researching Companies" to "Managing a Portfolio"

Execute a portfolio review and optimization for $ARGUMENTS.

**Supported input formats**:
- A list of positions, e.g.: `Tencent 30%, Meituan 20%, Moutai 20%, Nvidia 15%, Cash 15%`
- Or: `Tencent 500 shares @HKD 480, Meituan 1000 shares @HKD 130, ...`
- Or: `my portfolio` (if a saved portfolio file `reports/portfolio-latest.md` already exists)

> "Diversification is protection against ignorance. It makes little sense if you know what you are doing." — Buffett
>
> "In my entire life, the truly great investment opportunities I have seen can be counted on the fingers of both hands." — Li Lu

## Design Philosophy

Researching a company is only half of investing. The other half is **portfolio-level decision-making**:
- How much to buy? (position sizing)
- Where does the money come from? (source of funds — new cash or a swap)
- Does it conflict with existing positions? (correlation)
- What does the optimal portfolio look like? (opportunity cost)

Buffett never looks at a single stock in isolation — he is always asking "Is this the best thing I can do?"

## Execution Workflow

### Step 1: Parse Positions

Parse the current positions from the input and standardize them into the following format:

| Ticker | Symbol | Shares | Cost Basis | Current Price | Market Value | Weight | P&L |
|--------|--------|--------|------------|---------------|--------------|--------|-----|

If the input only provides percentages without dollar amounts, analyze by weight alone.

Also check whether an existing portfolio file (`reports/portfolio-latest.md`) exists; if so, read and update it.

### Step 2: Fetch Latest Data

Use the Task tool to launch a background Agent that uses WebSearch to fetch the following for each position in parallel:
1. Current price and valuation metrics (PE, PB, dividend yield)
2. Key financial changes from the most recent quarter
3. Recent material events
4. Analyst consensus estimates (forward PE, price targets)

Use `tools/financial_rigor.py verify-valuation` to validate valuation data for each position. Tag each position with an information-richness grade (A/B/C); label analytical conclusions for C-grade positions as low-confidence.

### Step 3: Individual Position Health Check

Perform a quick health check on each position:

| Ticker | Current PE | Buy Thesis Unchanged? | Thesis Health | Position Recommendation |
|--------|:----------:|:---------------------:|:------------:|------------------------|
| Tencent | 18x | Unchanged | 8/10 | Appropriate |
| Meituan | 25x | Competition intensifying | 6/10 | Overweight, consider trimming |

Answer the following for each position:
- [ ] **If you had no position today, would you buy at the current price?**
- [ ] **If you could not trade tomorrow, are you comfortable holding for 5 years?**
- [ ] **Is the buy thesis still intact?**

**Duan Yongping**: "If you don't want to hold a stock for 10 years, don't hold it for a single day."

### Step 4: Portfolio-Level Analysis

#### 4.1 Concentration Analysis

| Metric | Current Value | Recommended Range | Assessment |
|--------|--------------|-------------------|------------|
| Largest single position weight | | <40% | |
| Top 3 positions combined weight | | 50-80% | |
| Total number of positions | | 5-15 | |
| Cash weight | | 10-30% (depending on market environment) | |

**Li Lu's standard**: 3-5 core positions, top 3 comprising 80%+. **But this requires each one to be thoroughly researched.**

**Buffett's standard**: No more than 10 core positions, but satellite positions are allowed beyond that.

#### 4.2 Correlation Check

Identify hidden linkages among positions:

| Position A | Position B | Correlation Type | Risk |
|------------|------------|-----------------|------|
| Tencent | Kuaishou | Both Chinese internet | Regulatory risk resonance |
| Nvidia | TSMC | AI supply chain upstream/downstream | AI capex moves in tandem |
| Meituan | Pinduoduo | Both Chinese consumer | Macro consumption moves in tandem |

**Checklist**:
- [ ] Does more than 50% of the portfolio have exposure to the same theme/industry?
- [ ] Does more than 50% of the portfolio have exposure to the same country/currency?
- [ ] If US-China relations deteriorate, how much would the portfolio lose?
- [ ] If the global economy enters recession, how much would the portfolio lose?

#### 4.3 Opportunity Cost Analysis

This is Buffett's most fundamental mental model — **every dollar should be placed where it earns the highest return**.

Rank all positions by "expected annualized return":

| Rank | Ticker | Current Weight | Expected Annualized Return | Certainty | Expected Return × Certainty |
|:----:|--------|:--------------:|:--------------------------:|:---------:|:---------------------------:|
| 1 | | | | | |
| 2 | | | | | |
| ... | | | | | |

Expected return estimation methods (use `tools/financial_rigor.py three-scenario` to calculate):
- **Simplified formula**: Expected annualized ≈ FCF Yield + Expected Growth Rate (primary method)
- **Value-stock validation**: Margin of safety reversion + earnings growth + dividend yield
- **Growth-stock validation**: Earnings growth × change in fair PE

**Key question**: Does the lowest-ranked position have an expected return above cash (risk-free rate ~4%)? If not, it should be sold and replaced with cash.

#### 4.4 Stress Testing

| Scenario | Assumption | Estimated Portfolio Impact | Max Drawdown |
|----------|------------|---------------------------|--------------|
| Global recession | Corporate earnings decline 20-30% | | |
| US-China conflict escalation | Chinese ADRs discounted 50% | | |
| Interest rate spike | 10-year Treasury → 6% | | |
| Tech bubble burst | Tech sector PE compressed 40% | | |

Provide a qualitative + rough quantitative assessment for each scenario (based on the industry characteristics and historical valuation volatility of each position):
- Which positions are hit hardest? Approximate direction and magnitude of impact
- Can the portfolio as a whole withstand it?
- Is hedging necessary?

### Step 5: Optimization Recommendations

#### 5.1 Rebalancing Recommendations

Based on the above analysis, provide specific rebalancing recommendations:

| Action | Ticker | Current Weight | Target Weight | Rationale |
|--------|--------|:--------------:|:-------------:|-----------|
| Add | | | | |
| Trim | | | | |
| Exit | | | | |
| Initiate | | | | |
| Hold | | | | |

#### 5.2 Finding Replacement Candidates

If the portfolio contains positions that are "worse than cash," or if cash weight is too high, recommend using `/industry-research` or `/investment-checklist` to systematically screen industries/companies of interest — rather than recommending individual stocks directly within this skill.

#### 5.3 Cash Management

| Current Cash Weight | Target Cash Weight | Rationale |
|:-------------------:|:-----------------:|-----------|

**Buffett**: Currently holding $382 billion in cash, representing over 25% of total assets — when no good opportunities can be found, cash is the best position.

### Step 6: Output Portfolio Report

#### Report Structure

```
I.   Portfolio Overview (position table + pie chart description)
II.  Individual Position Health Check (health status of each position)
III. Portfolio Analysis
     - Concentration: Over-diversified or over-concentrated?
     - Correlation: Hidden linkages and risk resonance
     - Opportunity Cost: Is the lowest-ranked position worth holding?
     - Stress Test: Drawdown estimates under extreme scenarios
IV.  Rebalancing Recommendations (specific actions + rationale)
V.   Next review date and key focus areas
```

#### Conclusions Must Explicitly Answer

1. **Overall portfolio health**: Excellent / Good / Needs Adjustment / Serious Issues
2. **What is the single most important thing to do?** (Add X / Trim Y / Hold)
3. **What is the current greatest risk?**

### Step 7: Save Portfolio File

Write the portfolio information to `reports/portfolio-latest.md`, including:
- Latest position table
- Date and conclusions of this review
- Rebalancing log (appended)
- Next review reminder

---

## Core Principles

- **Every dollar has an opportunity cost** — holding a mediocre stock means missing out on an excellent one
- **Concentration is not risk; ignorance is** — holding 3 stocks you deeply understand is safer than holding 30 you barely know
- **Cash is a position** — when no good opportunities exist, holding cash is not a weakness
- **Portfolio level > individual stock level** — even a great stock in the wrong position size will drag you down
- **Review regularly, but do not overtrade** — reviewing once per quarter is sufficient; do not monitor positions daily and trade constantly
