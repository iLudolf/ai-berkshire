# Portfolio Management: From "Researching Companies" to "Managing a Portfolio"

Run portfolio review and optimization on $ARGUMENTS.

**Supported input formats**:
- Holdings list, e.g.: `PETR4 25%, VALE3 20%, MXRF11 15%, KNRI11 10%, BOVA11 15%, Cash 15%`
- Or: `PETR4 500 shares @R$38.50, MXRF11 1000 shares @R$9.80, BOVA11 200 shares @R$125.00, ...`
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
1. Current price and valuation metrics:
   - **Ações B3**: P/L, P/VPA, ROE, Dividend Yield, Dívida Líquida/EBITDA (Fundamentus primary)
   - **FIIs**: DY (12M), P/VP, vacância física/financeira, tipo (Tijolo/Papel/Híbrido/FOF) (FundsExplorer primary)
   - **ETFs**: TER (taxa de administração), índice de referência, desempenho vs. benchmark
2. Key financial changes in the most recent quarter (ITR/DFP for ações; Relatório Gerencial + CVM Informe Mensal for FIIs)
3. Recent major events (dividends announced, portfolio changes for FIIs, management updates)
4. Analyst consensus estimates (forward P/L, price targets from XP, Itaú BBA, BTG, Goldman Sachs Brasil)

Use `tools/financial_rigor.py verify-valuation` to validate valuation data for each holding. Rate each holding's information richness (A/B/C level); annotate C-level holdings with low confidence.

### Step 3: Individual Position Health Check

Run a quick health check on each holding:

**Ações / ETFs:**

| Security | Metric | Has buying thesis changed? | Thesis health | Position recommendation |
|----------|:------:|:-------------------------:|:----------:|------------------------|
| PETR4 | P/L 5x | No change — oil prices stable | 8/10 | Appropriate |
| VALE3 | P/L 7x | Iron ore demand slowing | 6/10 | Slightly high, consider trimming |
| BOVA11 | TER 0.10% | Index diversification thesis intact | 9/10 | Appropriate |

**FIIs:**

| FII | DY 12M | P/VP | Vacância | Thesis health | Recommendation |
|-----|:------:|:----:|:--------:|:----------:|----------------|
| MXRF11 | 14% | 0.98 | N/A (Papel) | 8/10 | Appropriate |
| KNRI11 | 8% | 0.95 | 8% físico | 7/10 | Monitor vacancy trend |

For each holding, answer:
- [ ] **If you had no position today, would you buy at the current price?**
- [ ] **If you couldn't trade tomorrow, are you comfortable holding for 5 years?**
- [ ] **Is the buying thesis still intact?**

**Additional checks for FIIs:**
- [ ] Is the DY still competitive vs. current Selic/CDI? (DY - Selic spread must justify illiquidity + risk)
- [ ] Vacancy trending up or down? Any lease renewals at risk?
- [ ] Is the fund manager executing consistently? (check Relatório Gerencial quality)
- [ ] For Papel FIIs: any CRI/CRA default risk in the portfolio?

**Additional checks for ETFs:**
- [ ] Is the tracked index still aligned with your thesis?
- [ ] Is TER competitive vs. alternatives (e.g., BOVA11 vs. BOVV11)?

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
| PETR4 | PRIO3 / RECV3 | Both oil producers | Oil price moves in tandem |
| VALE3 | CSNA3 / GGBR4 | Commodity / steel chain | Iron ore price sensitivity |
| MXRF11 | KNCR11 | Both Papel FIIs | CDI drop compresses yield together |
| KNRI11 | HGLG11 | Both Tijolo (logistics/office) | Vacancy cycle / rent correction |
| ITUB4 | BBDC4 | Both large-cap banks | Selic + default cycle resonance |
| BOVA11 | Any individual B3 stock | Index overlap | Ibovespa concentration (PETR+VALE+ITUB = ~30% of BOVA11) |

**Checklist**:
- [ ] More than 50% of positions exposed to the same commodity (oil / iron ore)?
- [ ] More than 50% of FII allocation in the same FII type (all Papel or all Tijolo)?
- [ ] If Selic rises 200bps, how much would the FII portion fall?
- [ ] If commodity prices drop 30%, how much would the portfolio lose?
- [ ] If BRL depreciates 20% vs. USD, is there any natural hedge?
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

**Key question for Brazilian portfolios**: Is the expected return on the lowest-ranked holding higher than **Selic/CDI** (the Brazilian risk-free rate, currently ≈14.75%)? This is a uniquely high hurdle — any asset that doesn't clearly beat Selic with a margin of safety should be replaced by Tesouro Selic (LFT) or a CDB 100% CDI. This is why Brazilian value investing requires exceptional conviction — the risk-free bar is very high.

#### 4.4 Stress Tests

| Scenario | Assumption | Estimated Portfolio Impact | Maximum Drawdown |
|----------|------------|--------------------------|-----------------|
| Global recession | Commodity prices −30%, Ibovespa −35% | | |
| Selic spike | Selic → 16%+ (FII P/VP compress, credit tightens) | | |
| BRL depreciation | USD/BRL → 7.00 (inflationary, raises Selic pressure) | | |
| Political / fiscal shock | Debt ceiling concerns, market repricing of Brazil risk | | |
| Commodity super-cycle end | Iron ore < $80/t, oil < $60/bbl sustained | | |
| FII sector correction | Office vacancy > 20%, logistics oversupply | | |

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

**Brazilian context**: "Cash" in Brazil = Tesouro Selic (LFT) or CDB 100%+ CDI — liquidity with ≈14.75% annual return. Holding idle BRL in a checking account while waiting for opportunities is a capital allocation error: the risk-free rate in Brazil is one of the highest in the world.

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
