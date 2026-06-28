# Investment Research: Four Masters Integrated Analysis Framework

Run systematic investment research analysis on $ARGUMENTS.

## Research Framework

Based on the methodologies of Buffett, Munger, Duan Yongping, and Li Lu, execute the research in the following seven modules in order.

### Pre-Step: AI Research Bias Awareness (Mandatory)

Before starting the research, evaluate the company's "AI researchability" and identify potential data biases:

**Information Richness Rating**:
| Rating | Characteristics | AI Research Pitfall | Mitigation Strategy |
|--------|----------------|--------------------|--------------------|
| A (Information-rich) | Long-listed, wide broker coverage, dense media reporting | Consensus too strong; AI output converges with market pricing, limited alpha | Focus on adversarial testing: why don't smart people buy? What risks are being ignored? |
| B (Moderate information) | Listed 1-3 years, limited coverage, some data requires estimation | AI may fill gaps with "reasonable guesses," appearing complete but falsely certain | Annotate confidence level on every estimated data point; distinguish "evidence-based estimates" from "made-up filler" |
| C (Information-scarce) | Newly listed / niche / emerging market, almost no coverage | AI may be excessively conservative due to limited data, misreading "hard to see = not good" | Use first-principles questions (see below); extract business essence from limited information |

**First-principles research approach for C-rated companies**:
When public information is insufficient, do not try to assemble a "seemingly complete" report. Instead, focus on these fundamental questions:
1. Who are the customers? Why do they pay? Are there alternatives?
2. What drives repeat purchases — habit, lock-in, or continuous new value creation?
3. Could a competitor replicate this business with $1 billion?
4. What key decisions has management made? What judgment and values do those decisions reflect?

**Bias self-check list** (maintain vigilance throughout the research):
- [ ] Is my sense of "certainty" coming from the business fundamentals, or from the volume of information?
- [ ] If I cut this company's available information in half, would my conclusion change?
- [ ] Is the AI-generated analysis highly similar to market consensus? If so, where is my information edge?
- [ ] Is there a possibility being underestimated that "little public data but an excellent business model"?

Include the information richness rating at the start of the report; at the end, distinguish between "AI research confidence" and "actual investment certainty."

### Step 1: Data Collection

> **Data source protocol**: See `skills/financial-data.md`. All financial data must come from two independent sources; deviations > 1% must be flagged.
> - US stocks: Macrotrends (primary) + Stock Analysis (secondary)
> - HK stocks: AAStocks (primary) + Macrotrends ADR (secondary)
> - A-shares: Eastmoney (primary) + CNINFO (secondary)

Launch a background agent via the Task tool to collect the following data from the web:

1. Revenue structure: Most recent fiscal year and last 4 quarters' segment revenues, growth rates, gross margins
2. Financial metrics: Past 5 years' revenue, net income, gross margin, operating margin, free cash flow, cash reserves
3. Competitive landscape: Market share, key competitor comparisons
4. Business model and moat: Sources of core competitive advantage
5. Technology capability: Core tech stack, R&D spending
6. Management: Founder/CEO background, ownership stake, key decision track record
7. Industry outlook: TAM (total addressable market), growth forecasts
8. Risk factors: Geopolitical, regulatory, supply chain, etc.
9. Current valuation: Market cap, PE, PS, PEG, EV/Revenue
10. Core bull and bear arguments

#### Data Cross-Validation (Mandatory — use the financial rigor tool)

After data collection, **must call `tools/financial_rigor.py` to programmatically validate key data** to eliminate LLM mental math errors.

**Data points that must be verified**:
- Total shares outstanding (confirmed from at least 2 sources: exchange, Yahoo Finance, Stock Analysis, etc.)
- Current price and market cap (**manually calculate price × shares and compare with reported market cap to catch unit errors**)
- Most recent fiscal year revenue and net income (confirmed from company annual report + at least 1 third-party source)
- Cash reserves and net cash (cash + short-term investments − total debt; watch for scope differences)
- Management ownership stake (distinguish economic interest from voting rights; note dual-class share structures)

**Mandatory verification steps (use Bash to call the tool)**:

Step 1 — Market cap verification (decimal-precise, not floating-point):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {price} --shares {shares} --reported {reported_market_cap} --currency {currency}
```

Step 2 — Key data multi-source cross-validation:
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field {field_name} --values '{"Source1": value, "Source2": value}' --unit {unit}
```
Run separately for revenue, net income, and cash reserves.

