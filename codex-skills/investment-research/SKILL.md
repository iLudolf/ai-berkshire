---
name: investment-research
description: "AI Berkshire skill: Investment Research — Buffett-Munger-Duan Yongping-Li Lu Four Masters comprehensive analysis framework. Source: skills/investment-research.md."
---

## Codex adapter note

This skill is generated from `skills/investment-research.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Investment Research: Buffett-Munger-Duan Yongping-Li Lu Four Masters Comprehensive Analysis Framework

Conduct systematic investment research analysis on $ARGUMENTS.

## Research Framework

Based on the methodologies of the four investment masters — Buffett, Munger, Duan Yongping, and Li Lu — execute the research in the following seven modules in sequence:

### Pre-Step: AI Research Bias Awareness (Must Execute)

Before beginning research, assess the company's "AI researchability" and identify potential data biases:

**Information Richness Rating**:
| Level | Characteristics | AI Research Pitfalls | Response Strategy |
|-------|----------------|---------------------|-------------------|
| A (Information Rich) | Listed for many years, broad analyst coverage, dense media reporting | Consensus too strong; AI output converges with market pricing, limited alpha | Focus on adversarial testing: why wouldn't smart investors buy? What risks are being ignored? |
| B (Information Moderate) | Listed 1–3 years, limited coverage, some data requires estimation | AI may fill gaps with "reasonable assumptions," appearing complete but actually creating false certainty | Label each estimated data point with confidence level; distinguish "evidence-based inference" from "gap-filling" |
| C (Information Scarce) | Recently listed / obscure / emerging market, almost no coverage | AI may be overly conservative due to lack of material, misjudging "hard to see = bad" | Use first-principles questioning (see below) to extract business essence from limited information |

**First-Principles Research Method for Level C Companies**:
When public information is insufficient, do not try to assemble a "seemingly complete" report. Instead, focus on these fundamental questions:
1. Who are the customers? Why do they pay? Are there alternatives?
2. What drives repeat purchases — habit, lock-in, or continuous creation of new value?
3. Could a competitor replicate this business with $1 billion?
4. What key decisions has management made? What do those decisions reveal about their judgment and values?

**Bias Self-Check List** (maintain vigilance throughout the research):
- [ ] Does my sense of "certainty" come from the nature of the business, or from the volume of available data?
- [ ] If the available material on this company were cut in half, would my conclusions change?
- [ ] Does the AI-generated analysis closely mirror market consensus? If so, where is my informational edge?
- [ ] Is there a possibility that "scarce public data but excellent underlying business" is being undervalued?

Record the information richness rating at the beginning of the report and note the distinction between "AI research confidence" and "actual investment conviction" in the final conclusions.

### Step 1: Data Collection

> **Data Source Standards**: See `skills/financial-data.md`. All financial data must come from two independent sources; discrepancies > 1% must be flagged.
> - US stocks: macrotrends (primary) + stockanalysis (secondary)
> - HK stocks: aastocks (primary) + macrotrends ADR (secondary)
> - A-shares: East Money (primary) + CNINFO (secondary)

Use the Task tool to launch a background Agent and collect the following data from the web:

1. Revenue breakdown: most recent fiscal year and last 4 quarters by segment, growth rate, gross margin
2. Financial metrics: 5-year revenue, net income, gross margin, operating margin, free cash flow, cash reserves
3. Competitive landscape: market share, key competitor comparisons
4. Business model and economic moat: sources of core competitive advantage
5. Technical capabilities: core technology stack, R&D investment
6. Management: founder/CEO background, ownership stake, record of key decisions
7. Industry outlook: TAM (Total Addressable Market), growth forecasts
8. Risk factors: geopolitical, regulatory, supply chain, etc.
9. Current valuation: market cap, PE, PS, PEG, EV/Revenue
10. Core arguments from both bulls and bears

#### Data Cross-Validation (Must Execute — Use Financial Rigor Tool)

After data collection, **you must call `tools/financial_rigor.py` to programmatically validate key data points** to eliminate LLM mental arithmetic errors.

**Data points that must be validated**:
- Total shares outstanding (confirm from at least 2 sources: exchange, Yahoo Finance, StockAnalysis, etc.)
- Current share price and market cap (**manually calculate price × shares outstanding and compare against reported market cap to prevent unit errors**)
- Most recent fiscal year revenue and net income (confirm from company annual report + at least 1 third-party source)
- Cash reserves and net cash (cash + short-term investments − total debt; note definitional differences)
- Management ownership stake (distinguish economic interest from voting rights; note dual-class share structures)

**Mandatory Validation Steps (Use Bash to call tools)**:

Step 1 — Market cap verification (precise decimal, not floating-point):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {share_price} --shares {total_shares} --reported {reported_market_cap} --currency {currency}
```

