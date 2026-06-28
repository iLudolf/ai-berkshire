---
name: thesis-tracker
description: "AI Berkshire skill: Investment thesis tracking: the discipline system after buying. Source: skills/thesis-tracker.md."
---

## Codex adapter note

This skill is generated from `skills/thesis-tracker.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Investment Thesis Tracking: The Discipline System After Buying

Execute an investment thesis tracking check on $ARGUMENTS.

**Supported input formats**:
- `company name` — establish an investment thesis on first use, or run a tracking check on subsequent uses
- `company name establish thesis` — force re-establishment of the investment thesis
- `company name quarterly check` — run a thesis check based on the latest earnings report

> "Buying is just the beginning. The real work is the continuous tracking during the holding period." — Li Lu
>
> "When the facts change, I change my mind. What do you do?" — Keynes

## Design Philosophy

Most investors follow this process: research → buy → pray. The lack of systematic tracking after buying leads to:
- Unwilling to sell when you should ("just wait a bit longer, it will come back")
- Panic selling when you shouldn't ("it's down 20%, did I get it wrong?")
- Forgetting why you bought in the first place ("why did I buy this again?")

Buffett and Li Lu's approach: **write down the sell conditions before you buy**. Then check every quarter whether the thesis is still intact.

## Execution Process

### Step 1: Determine the Operating Mode

Check whether an investment thesis file already exists for this company (`reports/{company name}-thesis.md`):
- If it does not exist → enter **Establish Thesis** mode
- If it exists → enter **Tracking Check** mode
- If not found but the user says one exists → ask for the file path

---

## Mode A: Establish Investment Thesis

### A0: Data Collection

Use WebSearch to obtain the current share price, valuation metrics (PE/PB/dividend yield), and core data from the latest earnings report, for use in filling in the valuation anchor. If there is an existing `/investment-research` or `/investment-team` report for this company, read from that first.

Use `tools/financial_rigor.py verify-valuation` to validate the valuation data.

### A1: Core Thesis (Must Be Written Clearly in 200 Words or Fewer)

The investment thesis must answer the following 5 questions, one sentence each:

```
I bought ___ company at ___ per share, because:
1. The essence of this business is ___, and I understand how it makes money
2. Its economic moat is ___, and it is widening / stable
3. Management ___, and the reason they are trustworthy is ___
4. The current price represents a ___% discount to intrinsic value; the margin of safety comes from ___
5. Even if I am wrong, downside risk is manageable, because ___
```

**If you cannot complete these 5 sentences, the thesis itself has a problem — it means the buy decision was not clear enough.**

### A2: Core Assumptions Checklist

Break down the investment thesis into specific, verifiable assumptions:

| # | Core Assumption | How to Verify | Frequency | Current Status |
|---|----------------|--------------|-----------|----------------|
| 1 | Example: Revenue growth sustains 15%+ | Quarterly revenue growth | Every quarter | 🟢 Holds |
| 2 | Example: Gross margin stable at 60%+ | Quarterly gross margin | Every quarter | 🟢 Holds |
| 3 | Example: Management continues buybacks | Buyback announcements / cash flow statement | Every quarter | 🟢 Holds |
| 4 | Example: Competitors have not made a breakthrough | Industry data / competitor earnings | Every half year | 🟢 Holds |
| 5 | ... | ... | ... | ... |

Typically 3–7 assumptions. Too few means thinking is not deep enough; too many means the thesis is not focused enough.

### A3: Red Line Checklist (Triggering Any One = Must Re-evaluate)

| # | Red Line Condition | Severity | Action After Trigger |
|---|-------------------|----------|---------------------|
| 1 | Example: Management integrity issue (financial fraud, related-party transactions) | Fatal | Exit immediately |
| 2 | Example: Core business revenue declines for 2 consecutive quarters | Severe | Trim 50%, re-evaluate |
| 3 | Example: Moat clearly breached (competitor achieves equivalent capability) | Severe | Initiate deep research, consider exit |
| 4 | Example: Regulatory policy fundamentally changes the business model | Severe | Re-evaluate intrinsic value |
| 5 | Example: Large-scale unplanned insider selling | Warning | Investigate reasons in depth |

**Duan Yongping**: "There are only three reasons to sell: 1. You discovered you bought wrong; 2. The company's fundamentals changed; 3. You found something better."

### A4: Valuation Anchor

| Metric | At Purchase | Optimistic Target | Neutral Target | Bear Case |
|--------|-------------|-------------------|----------------|-----------|
| Share Price | | | | |
| PE | | | | |
| Market Cap | | | | |
| Intrinsic Value Estimate | | | | |
| Margin of Safety | | | | |

### A5: Save the Thesis

Write the investment thesis to `reports/{company name}-thesis.md`, including:
- Date established
- Purchase price and position size
- Core thesis (5 sentences)
- Core assumptions checklist
- Red line checklist
- Valuation anchor
- Tracking log table (initially empty)

---

## Mode B: Tracking Check

### B1: Read the Existing Thesis

Read `reports/{company name}-thesis.md` and load:
- Core thesis
- Core assumptions checklist
- Red line checklist
- Record from last check

### B2: Collect Latest Data

Use WebSearch to collect:
1. Latest earnings data (if there is a new quarterly or annual report)
2. Recent major events (management changes, regulatory policy, competitive dynamics)
3. Current share price and valuation metrics
4. Insider trading records (major shareholder increases/decreases)

### B3: Check Each Core Assumption Against Latest Data

For each core assumption, validate against the latest data:

| # | Core Assumption | Last Status | Latest Evidence | Current Status | Change |
|---|----------------|-------------|-----------------|----------------|--------|
| 1 | Revenue growth 15%+ | 🟢 Holds | Q4 revenue growth 12% | 🟡 Marginally weakening | ⚠️ |
| 2 | Gross margin 60%+ | 🟢 Holds | Gross margin 61.2% | 🟢 Holds | — |
| 3 | ... | ... | ... | ... | ... |

Status definitions:
- 🟢 **Holds** — latest data supports the assumption
- 🟡 **Marginally Weakening** — data still within acceptable range, but trend is unfavorable
- 🔴 **Impaired** — data clearly does not support the assumption
- ⚫ **Broken** — assumption has been invalidated

### B4: Red Line Check

Check each item in the red line checklist:

| # | Red Line Condition | Triggered | Evidence |
|---|-------------------|:---------:|----------|
| 1 | Management integrity issue | ❌ Not triggered | — |
| 2 | Core business revenue declines 2 consecutive quarters | ❌ Not triggered | — |

**If any red line is triggered → mark it prominently in the report and provide a clear action recommendation.**

### B5: Valuation Update

| Metric | At Purchase | Last Check | Current | Change |
|--------|-------------|------------|---------|--------|
| Share Price | | | | |
| PE (TTM) | | | | |
| Intrinsic Value Estimate | | | | |
| Margin of Safety | | | | |

### B6: Output Tracking Report

#### Report Structure

```
1. Thesis Health Score (out of 10)
2. Core Assumptions Check Results (table)
3. Red Line Check Results (table)
4. Key Changes This Period (500 words or fewer)
5. Valuation Update
6. Conclusions and Action Recommendations
7. Key Focus Areas for the Next Check
```

#### Thesis Health Score Criteria

**Formula**: Health Score = 10 − (⚫ broken assumptions × 3) − (🔴 impaired assumptions × 2) − (🟡 weakening assumptions × 1) − (red lines triggered × 5), minimum 1, maximum 10.

| Score | Meaning | Recommended Action |
|:-----:|---------|-------------------|
| 9–10 | All assumptions hold; thesis is stronger than at purchase | Consider adding to position |
| 7–8 | Core assumptions hold; a few marginally weakening | Continue holding |
| 5–6 | 1–2 assumptions impaired, but core logic unchanged | Hold but raise vigilance |
| 3–4 | Multiple assumptions impaired; thesis foundation shaken | Consider trimming |
| 1–2 | Red line triggered or core assumption broken | Strongly recommend selling |

#### Conclusions Must Explicitly Answer

1. **Is the thesis still intact?** Intact / Marginally Weakening / Impaired / Broken
2. **What should be done?** Add / Hold / Trim / Exit
3. **Next check date**: After the next earnings release / After a specific event

### B7: Update the Thesis File

Append this check's record to the tracking log table in `reports/{company name}-thesis.md`:

| Check Date | Health Score | Key Changes | Action Recommendation |
|------------|:------------:|-------------|----------------------|
| 2026-04-09 | 7/10 | Revenue growth slowed to 12%, but margin improved | Hold |

---

## Key Principles

- **Write the sell conditions before you buy** — decisions made calmly are better than decisions made in panic
- **The thesis must be specific enough to verify** — "the company is good" is not a thesis; "ROE > 25% with a stable trend" is
- **Act when a red line is triggered** — the danger is "just wait and see," which is how big losses begin
- **Thesis broken ≠ share price falling** — a 30% price drop does not necessarily mean sell; a broken thesis does
- **Be honest about mistakes** — if the thesis was wrong, admit it; do not hold on for the sake of pride
