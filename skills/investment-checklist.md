# Buffett Value Investing Pre-Purchase Checklist

Run a Buffett value investing pre-purchase Checklist analysis on $ARGUMENTS.

**Supported input formats**: Single or multiple companies, separated by commas / Chinese enumeration marks / spaces. Example: `Tencent, Moutai, Nvidia` or `NVDA AAPL MSFT`

## Execution Flow

### Step 1: Parse Input and Identify All Companies to Analyze

Parse all company names / ticker symbols from $ARGUMENTS. For each company, determine:
- Full company name, ticker symbol, listing exchange
- If the company is not publicly listed, mark as "Not Listed" and provide a brief note (whether indirect investment routes exist), then skip the full Checklist

### Step 1.5: AI Research Bias Warning

Perform a quick "information richness" rating (A/B/C) for each company and annotate in the report:

| Grade | Criteria | Impact on Checklist |
|-------|----------|---------------------|
| A | Listed for many years, data is abundant | Execute normally, but beware of "consensus trap" — all indicators looking clear does not mean true certainty |
| B | Limited data, requires estimation | Annotate each estimated indicator with confidence level; weight "good business" judgment against data reliability |
| C | Extremely scarce information | Do not force-fill the six-gate table; honestly annotate "insufficient data, cannot judge"; focus on verifiable core questions |

**Core principle**: The Checklist's goal is to **eliminate bad choices**. For Grade C companies, "insufficient data" does not equal "failed" nor "passed" — honestly annotate as "gray area, requires first-hand information to supplement" rather than rejecting because the AI cannot fill the table.

Duan Yongping once said: "Cannot understand" comes in two forms — one is a business genuinely too complex to understand, the other is that you haven't spent the time to look. The limitation of AI research is that it easily conflates "scarce data" with "cannot understand."

### Step 2: Parallel Data Collection

Use the Task tool to launch an independent background Agent for **each company** to collect data (all companies launched simultaneously in parallel). Each Agent is responsible for collecting:

1. **Profitability**: ROE (5–10 year trend), gross margin, net margin, free cash flow
2. **Valuation data**: Current share price, market cap, PE (TTM), forward PE, PB, dividend yield
3. **Growth trends**: Revenue / earnings growth over the past 3 years
4. **Financial health**: Debt levels, CapEx requirements, cash reserves, net cash / net debt
5. **Competitive landscape**: Market share, key competitors, share trend changes
6. **Economic moat evidence**: Specific evidence of brand / switching costs / network effects / scale advantages / technology barriers
7. **Management track record**: CEO background, key decisions, shareholding, capital allocation record
8. **Latest developments**: Major events in the past 6 months (earnings, M&A, regulatory, management changes, etc.)

### Step 3: Execute the Six-Gate Checklist Company by Company

For each listed company, go through six gates in order:

---

#### Gate 1: Do I Understand This Business? (Circle of Competence)

Must answer:
- [ ] Can you explain in one sentence how this company makes money?
- [ ] With high probability, what business will it still be doing in 10 years?
- [ ] What are the key variables that determine success or failure?
- [ ] Is your understanding of this industry based on deep research or hearsay?

**Scoring criteria** (★1–5):
- ★★★★★: Business model is extremely simple and clear; 10-year certainty is high (e.g., Moutai: brew and sell liquor)
- ★★★★☆: Model is clear but has a technical threshold; requires some domain knowledge to understand
- ★★★☆☆: Model is understandable but 10-year certainty is low; industry changes fast
- ★★☆☆☆: Business lines are complex or the industry is in upheaval; future is hard to predict
- ★☆☆☆☆: Completely outside the circle of competence

**Hard veto**: If you cannot explain how it makes money, immediately mark as "Outside circle of competence — no analysis."

---

#### Gate 2: Is This a Good Business? (Economic Characteristics)

Let data do the talking — **key metrics must be calculated precisely using tools**:

```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
  --price {share price} --eps {EPS} --bvps {book value per share} --fcf-per-share {FCF per share} --dividend {dividend per share}
```

| Metric | Company Value | Reference Standard | Judgment |
|--------|--------------|-------------------|----------|
| ROE (5-year average) | | >15% excellent, >20% exceptional | |
| Gross margin | | >40% implies pricing power | |
| Free cash flow | | Consistently positive, ≈ net income | |
| CapEx intensity | | Asset-light beats asset-heavy | |
| Debt level | | Interest-bearing debt / net income < 3 years | |

**Scoring criteria** (★1–5):
- ★★★★★: ROE >25%, high gross margin, strong FCF, asset-light, low debt (all criteria met)
- ★★★★☆: 4 criteria met
- ★★★☆☆: 3 criteria met
- ★★☆☆☆: 2 criteria met or trend deteriorating
- ★☆☆☆☆: Most criteria not met or FCF consistently negative

---

#### Gate 3: Is the Economic Moat Deep Enough? (Competitive Advantage)

Check each item:

| Moat Type | Present? | Specific Evidence | Widening or Narrowing? |
|-----------|----------|------------------|------------------------|
| Brand / pricing power | | | |
| Switching costs | | | |
| Network effects | | | |
| Cost / scale advantages | | | |
| Technology / patent barriers | | | |