Step 2 — Key data multi-source cross-validation:
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate \
  --field {field_name} --values '{"source1": value, "source2": value}' --unit {unit}
```
Execute separately for revenue, net income, and cash reserves.

Step 3 — Precise valuation metric verification (PE/PB/ROE/FCF Yield, etc.):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {share_price} --eps {EPS} --bvps {book_value_per_share} --fcf-per-share {FCF_per_share} --dividend {dividend_per_share}
```

**Validation Rules**:
1. Each key data point must have at least 2 independent sources
2. When discrepancies between sources are found, prioritize company annual reports/exchange data and note the reason for the discrepancy
3. **All data involving calculations must be verified via the tool — LLM mental arithmetic is prohibited**
4. Tool output results should be embedded directly in the report appendix under "Key Data Cross-Validation Records"
5. If the tool reports ❌ excessive deviation, the cause must be investigated before proceeding with analysis

**Common Error Prevention**:
- Market cap units: HKD hundreds of millions vs. CNY hundreds of millions vs. USD hundreds of millions — easy to drop or add a zero
- FCF definition: different sources may define capex differently (whether to include leases, acquisitions, etc.)
- Debt definition: whether operating lease liabilities are included
- Ownership stake: economic interest ≠ voting rights in dual-class share companies

### Step 2: Business Essence Analysis — Duan Yongping's "Right Business"

Analysis points:
- Define the essence of this business in one sentence
- Revenue structure breakdown (chart)
- 5-year profitability trend (chart)
- Business model canvas: one-time sales vs. subscription/repeat purchase? Hardware vs. software vs. platform?
- Ecosystem stickiness / customer lock-in strength
- Gross margin level vs. peers — explain why it is high or low
- Operating leverage analysis
- **Duan Yongping's probing question**: What makes this business good? If you could describe it in one sentence, what would it be?

### Step 3: Economic Moat Assessment — Buffett's "Economic Moat"

Verify each of the five moat types:

| Moat Type | Verification Method |
|-----------|---------------------|
| Brand / Pricing Power | Can prices be raised without losing sales volume? |
| Switching Costs | How high is the cost for customers to switch to competitors? |
| Network Effects | Does the product improve as more users join? |
| Scale Advantages | How significant is the cost advantage from scale? |
| Technology / Patent Barriers | How many years ahead technologically? Can it be replicated? |

Analyze moat trend: Has it widened or narrowed over the past 5 years? Forecast for the next 5 years.

**Buffett's probing question**: Will this moat still exist in 10 years? What could destroy it?

### Step 4: Inversion Thinking and Risk Checklist — Munger's "Think It Through Backwards"

- List "all paths by which this company could fail" (table: path / probability / severity)
- Historical analogy: find companies that were in similar positions historically — what happened to them?
- Interdisciplinary analysis: cross-validate using network effects theory, technology adoption curves, competitive game theory, and other models
- Bias self-check: narrative bias, anchoring effect, survivorship bias
- Collect the bear case's core arguments

**Munger's probing question**: Where am I most likely to be wrong? Why would a smart person not buy or even short this company?

### Step 5: Management Assessment — Duan Yongping's "Right People" + Buffett's "Management Integrity"

- Post-mortem review of key CEO/founder decisions (table: date / decision / outcome / score)
- Capital allocation ability: R&D return rate, M&A success rate, buyback timing
- Alignment with shareholder interests: management ownership, compensation structure, insider selling records
- Organizational capability: team stability, key personnel risk
- Corporate culture characteristics

