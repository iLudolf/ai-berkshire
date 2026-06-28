# Investment Thesis Tracker: The Discipline System After You Buy

Run investment thesis tracking on $ARGUMENTS.

**Supported input formats**:
- `Company name` — Establish an investment thesis on first use; run a tracking check on subsequent uses
- `Company name establish-thesis` — Force a fresh thesis to be created
- `Company name quarterly-check` — Run a thesis check based on the latest earnings

> "Buying is just the beginning. The real work is the systematic tracking during the holding period." — Li Lu
>
> "When the facts change, I change my mind. What do you do?" — Keynes

## Design Philosophy

Most investors' process is: research → buy → hope. Without systematic post-purchase tracking, they end up:
- Unable to sell when they should ("just wait a bit, it'll come back")
- Panic-selling when they shouldn't ("down 20% — did I get it wrong?")
- Forgetting why they bought in the first place ("why did I buy this again?")

Buffett and Li Lu's practice: **write down the sell conditions before you buy**. Then check every quarter whether the thesis is still intact.

## Execution Process

### Step 1: Determine Operating Mode

Check whether an investment thesis file already exists for this company (`reports/{company-name}-thesis.md`):
- If it doesn't exist → enter **Establish Thesis** mode
- If it exists → enter **Track and Check** mode
- If it can't be found but the user says they have one → ask for the file path

---

## Mode A: Establish Investment Thesis

### A0: Data Collection

Use WebSearch to obtain current price, valuation metrics (PE/PB/dividend yield), and core data from the latest earnings. Use this to fill in the valuation anchor. If an existing `/investment-research` or `/investment-team` report exists for this company, read that first.

Use `tools/financial_rigor.py verify-valuation` to validate the valuation data.

### A1: Core Thesis (Must be written in under 200 words)

The investment thesis must answer these 5 questions — one sentence each:

```
I bought {company} at {price} per share because:
1. The essence of this business is {___}, and I understand how it makes money.
2. Its economic moat is {___}, and it is widening / stable.
3. Management {___}; the reason they are trustworthy is {___}.
4. The current price represents {___} discount to intrinsic value; the margin of safety comes from {___}.
5. Even if I'm wrong, the downside is manageable because {___}.
```

**If you can't complete all 5 sentences, the thesis itself has a problem — it means the buying decision wasn't clear enough.**

### A2: Core Assumptions Checklist

Break the investment thesis down into specific, verifiable assumptions:

| # | Core Assumption | Verification Method | Check Frequency | Current Status |
|---|----------------|--------------------|--------------------|----------------|
| 1 | E.g.: Revenue growth stays at 15%+ | Quarterly revenue growth | Every quarter | 🟢 Valid |
| 2 | E.g.: Gross margin stable at 60%+ | Quarterly gross margin | Every quarter | 🟢 Valid |
| 3 | E.g.: Management continues buybacks | Buyback announcements / cash flow statement | Every quarter | 🟢 Valid |
| 4 | E.g.: No competitor breakthrough | Industry data / competitor earnings | Every 6 months | 🟢 Valid |
| 5 | ... | ... | ... | ... |

Typically 3–7 assumptions. Too few means insufficient thinking; too many means the thesis isn't focused enough.

### A3: Red Lines Checklist (Trigger any one = must re-evaluate)

| # | Red Line Condition | Severity | Action if Triggered |
|---|--------------------|----------|---------------------|
| 1 | E.g.: Management integrity compromised (fraud, related-party transactions) | Fatal | Exit immediately |
| 2 | E.g.: Core business revenue declines for 2+ consecutive quarters | Serious | Reduce by 50%, re-evaluate |
| 3 | E.g.: Moat clearly breached (competitor achieves equivalent capability) | Serious | Launch deep research, consider exit |
| 4 | E.g.: Regulatory policy fundamentally changes the business model | Serious | Re-evaluate intrinsic value |
| 5 | E.g.: Management sells large amounts of stock (unplanned) | Warning | Investigate reasons thoroughly |

**Duan Yongping**: "There are only three reasons to sell: 1. You found you bought wrong; 2. The company's fundamentals changed; 3. You found something better."

### A4: Valuation Anchor

| Metric | At Time of Purchase | Optimistic Target | Neutral Target | Pessimistic Scenario |
|--------|--------------------|--------------------|----------------|---------------------|
| Stock price | | | | |
| PE | | | | |
| Market cap | | | | |
| Intrinsic value estimate | | | | |
| Margin of safety | | | | |

