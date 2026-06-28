---
name: investment-checklist
description: "AI Berkshire skill: Buffett value investing pre-buy Checklist. Source: skills/investment-checklist.md."
---

## Codex adapter note

This skill is generated from `skills/investment-checklist.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Buffett Value Investing Pre-Buy Checklist

Run the Buffett value investing pre-buy Checklist analysis on $ARGUMENTS.

**Supported input formats**: Single or multiple companies, separated by commas/spaces. Example: `Tencent, Moutai, Nvidia` or `NVDA AAPL MSFT`

## Execution Flow

### Step 1: Parse Input, Identify All Companies to Analyze

Parse all company names/tickers from $ARGUMENTS. For each company, determine:
- Full company name, ticker symbol, listing exchange
- If the company is not publicly listed, mark as "not listed" with a brief note (whether indirect investment routes exist), and skip the full Checklist

### Step 1.5: AI Research Bias Warning

Assign a quick "information richness" rating (A/B/C) for each company and note it in the report:

| Grade | Criteria | Impact on Checklist |
|-------|----------|---------------------|
| A | Listed for many years, data abundant | Execute normally, but beware the "consensus trap" — all indicators looking clear does not mean true certainty |
| B | Limited data, estimation required | Label confidence level on each estimated indicator; weight "good business" judgment by data reliability |
| C | Information extremely scarce | Do not force-fill the six-gate table; honestly mark "insufficient data, unable to judge"; focus on verifiable core questions |

**Core principle**: The Checklist's goal is to **eliminate bad choices**. For Grade C companies, "insufficient data" does not equal "fail" nor "pass" — honestly label as "gray area, first-hand information needed" rather than rejecting because the AI cannot fill the table.

Duan Yongping said: "Can't understand" comes in two forms — one where the business is genuinely too complex, and one where you simply haven't spent enough time looking. AI research tends to confuse "scarce data" with "can't understand."

### Step 2: Parallel Data Collection

Use the Task tool to launch an independent background Agent for **each company** (all companies launch simultaneously in parallel). Each Agent collects:

1. **Profitability**: ROE (5–10 year trend), gross margin, net margin, free cash flow
2. **Valuation data**: Current price, market cap, PE (TTM), forward PE, PB, dividend yield
3. **Growth trend**: Revenue/profit growth over the past 3 years
4. **Financial health**: Debt levels, capex requirements, cash reserves, net cash/net debt
5. **Competitive landscape**: Market share, main competitors, share change trends
6. **Moat evidence**: Specific evidence of brand/switching costs/network effects/scale advantages/technology barriers
7. **Management track record**: CEO background, key decisions, shareholding, capital allocation record
8. **Latest developments**: Major events in the past 6 months (earnings, M&A, regulation, management changes, etc.)

### Step 3: Execute the Six-Gate Checklist for Each Company

For each listed company, work through the six gates in sequence:

---

#### Gate 1: Do I Understand This Business? (Circle of Competence)

Must answer:
- [ ] Can I explain in one sentence how this company makes money?
- [ ] What business will it most likely still be doing in 10 years?
- [ ] What are the key variables that determine success or failure?
- [ ] Is my knowledge of this industry from deep research or hearsay?

**Scoring criteria** (★1–5):
- ★★★★★: Business model extremely simple and clear, high 10-year certainty (e.g., Moutai: brewing and selling liquor)
- ★★★★☆: Model is clear but has a technical threshold requiring some expertise to understand
- ★★★☆☆: Model is understandable but 10-year certainty is low, industry changes fast
- ★★☆☆☆: Business lines are complex or industry is in upheaval, hard to predict the future
- ★☆☆☆☆: Completely outside my circle of competence

**Hard veto**: If I cannot explain how the company makes money, mark it as "outside circle of competence, no analysis" immediately.

---

#### Gate 2: Is This a Good Business? (Economic Characteristics)

Let the data speak — **key metrics must be calculated precisely using tools**:

```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {price} --eps {EPS} --bvps {book value per share} --fcf-per-share {FCF per share} --dividend {dividend per share}
```

| Metric | Company Value | Reference Standard | Judgment |
|--------|--------------|-------------------|----------|
| ROE (5-year average) | | >15% good, >20% excellent | |
| Gross margin | | >40% implies pricing power | |
| Free cash flow | | Consistently positive, ≈ net income | |
| Capex intensity | | Asset-light preferred over asset-heavy | |
| Debt level | | Interest-bearing debt / net income < 3 years | |

**Scoring criteria** (★1–5):
- ★★★★★: ROE>25%, high gross margin, strong FCF, asset-light, low debt (all met)
- ★★★★☆: 4 criteria met
- ★★★☆☆: 3 criteria met
- ★★☆☆☆: 2 criteria met or trend deteriorating
- ★☆☆☆☆: Most criteria not met or FCF consistently negative

---

#### Gate 3: Is the Moat Deep Enough? (Competitive Advantage)

Check each item:

| Moat Type | Present? | Specific Evidence | Widening or Narrowing? |
|-----------|----------|------------------|----------------------|
| Brand / pricing power | | | |
| Switching costs | | | |
| Network effects | | | |
| Cost / scale advantages | | | |
| Technology / patent barriers | | | |

Additional test: If a competitor were given $10 billion, could they replicate this business?

**Scoring criteria** (★1–5):
- ★★★★★: Multiple moats stacked and widening
- ★★★★☆: At least one strong moat and stable
- ★★★☆☆: Moat exists but not deep enough, or trend unclear
- ★★☆☆☆: Moat is being eroded
- ★☆☆☆☆: No obvious moat

---

#### Gate 4: Is Management Trustworthy? (The Human Factor)

| Check Item | Assessment |
|------------|-----------|
| Honesty (promises vs. delivery) | |
| Capital allocation skill (buyback/dividend/M&A record) | |
| Shareholder-oriented (shareholding, compensation) | |
| Owner mindset (founder vs. hired professional manager) | |
| Corporate governance (related-party transactions, goodwill, audits) | |
| Can the company run normally if the CEO leaves? | |

**Scoring criteria** (★1–5):
- ★★★★★: Founder at the helm, excellent capital allocation, interests fully aligned
- ★★★★☆: Management excellent but with minor flaws
- ★★★☆☆: Management adequate but with governance risks
- ★★☆☆☆: Integrity or governance issues present
- ★☆☆☆☆: Serious integrity issues (→ hard veto)

---

#### Gate 5: Is the Price Cheap Enough? (Margin of Safety)

| Metric | Value | Historical Percentile | Judgment |
|--------|-------|-----------------------|----------|
| PE (TTM) | | | |
| Forward PE | | | |
| PB | | | |
| Dividend yield | | | |
| FCF Yield | | | |

Additional test (**must use tools for precise calculation — no mental math**):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {price} --eps {EPS} --shares {shares in hundreds of millions} \
  --growth {optimistic} {neutral} {pessimistic} --pe {optimistic PE} {neutral PE} {pessimistic PE} --currency {currency}
```
- Valuation range under three scenarios (use tool output)
- If the analysis is wrong, how much at most can be lost buying at the current price?
- If the stock price drops 50%, would I dare to add?

