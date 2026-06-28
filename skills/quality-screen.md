# Quality Screen: 7 Indicators to Eliminate Below-Par Companies

Run quality elimination screening on $ARGUMENTS, rapidly filtering out companies that fail to meet first-class standards.

**Supported input formats**:

| Input Type | Example | Notes |
|-----------|---------|-------|
| Individual stocks | `WEGE3, ITUB4, Nvidia` | Screen each one |
| Industry | `Brazil energy sector` `Global cloud computing` `B3 financials` | Search for 10-20 major listed companies first, then screen each |
| Market/Index | `Ibovespa constituents` `SMLL (small caps)` `Nasdaq 100` | Fetch constituent list, screen each |
| Theme | `Brazil top-50 dividend stocks` `Global AI compute chain` | Search for related companies first, then screen |

In industry/market/theme mode, output additionally includes: pass rate statistics, intra-industry rankings, and sector comparison summary.

## Design Principles

- **Goal**: Never eliminate any genuinely first-class company, but reliably exclude definitely below-par ones
- **Logic**: 7 hard indicators + 3 exemption rules — prefer false negatives over false positives
- **Scope**: All listed companies (banks/insurance companies exempt from #3, interest coverage)

---

## 7 Quality Elimination Indicators

| # | Indicator | Elimination Threshold | What It Measures |
|---|-----------|----------------------|-----------------|
| 1 | 10-year average ROE | < 8% | Capital efficiency — can shareholders' money beat opportunity cost? |
| 2 | 5-year cumulative FCF | Negative | Real cash generation — is profit just paper gains? |
| 3 | Interest coverage ratio (EBIT/Interest) | < 2x | Debt safety — can it service its debt? |
| 4 | Long-term gross margin | < 15% | Pricing power — does the product/service have differentiation? |
| 5 | Operating cash flow / Net income (5-yr avg) | < 0.7 | Profit quality — can earned profit be collected in cash? |
| 6 | Long-term net margin | < 5% | Resilience — does profit go to zero when revenue fluctuates? |
| 7 | 5-year total share count growth | > 20% (non-acquisition) | Shareholder interests — is management diluting your equity? |

## 3 Exemption Rules

### Exemption A: Strategic Investment Phase (applies to #1)

A company may be exempted from the ROE threshold if it simultaneously meets all 3 conditions:
1. Listed fewer than 10 years
2. Gross margin > 30% (proves the business model itself has pricing power)
3. Operating cash flow positive in the last 2 years (proves earning capacity is established)

**Logic**: High gross margin + positive cash flow means the business model is sound; low ROE is only because it's still in investment mode. Typical case: RDOR3 (Rede D'Or) in its post-IPO expansion phase.

### Exemption B: Deliberate Low Margin (applies to #6)

A company may be exempted from the net margin threshold if it simultaneously meets both conditions:
1. Gross margin > 30% (can earn but chooses not to)
2. Net margin has recovered above 5% in the last 2 years, or shows a clear upward trend

**Logic**: High gross margin indicates pricing power; low net margin is a strategic choice (reinvestment), not a capability deficit. Typical case: Amazon.

### Exemption C: High-Turnover Thin-Margin Model (applies to #4 and #6)

A company may be exempted from both gross margin and net margin thresholds if it simultaneously meets all 3 conditions:
1. ROE > 20% (proves that despite low margins, capital returns are exceptional)
2. Operating cash flow / Net income > 1.0 (profit quality is solid)
3. Business model is membership/platform commission/high-turnover thin-margin type (profit not embedded in product markup)

**Logic**: Some first-class companies hide their profits not in gross margins, but in membership fees, turnover efficiency, or platform take rates. Their gross and net margins are naturally low, but high ROE proves capital efficiency is exceptional. Typical case: Costco (gross margin 12%, net margin 2.5%, but ROE 25%+, membership renewal rate 90%+).

---

## Execution Process

### Step 1: Parse Input, Define Screening Scope

**Mode determination**:
- If input is specific company names/tickers → **Individual stock mode**, proceed to Step 2
- If input is industry/market/theme → **Batch mode**, first execute:
  1. Use WebSearch to find major listed companies in the industry/market/theme
  2. Industry mode: cover the 15-20 largest listed companies by market cap
  3. Index mode: fetch the complete constituent list
  4. Theme mode: search for related companies, covering 15-30
  5. List the complete company roster for confirmation (if companies > 30, process in parallel batches)