### A5: Save the Thesis

Write the investment thesis to `reports/{company-name}-thesis.md`, including:
- Date established
- Purchase price and position size
- Core thesis (5 sentences)
- Core assumptions checklist
- Red lines checklist
- Valuation anchor
- Tracking log (initially empty)

---

## Mode B: Track and Check

### B1: Load Existing Thesis

Read `reports/{company-name}-thesis.md` and load:
- Core thesis
- Core assumptions checklist
- Red lines checklist
- Previous check record

### B2: Collect Latest Data

Use WebSearch to collect:
1. Latest earnings data (if a new quarterly/annual report is available)
2. Recent major events (management changes, regulatory policy, competitive dynamics)
3. Current price and valuation metrics
4. Insider trading record (major shareholders buying/selling)

### B3: Check Core Assumptions One by One

For each core assumption, validate using the latest data:

| # | Core Assumption | Previous Status | Latest Evidence | Current Status | Change |
|---|----------------|----------------|-----------------|----------------|--------|
| 1 | Revenue growth 15%+ | 🟢 Valid | Q4 revenue growth 12% | 🟡 Marginally weakening | ⚠️ |
| 2 | Gross margin 60%+ | 🟢 Valid | Gross margin 61.2% | 🟢 Valid | — |
| 3 | ... | ... | ... | ... | ... |

Status definitions:
- 🟢 **Valid** — Latest data supports the assumption
- 🟡 **Marginally weakening** — Data still within acceptable range, but trend is unfavorable
- 🔴 **Damaged** — Data clearly does not support the assumption
- ⚫ **Broken** — Assumption has been refuted

### B4: Red Lines Check

Check each red line one by one:

| # | Red Line Condition | Triggered | Evidence |
|---|--------------------|:---------:|---------|
| 1 | Management integrity issues | ❌ Not triggered | — |
| 2 | Core business declines 2+ consecutive quarters | ❌ Not triggered | — |

**Any red line triggered → flag prominently in the report with a clear action recommendation.**

### B5: Valuation Update

| Metric | At Purchase | Last Check | Current | Change |
|--------|------------|-----------|---------|--------|
| Stock price | | | | |
| PE (TTM) | | | | |
| Intrinsic value estimate | | | | |
| Margin of safety | | | | |

### B6: Output Tracking Report

#### Report Structure

```
1. Thesis Health Score (out of 10)
2. Core Assumptions Check Results (table)
3. Red Lines Check Results (table)
4. Key Changes This Period (under 500 words)
5. Valuation Update
6. Conclusion and Action Recommendation
7. Key Focus Points for Next Check
```

#### Thesis Health Score Formula

**Formula**: Health = 10 − (⚫ broken assumptions × 3) − (🔴 damaged assumptions × 2) − (🟡 weakened assumptions × 1) − (red lines triggered × 5), minimum 1, maximum 10.

| Score | Meaning | Recommended Action |
|:-----:|---------|-------------------|
| 9–10 | All assumptions valid, thesis stronger than at purchase | Consider adding to position |
| 7–8 | Core assumptions valid, a few marginally weakening | Continue holding |
| 5–6 | 1–2 assumptions damaged, but core logic unchanged | Hold but heighten vigilance |
| 3–4 | Multiple assumptions damaged, thesis foundation shaken | Consider reducing position |
| 1–2 | Red line triggered or core assumption broken | Strongly recommend exiting |

#### Conclusion Must Explicitly Answer

1. **Is the thesis still intact?** Intact / Marginally weakening / Damaged / Broken
2. **What should you do?** Add / Hold / Reduce / Exit
3. **Next check timing**: After the next quarterly report / After a specific event

### B7: Update Thesis File

Append this check's record to the tracking log in `reports/{company-name}-thesis.md`:

| Check Date | Health Score | Key Change | Action Recommended |
|-----------|:----------:|-----------|-------------------|
| 2026-04-09 | 7/10 | Revenue growth slowed to 12%, but margin improved | Hold |

---

## Key Principles

- **Write your sell conditions before you buy** — decisions made when calm are better than decisions made in panic
- **Thesis must be specific enough to verify** — "great company" is not a thesis; "ROE > 25% and trend stable" is
- **Act once a red line is triggered** — the biggest danger is "let's just wait and see"; that's how large losses happen
- **Thesis broken ≠ stock price declined** — a 30% price drop isn't necessarily a reason to sell; a broken thesis is
- **Be honest about mistakes** — if the thesis was wrong, admit it; don't hold on just to save face