**Scoring criteria** (★1–5):
- ★★★★★: Below 50% of intrinsic value, extreme margin of safety
- ★★★★☆: 70% of intrinsic value, good margin of safety
- ★★★☆☆: Fair valuation, average margin of safety
- ★★☆☆☆: Somewhat expensive, insufficient margin of safety
- ★☆☆☆☆: Severely overvalued

---

#### Gate 6: Position Sizing & Decision Discipline (Preventing Emotional Mistakes)

Check the following emotional signals:
- Am I buying because of FOMO?
- Am I buying only because someone recommended it?
- Could I accept if the stock were halted for 5 years?
- Can I write out the buy thesis in under 200 words?

---

### Step 4: Mirror Test

Write a mirror test statement for each company:

> "I am buying ___ company at ___ per share because:
> 1. The essence of this business is ___, and I understand it;
> 2. Its moat is ___, and it is widening / narrowing;
> 3. Management ___, and is / is not trustworthy;
> 4. The current price is equivalent to ___ % of intrinsic value, with / without sufficient margin of safety;
> 5. Even if I'm wrong, the downside risk is controllable / uncontrollable because ___."

**If all 5 sentences cannot be completed = do not buy.** Clearly mark "Pass" or "Fail."

---

### Step 5: Quick Veto Checklist

Check each item for every company — triggering any one item marks it as "vetoed":

- [ ] Cannot explain how this company makes money
- [ ] Free cash flow has been negative for 3 consecutive years with no improvement in sight
- [ ] Management has integrity blemishes
- [ ] Competitive advantage is being irreversibly eroded
- [ ] Profits depend on "the next buyer paying a higher price" (greater fool theory)
- [ ] Cannot afford the consequence of this investment going to zero
- [ ] Buy reason is mainly "everyone is buying" or "it's been rising lately"
- [ ] Cannot write out the buy thesis in under 200 words

---

### Step 6: Output Summary Comparison Table (Required When Analyzing Multiple Companies)

When analyzing multiple companies, a comparison overview table must be generated:

| Company | Checklist Pass? | Circle of Competence | Good Business | Moat | Management | Margin of Safety | Core Conclusion |
|---------|----------------|----------------------|---------------|------|------------|-----------------|----------------|
| | | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | |

---

### Step 7: Final Conclusion and Write to File

Give a clear conclusion for each company (no hedging):
- ✅ **Passed Checklist** (X/6 gates) — ready to proceed to deep research
- ❌ **Failed Checklist** — state which red line was triggered
- ❓ **Gray Area** — state what the key dispute is, and what the investor needs to judge for themselves
- N/A — not listed / cannot be purchased

Write the complete report to `~/Buffett-Checklist-[company name or "multi-company-comparison"].md`

## Output Format Requirements

1. Each company in its own section, including: six-gate scoring table + core data table + key risks (3–5 items) + mirror test + clear conclusion
2. For multiple companies, append a summary comparison table at the end
3. All scores must use the ★ symbol (★1–5), no half stars
4. Data must note source and date; estimated values must be labeled "estimated"
5. Conclude with a closing remark echoing Buffett's quote: "The first rule of investing is not to lose money"
6. Style: direct, sharp, no filler. Intersperse quotes from Buffett / Munger / Duan Yongping / Li Lu

## Key Principles

- **Better to miss than to make a mistake**: The Checklist's goal is to eliminate bad choices, not to find the best one
- **Be honest about your circle of competence**: If you don't understand it, say so — don't force the analysis
- **Margin of safety is the lifeline**: Even a great company bought at the wrong price will lose money
- **The mirror test cannot be skipped**: If you can't articulate the reason, don't buy — no exceptions