Confirm full name, ticker, and exchange for each company.

### Step 2: Parallel Data Collection

Launch an independent background agent for each company to search the following data via WebSearch:

1. **ROE**: Annual ROE for the past 10 years (or since IPO), calculate average
2. **Free cash flow**: Operating cash flow and CapEx for the past 5 years, calculate 5-year cumulative FCF
3. **Interest coverage**: Latest annual EBIT and interest expense, calculate ratio
4. **Gross margin**: Gross margin trend over the past 5 years
5. **OCF/Net income**: 5-year ratio, calculate average
6. **Net margin**: Net margin trend over the past 10 years, calculate average
7. **Share count change**: Total shares 5 years ago vs. current, calculate growth percentage

Data source priority: CVM filings (DFP/ITR) > Fundamentus / Status Invest > Broker research (XP, BTG, Itaú BBA) > Financial data platforms

### Step 3: Check Each Indicator

For each company, check each of the 7 indicators:
- ✅ Pass
- ❌ Fail
- ⚠️ Borderline (with specific data note)

If a company triggers a failure, check whether it meets the corresponding exemption conditions.

### Step 4: Output Results

#### Output Format

```markdown
# Quality Screen Results

**Screening Date**: {today's date}
**Companies Screened**: {N}

## Summary Table

| Company | ①ROE | ②FCF | ③Int.Cov | ④Gross Margin | ⑤OCF/NI | ⑥Net Margin | ⑦Dilution | Result |
|---------|------|------|---------|--------------|---------|------------|----------|--------|
| xxx | ✅ 24% | ✅ | ✅ | ✅ 56% | ✅ | ✅ 30% | ✅ | **Pass** |
| yyy | ❌ 3% | ❌ | ❌ | ✅ 20% | ✅ | ❌ 2% | ✅ | **Eliminated** |
| zzz | ⚠️→✅ | ✅ | ✅ | ✅ 35% | ✅ | ⚠️→✅ | ✅ | **Exemption Pass** |

## Companies That Passed ({N})
[List]

## Companies Eliminated ({N})
| Company | Indicators Triggered | Specific Data | Reason for Elimination |
|---------|---------------------|--------------|----------------------|

## Companies Passing via Exemption ({N})
| Company | Exemption Applied | Specific Data | Exemption Rationale |
|---------|------------------|--------------|---------------------|

## Borderline Cases (if any)
[Additional notes on companies near the thresholds]

## Sector Summary (industry/market mode only)

**Pass rate**: {passed}/{total} = {percentage}%
**Industry quality judgment**: [Overall quality assessment based on pass rate]

| Quality Tier | Companies | Common Traits |
|-------------|---------|--------------|
| First-class (all pass + high ROE) | xxx, yyy | ... |
| Acceptable (all pass but mediocre metrics) | aaa, bbb | ... |
| Eliminated | ccc, ddd | ... |

**Industry stock-picking conclusion**: [One sentence on whether the industry is worth digging into, and which 2-3 deserve the most attention]
```

---

## Notes

1. **Banks/Insurance**: Not subject to #3 (interest coverage) — their business model is fundamentally interest-margin based
2. **FIIs (Brazilian REITs)**: ROE/FCF metrics do not apply — use DY (dividend yield), P/VP (price/book), and vacância (vacancy rate) instead; screen FIIs separately using the FII-specific checklist
3. **Insufficient data**: If a data point is unavailable, note "data unavailable" rather than defaulting to pass/fail
4. **Cyclical industries**: Use averages across a full cycle (covering at least one peak and one trough), not a single year
5. **Short listing history**: Companies listed fewer than 5 years — use all available data, but note "limited data window" in results

## Limitations

These indicators eliminate "definitely poor" companies, but passing does not mean "definitely good." Companies that pass still require further research:
- Is the business model sustainable?
- Is management trustworthy?
- Is the current valuation reasonable?
- Is the competitive landscape deteriorating?

Quality screening is the first step, not the last.