Step 3 — Precise valuation metric verification (PE/PB/ROE/FCF Yield, etc.):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {price} --eps {EPS} --bvps {book_value_per_share} --fcf-per-share {FCF_per_share} --dividend {dividend_per_share}
```

**Verification rules**:
1. At least 2 independent sources for each key data point
2. When sources disagree, prioritize company annual report / exchange data; note the reason for the discrepancy
3. **All data involved in calculations must be verified by the tool — LLM mental math is forbidden**
4. Tool output results embedded directly into the report appendix "Key Data Cross-Validation Record"
5. If the tool reports ❌ deviation too large, investigate the cause before proceeding

**Common error prevention**:
- Market cap units: HKD billions vs. CNY billions vs. USD billions — easy to misplace a zero
- FCF definition: different sources may define capex differently (include/exclude lease payments, acquisitions, etc.)
- Debt scope: whether operating lease liabilities are included
- Ownership stake: for dual-class share companies, economic interest ≠ voting rights

### Step 2: Business Nature Analysis — Duan Yongping's "Right Business"

Key analysis points:
- Define the essence of this business in one sentence
- Revenue structure breakdown (table)
- 5-year profitability trend (table)
- Business model canvas: one-time sale vs. subscription/repeat? Hardware vs. software vs. platform?
- Ecosystem stickiness / customer lock-in strength
- Gross margin level vs. peer comparison, explain why it's high/low
- Operating leverage analysis
- **Duan Yongping's follow-up question**: What's great about this business? If you had to describe it in one sentence, what would it be?

### Step 3: Moat Assessment — Buffett's "Economic Moat"

Verify each of the five moat types one by one:

| Moat Type | Verification Method |
|-----------|---------------------|
| Brand / pricing power | Can they raise prices without losing volume? |
| Switching costs | How costly is it for customers to move to a competitor? |
| Network effects | Does the product get better as more users join? |
| Scale economies | How large are the cost advantages from scale? |
| Technology / patent barriers | How many years ahead? Can it be replicated? |

Analyze moat trend: has it widened or narrowed over the past 5 years? Forecast for the next 5 years.

**Buffett's follow-up question**: Will this moat still exist in 10 years? What could destroy it?

### Step 4: Reverse Thinking and Risk Checklist — Munger's "Think It Through Backwards"

- List "all the paths this company could fail" (table: path / probability / impact severity)
- Historical analogies: find companies that were in a similar position historically; how did they end up?
- Cross-disciplinary analysis: cross-validate using network effects theory, technology adoption curves, competitive game theory, etc.
- Bias self-check: narrative bias, anchoring effect, survivorship bias
- Collect the core bear arguments

**Munger's follow-up question**: Where am I most likely to be wrong? Why would smart people not buy / sell short this company?

### Step 5: Management Assessment — Duan Yongping's "Right People" + Buffett's "Management Integrity"

- CEO/founder key decisions post-mortem (table: date / decision / outcome / score)
- Capital allocation capability: R&D ROI, M&A success rate, buyback timing
- Shareholder interest alignment: management ownership, compensation structure, insider selling record
- Organizational capability: team stability, key talent risks
- Corporate culture characteristics

**Duan Yongping's follow-up question**: If the CEO retired tomorrow, could this company maintain its competitiveness?

### Step 6: Industry and Civilization Trends — Li Lu's "Civilization Evolution Framework"

- Assess whether the industry is in a "civilization-level paradigm shift"
- Historical technology revolution analogies (steam engine / electricity / internet / AI)
- TAM growth curve and ceiling analysis
- Company's position in the industry value chain
- Technology path risks
- Customer / supplier concentration analysis

**Li Lu's follow-up question**: Looking back from 20 years in the future, will this company be "the Standard Oil of its era" or "a flash-in-the-pan 3Com"?

### Step 7: Valuation and Margin of Safety — Buffett's "Intrinsic Value" + Duan Yongping's "Right Price"

- Current market pricing (key valuation metrics table) — **must be verified by the tool**
- Reverse DCF: what growth expectations are implied in the current price?
- Three-scenario valuation — **must be precisely calculated by the tool; mental math is forbidden**:
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {price} --eps {EPS} --shares {shares_in_billions} \
  --growth {optimistic_growth} {neutral_growth} {pessimistic_growth} \
  --pe {optimistic_PE} {neutral_PE} {pessimistic_PE} --years 3 --currency {currency}
```
- Comparison with historical valuation
- Comparison with peer valuations

**Duan Yongping's follow-up question**: If the stock market closed for 5 years tomorrow, would you be willing to hold at this price?

### Step 8: Comprehensive Decision Memo

Summary table:

| Dimension | Conclusion | Confidence |
|-----------|-----------|-----------|
| Business quality (Duan Yongping) | | |
| Moat (Buffett) | | |
| Management (Duan Yongping + Buffett) | | |
| Biggest risk (Munger) | | |
| Civilization trend (Li Lu) | | |
| Valuation (Buffett + Duan Yongping) | | |

Final decision table:

| Strategy | Recommendation |
|----------|---------------|
| No position | |
| Current holder | |
| Sell signal | |
| Add signal | |

Simulated commentary from each of the four masters (in quote format).

## Output Requirements

1. All analysis must be data-backed, with data sources cited
2. Use Markdown tables for key data
3. Every module must end with the corresponding master's "follow-up question"
4. Save the complete report to `~/[company_name]-investment-research.md`
5. Conclusions must be clear — do not shy away from giving a buy / wait / avoid recommendation
6. The valuation section must give a specific price range
7. **Report opening** must include an "Information Richness Rating" (A/B/C) and "AI Research Limitations Disclaimer"
8. **Report closing** must distinguish "AI analysis confidence" from "investment certainty" — the former depends on data volume; the latter depends on business fundamentals. Explicitly tell the reader: which conclusions are based on adequate data, and which are based on reasoning from limited information
9. If the company is C-rated (information-scarce), the report must end with a "Questions Requiring First-Hand Verification" checklist — recommending the reader supplement AI blind spots through field research, product trials, supply chain interviews, etc.

## Data Audit (Publication Gate)

After writing the report to file, **must** execute the data audit before publishing:

**Step 1 — Extract audit checklist (15% random sampling)**:
```bash
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report_file_path>
```
Outputs a JSON template; each item contains `fetched_value` (to be filled in).

**Step 2 — Verify each data point**:
For each data point in the checklist, retrieve values from reliable sources per `skills/financial-data.md`
(US stocks: Macrotrends + Stock Analysis; HK stocks: AAStocks + Macrotrends; A-shares: Eastmoney + CNINFO),
fill in `fetched_value` / `fetched_source` / `fetched_value2` / `fetched_source2`.

**Step 3 — Output verdict**:
```bash
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<filled_JSON>' \
  --report <report_filename>
```

- **[PASS]**: All audit points deviate ≤ 1% → report may be published
- **[REJECT]**: Any point deviates > 1% → correct the relevant data and re-audit until passing