Additional test: If you gave a competitor $10 billion, could they replicate this business?

**Scoring criteria** (★1–5):
- ★★★★★: Multiple moats stacked and widening
- ★★★★☆: At least one strong moat and stable
- ★★★☆☆: Moat exists but not deep enough, or trend is unclear
- ★★☆☆☆: Moat is being eroded
- ★☆☆☆☆: No obvious economic moat

---

#### Gate 4: Is Management Trustworthy? (The Human Factor)

| Check Item | Assessment |
|------------|-----------|
| Integrity (promises vs. delivery) | |
| Capital allocation ability (buyback / dividend / M&A track record) | |
| Shareholder-oriented (shareholding, compensation) | |
| Owner mindset (founder vs. professional manager) | |
| Corporate governance (related-party transactions, goodwill, audit) | |
| Can it operate normally after the CEO leaves? | |

**Scoring criteria** (★1–5):
- ★★★★★: Founder at the helm, exceptional capital allocation, interests fully aligned
- ★★★★☆: Excellent management with minor flaws
- ★★★☆☆: Competent management but with governance concerns
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

Additional test (**must be calculated precisely using tools — mental math is prohibited**):
```bash
python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
  --price {share price} --eps {EPS} --shares {shares in hundreds of millions} \
  --growth {bull} {base} {bear} --pe {bull PE} {base PE} {bear PE} --currency {currency}
```
- Valuation range under three scenarios (use tool output)
- If your judgment is wrong, what is the maximum loss at the current price?
- If the share price is cut in half, would you dare to add to your position?

**Scoring criteria** (★1–5):
- ★★★★★: Below 50% of intrinsic value — extreme margin of safety
- ★★★★☆: 70% of intrinsic value — good margin of safety
- ★★★☆☆: Fair valuation, average margin of safety
- ★★☆☆☆: Somewhat expensive, insufficient margin of safety
- ★☆☆☆☆: Severely overvalued

---

#### Gate 6: Position Sizing and Decision Discipline (Preventing Emotional Breakdown)

Check the following emotional signals:
- Are you buying because of FOMO?
- Are you buying because someone recommended it?
- If it were suspended for 5 years, could you accept that?
- Can you write out your buy thesis in under 200 words?

---

### Step 4: Mirror Test

Write a mirror test statement for each company:

> "I am buying ___ Company at ___ per share, because:
> 1. The essence of this business is ___, and I understand it;
> 2. Its economic moat is ___, and it is widening / narrowing;
> 3. Management ___, is / is not trustworthy;
> 4. The current price represents ___% of intrinsic value, with / without sufficient margin of safety;
> 5. Even if I am wrong, the downside risk is manageable / unmanageable, because ___."

**If you cannot complete all 5 sentences = do not buy.** Explicitly annotate "Passed" or "Not Passed."

---

### Step 5: Quick Veto Checklist

Check each item for every company; if any one is triggered, immediately annotate as "Vetoed":

- [ ] Cannot explain how this company makes money
- [ ] Free cash flow has been negative for 3 consecutive years with no sign of improvement
- [ ] Management has an integrity blemish
- [ ] Competitive advantage is being irreversibly eroded
- [ ] Requires "the next greater fool to pay a higher price" to profit (momentum speculation)
- [ ] Cannot accept the consequence of this investment going to zero
- [ ] The primary buy reason is "everyone is buying" or "it has been performing well recently"
- [ ] Cannot write out the buy thesis in under 200 words

---

### Step 6: Summary Comparison Table (Required for Multiple Companies)

When analyzing multiple companies, a comparison summary table must be generated:

| Company | Checklist Passed? | Circle of Competence | Good Business | Economic Moat | Management | Margin of Safety | Core Conclusion |
|---------|-------------------|----------------------|---------------|---------------|------------|-----------------|----------------|
| | | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | ★☆☆☆☆ | |

---

### Step 7: Final Conclusion and Write to File

Give a clear conclusion for each company (no hedging):
- ✅ **Checklist Passed** (X/6 gates) — Ready to enter the deep research phase
- ❌ **Checklist Not Passed** — State which red line was triggered
- ❓ **Gray Area** — State what the key point of contention is and what the investor needs to judge for themselves
- N/A — Not listed / cannot be purchased

Write the complete report to `~/Buffett-Checklist-[company name or "multi-company-comparison"].md`

## Output Format Requirements

1. Each company gets its own section, including: six-gate scoring table + core data table + key risks (3–5 items) + mirror test + explicit conclusion
2. For multiple companies, append a summary comparison table at the end
3. All ratings must use the ★ symbol (★1–5), no half stars
4. Data must be annotated with source date; estimated values must be noted as "estimated"
5. End with a closing remark echoing Buffett's quote: "The first rule of investing is not to lose money"
6. Language style: direct, sharp, no filler. Intersperse quotes from Buffett / Munger / Duan Yongping

## Core Principles

- **Better to miss than to err**: The Checklist's goal is to eliminate bad choices, not to find the best one
- **Be honest about your circle of competence**: If you don't understand it, say so — don't force the analysis
- **Margin of safety is the lifeline**: Even a great company bought at too high a price will lose money
- **The mirror test cannot be skipped**: If you cannot articulate the reason, do not buy — no exceptions
