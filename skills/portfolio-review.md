# Portfolio Management: From "Researching Companies" to "Managing a Portfolio"

Run portfolio review and optimization on $ARGUMENTS.

**Supported input formats**:
- Holdings list, e.g.: `Tencent 30%, Meituan 20%, Moutai 20%, Nvidia 15%, Cash 15%`
- Or: `Tencent 500 shares @HK$480, Meituan 1000 shares @HK$130, ...`
- Or: `my portfolio` (if a saved portfolio file `reports/portfolio-latest.md` already exists)

> "Diversification is protection against ignorance. If you know what you're doing, diversification makes no sense." — Buffett
>
> "The truly good investment opportunities I've seen in my lifetime — I can count them on ten fingers." — Li Lu

## Design Philosophy

Researching companies is only half of investing. The other half is **portfolio-level decisions**:
- How much do you buy? (position sizing)
- What money do you use? (capital source — fresh capital or rotation)
- Does it conflict with existing holdings? (correlation)
- What does the optimal portfolio look like? (opportunity cost)

Buffett never looks at a single stock in isolation — he's always asking "is this the best thing I can do?"

## Execution Process

### Step 1: Parse Holdings

Parse the current holdings from the input, standardized as follows:

| Security | Ticker | Shares | Cost Basis | Current Price | Market Value | Weight | P&L |
|----------|--------|--------|------------|--------------|-------------|--------|-----|

If the input is only percentages without amounts, analyze based on percentages.

Also check whether an existing portfolio file exists (`reports/portfolio-latest.md`); if so, read and update it.

### Step 2: Fetch Latest Data

Launch a background agent to fetch the following for each holding in parallel via WebSearch:
1. Current price and valuation metrics (PE, PB, dividend yield)
2. Key financial changes in the most recent quarter
3. Recent major events
4. Analyst consensus estimates (forward PE, price targets)

Use `tools/financial_rigor.py verify-valuation` to validate valuation data for each holding. Rate each holding's information richness (A/B/C level); annotate C-level holdings with low confidence.

### Step 3: Individual Position Health Check

Run a quick health check on each holding:

| Security | Current PE | Has buying thesis changed? | Thesis health | Position recommendation |
|----------|:----------:|:-------------------------:|:----------:|------------------------|
| Tencent | 18x | No change | 8/10 | Appropriate |
| Meituan | 25x | Competition intensifying | 6/10 | Slightly high, consider trimming |

For each holding, answer:
- [ ] **If you had no position today, would you buy at the current price?**
- [ ] **If you couldn't trade tomorrow, are you comfortable holding for 5 years?**
- [ ] **Is the buying thesis still intact?**

**Duan Yongping**: "If you don't want to hold a stock for 10 years, don't hold it for a single day."

### Step 4: Portfolio-Level Analysis

#### 4.1 Concentration Analysis

| Metric | Current | Recommended Range | Assessment |
|--------|---------|-------------------|------------|
| Largest single position | | < 40% | |
| Top 3 positions combined | | 50–80% | |
| Total number of holdings | | 5–15 | |
| Cash allocation | | 10–30% (depending on market) | |

**Li Lu's standard**: 3–5 core holdings, top 3 at 80%+. **But this requires each one to be thoroughly researched.**

**Buffett's standard**: No more than 10 core positions, but more satellite positions are acceptable.

#### 4.2 Correlation Check

Identify hidden correlations across holdings:

| Holding A | Holding B | Correlation Type | Risk |
|-----------|-----------|-----------------|------|
| Tencent | Kuaishou | Both Chinese internet | Regulatory risk resonance |
| Nvidia | TSMC | AI supply chain (upstream/downstream) | AI CapEx moves in tandem |
| Meituan | Pinduoduo | Both Chinese consumer | Macro consumption moves in tandem |

**Checklist**:
- [ ] More than 50% of positions exposed to the same theme/sector?
- [ ] More than 50% of positions exposed to the same country/currency?
- [ ] If US-China relations deteriorate, how much would the portfolio lose?
- [ ] If global recession hits, how much would the portfolio lose?