**Duan Yongping's probing question**: If the CEO retired, could this company maintain its competitiveness?

### Step 6: Industry and Civilizational Trends — Li Lu's "Civilizational Evolution Framework"

- Determine whether the industry is undergoing a "civilization-level paradigm shift"
- Historical technology revolution analogies (steam engine / electricity / internet / AI)
- TAM growth curve and ceiling analysis
- Company's position in the industry value chain
- Technology roadmap risks
- Customer / supplier concentration analysis

**Li Lu's probing question**: Looking back from 20 years from now, will this company be "the Standard Oil of this era" or "a flash-in-the-pan 3Com"?

### Step 7: Valuation and Margin of Safety — Buffett's "Intrinsic Value" + Duan Yongping's "Right Price"

- Current market pricing (key valuation metrics table) — **must be verified via tool**
- Reverse DCF: what growth expectations are implied by the current share price?
- Three-scenario valuation — **must be calculated precisely via tool; mental arithmetic prohibited**:
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {share_price} --eps {EPS} --shares {total_shares_in_hundreds_of_millions} \
  --growth {bull_growth_rate} {base_growth_rate} {bear_growth_rate} \
  --pe {bull_PE} {base_PE} {bear_PE} --years 3 --currency {currency}
```
- Compare against historical valuation
- Compare against peer valuation

**Duan Yongping's probing question**: If the stock market closed for 5 years tomorrow, would you be willing to hold at this price?

### Step 8: Comprehensive Decision Memo

Summary table:

| Dimension | Conclusion | Confidence |
|-----------|-----------|------------|
| Business Quality (Duan Yongping) | | |
| Economic Moat (Buffett) | | |
| Management (Duan Yongping + Buffett) | | |
| Greatest Risk (Munger) | | |
| Civilizational Trend (Li Lu) | | |
| Valuation (Buffett + Duan Yongping) | | |

Final decision table:

| Strategy | Recommendation |
|----------|---------------|
| No position | |
| Current position holders | |
| Sell signal | |
| Add signal | |

Simulated commentary from the four masters (in quote format).

## Output Requirements

1. All analysis must be data-supported with sources cited
2. Use Markdown tables to present key data
3. Each module must end with the corresponding master's "probing question"
4. Write the complete final report to `~/[CompanyName]-investment-research-report.md`
5. Conclusions must be clear — do not avoid giving a buy / hold / avoid recommendation
6. The valuation section must provide a specific price range
7. **The beginning of the report** must include the "Information Richness Rating" (A/B/C) and an "AI Research Limitations Statement"
8. **The end of the report** must distinguish "AI analysis confidence" from "investment conviction" — the former depends on the volume of available data; the latter depends on business fundamentals. Clearly inform readers which conclusions are based on sufficient data and which are based on reasoning from limited information
9. If the company is Level C (information scarce), the report must end with a "List of Questions Requiring Primary Research Verification" — recommending readers supplement AI blind spots through field research, product experience, supply chain interviews, etc.

## Data Spot-Check (Release Gate Process)

After writing the report to file, you **must** perform a data spot-check and pass before publishing:

**Step 1 — Extract spot-check list (15% random sample):**
```bash
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report_file_path>
```
Outputs a JSON template; each item contains `fetched_value` (to be filled in).

**Step 2 — Retrieve and verify data:**
For each data point in the list, retrieve data from reliable sources per `skills/financial-data.md` standards
(US stocks: macrotrends + stockanalysis; HK stocks: aastocks + macrotrends; A-shares: East Money + CNINFO),
and fill in `fetched_value` / `fetched_source` / `fetched_value2` / `fetched_source2`.

**Step 3 — Output verdict:**
```bash
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed_JSON>' \
  --report <report_file_name>
```

- **[PASS]**: All spot-checked points have deviation ≤ 1% → report may be published
- **[REJECT]**: Any point has deviation > 1% → correct the relevant data and re-run the spot-check until it passes