#### 4.3 Opportunity Cost Analysis

This is Buffett's most central mode of thinking — **every dollar should be placed where it generates the best return**.

Rank all holdings by "expected annualized return":

| Rank | Security | Current Weight | Expected Annual Return | Confidence | Expected Return × Confidence |
|:----:|----------|:-------------:|:---------------------:|:----------:|:----------------------------:|
| 1 | | | | | |
| 2 | | | | | |
| ... | | | | | |

Expected return estimation method (use `tools/financial_rigor.py three-scenario`):
- **Simplified formula**: Expected annual return ≈ FCF yield + expected growth rate (primary method)
- **Value stock verification**: Margin of safety reversion + earnings growth + dividend yield
- **Growth stock verification**: Earnings growth × change in justified PE

**Key question**: Is the expected return on the lowest-ranked holding higher than cash (risk-free rate ~4%)? If not, sell and move to cash.

#### 4.4 Stress Tests

| Scenario | Assumption | Estimated Portfolio Impact | Maximum Drawdown |
|----------|------------|--------------------------|-----------------|
| Global recession | Corporate earnings down 20–30% | | |
| US-China conflict escalates | Chinese stocks discount 50% | | |
| Interest rates spike | 10-yr Treasury → 6% | | |
| Tech bubble bursts | Tech PE compresses 40% | | |

For each scenario, provide a qualitative + rough quantitative assessment (based on each holding's sector characteristics and historical valuation range):
- Which holdings are hit hardest? Approximate direction and magnitude
- Can the portfolio as a whole withstand it?
- Is hedging necessary?

### Step 5: Optimization Recommendations

#### 5.1 Rebalancing Recommendations

Based on the above analysis, give specific rebalancing recommendations:

| Action | Security | Current Weight | Recommended Weight | Rationale |
|--------|----------|:-------------:|:-----------------:|----------|
| Add | | | | |
| Trim | | | | |
| Exit | | | | |
| New position | | | | |
| No change | | | | |

#### 5.2 Finding Replacement Holdings

If the portfolio has positions "worse than cash," or if cash allocation is too high, recommend using `/industry-research` or `/investment-checklist` to systematically screen industries/companies of interest — rather than directly recommending individual stocks within this skill.

#### 5.3 Cash Management

| Current Cash | Recommended Cash | Rationale |
|:------------:|:---------------:|----------|

**Buffett**: Currently holds $382B in cash, over 25% of total assets — when you can't find good opportunities, cash is the best position.

### Step 6: Output Portfolio Report

#### Report Structure

```
1. Portfolio Overview (holdings table + pie chart description)
2. Individual Position Health Checks (health status per holding)
3. Portfolio Analysis
   - Concentration: Over-diversified or over-concentrated?
   - Correlation: Hidden linkages and risk resonance
   - Opportunity cost: Is the lowest-ranked holding worth keeping?
   - Stress tests: Estimated drawdown in extreme scenarios
4. Rebalancing Recommendations (specific actions + rationale)
5. Next review timing and key focus points
```

#### Conclusion Must Explicitly Answer

1. **Overall portfolio health**: Excellent / Good / Needs adjustment / Seriously problematic
2. **The single most important action**: Add to X / Trim Y / Do nothing
3. **Biggest current risk**

### Step 7: Save Portfolio File

Write portfolio information to `reports/portfolio-latest.md`, including:
- Latest holdings table
- Date and conclusion of this review
- Rebalancing log (append)
- Next review reminder

---

## Key Principles

- **Every dollar has an opportunity cost** — holding a mediocre stock costs you a better one
- **Concentration is not risk; ignorance is** — 3 stocks you deeply understand are safer than 30 you half-understand
- **Cash is a position** — holding cash when you can't find good opportunities is not embarrassing
- **Portfolio-level > individual stock-level** — a great stock in the wrong position size still drags you down
- **Review regularly, but don't over-trade** — a quarterly review is enough; don't check prices every day
