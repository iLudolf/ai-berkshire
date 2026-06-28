---
name: earnings-review
description: "AI Berkshire skill: Earnings Deep Read: In-Depth Analysis of Primary Sources. Source: skills/earnings-review.md."
---

## Codex adapter note

This skill is generated from `skills/earnings-review.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Earnings Deep Read: In-Depth Analysis of Primary Sources

Perform an earnings deep read analysis on $ARGUMENTS.

**Supported input formats**: `Company Quarter`, e.g.: `Tencent 2025Q4`, `PDD 2025 Annual Report`, `Meituan Latest` (defaults to the most recent period)

> "I never read sell-side research reports — I only read original filings." — Li Lu
>
> "I read 500 pages every day. That's how knowledge builds up, compounding like interest." — Buffett

## Design Philosophy

Most AI investment research tools rely on secondary information (news, research report summaries, data websites). But the core competency of Buffett and Li Lu is reading **primary sources** — annual reports, quarterly reports, and earnings call transcripts.

The problem with secondary information:
- It is filtered — analysts selectively present data that supports their own views
- It is lagged — by the time others have digested it, the alpha is already gone
- It lacks context — "revenue grew 15%" is stripped from management's discussion of growth quality

This skill reads primary sources directly, focusing on what Buffett and Li Lu actually look for.

## Execution Workflow

### Pre-Step: Source Availability Rating

| Grade | Characteristics | Impact |
|-------|----------------|--------|
| A | Full original text obtained (10-K / annual report / earnings call transcript) | Execute all steps normally |
| B | Only partial original text or third-party summary obtained | Label as "non-original source," reduce weight on footnote analysis |
| C | Only news coverage and data-website summaries available | Focus on core financial data changes, skip footnote mining, label as "primary source insufficient" |

### Step 1: Obtain Primary Sources

Use the Task tool to launch multiple background Agents **in parallel** to fetch the following raw materials:

1. **Original earnings report**: Obtain from the company IR page, SEC EDGAR (US stocks 10-K/10-Q), Hong Kong Stock Exchange HKEXnews (HK stocks), or CNINFO (A-shares)
2. **Earnings call transcript / recording**: Obtain from Seeking Alpha, company IR page, Xueqiu, etc.
3. **Management letter to shareholders** (if annual report): Read in full
4. **Investor Day / Analyst Day materials** (if recent)

If the full original text cannot be obtained, use standard data sources following `skills/financial-data.md` to piece together the data (US stocks: macrotrends + stockanalysis; HK stocks: aastocks + macrotrends; A-shares: East Money + CNINFO), but must label as "not original filing, sourced from third-party aggregator," and key data points with >1% discrepancy between two sources must be flagged.

### Step 2: Core Financial Data Extraction and Verification

#### 2.1 Revenue and Income Statement

| Metric | Current Period | Prior Period | YoY Change | Management Guidance | Met? |
|--------|---------------|-------------|-----------|---------------------|------|

Must cover:
- Total revenue and revenue breakdown by business segment / geography
- Gross profit and gross margin changes
- Operating profit and operating margin changes (distinguish GAAP vs. Non-GAAP)
- Net income (note the impact of non-recurring items)
- EPS (basic vs. diluted)

#### 2.2 Cash Flow Statement (Buffett's Top Priority)

| Metric | Current Period | Prior Period | Change | Key Focus |
|--------|---------------|-------------|--------|-----------|

Must cover:
- Operating cash flow vs. net income ratio (>100% is ideal; <80% warrants caution)
- Capital expenditures and their composition (maintenance vs. growth)
- Free cash flow = Operating cash flow − Capital expenditures
- Buyback amount and dividend amount
- Cash and cash equivalents ending balance

#### 2.3 Balance Sheet Health

Must cover:
- Cash + short-term investments vs. interest-bearing debt
- Net cash / net debt trend
- Accounts receivable days outstanding change (are they loosening credit terms to pump revenue?)
- Inventory days outstanding change (is inventory piling up?)
- Goodwill and intangible assets as a percentage of assets (impairment risk?)

**Data Verification**: Use `tools/financial_rigor.py` to validate key data:

```bash
# Cross-validate revenue and net income (at least 2 sources)
python3 tools/financial_rigor.py cross-validate \
  --metric "revenue" --values 108.3e9 107.9e9 --sources "Company Filing" "Yahoo Finance"

# Verify market cap
python3 tools/financial_rigor.py verify-market-cap \
  --price 101 --shares 1.488e9 --reported 1.44e11 --currency USD

# Verify valuation metrics
python3 tools/financial_rigor.py verify-valuation \
  --price 101 --eps 9.6 --bvps 26.5 --fcf-per-share 10.2
```

### Step 3: Management Discussion Deep Read (MD&A)

This is the section where Buffett and Li Lu spend the most time. It's not about looking at numbers — it's about **listening to how management talks**.

#### 3.1 Management Tone Analysis

Read the management discussion / earnings call statements paragraph by paragraph, and flag the following signals:

| Signal Type | Specific Manifestation | Example |
|-------------|----------------------|---------|
| 🟢 **Candor signal** | Proactively acknowledges problems, gives specific reasons | "Margin declined this quarter primarily because our investment in X exceeded expectations" |
| 🟢 **Clarity signal** | Strategic statements are specific, with quantified targets | "We plan to grow X business's market share from 15% to 20% over the next 12 months" |
| 🔴 **Vagueness signal** | Heavy use of "we believe," "in the long run," and other substance-free phrases | "We are full of confidence about the future" |
| 🔴 **Deflection signal** | Avoids direct questions, pivots to other topics | When asked about margins, pivots to discussing revenue growth |
| 🔴 **External attribution** | Blames all problems on macro / industry / competitors | "Due to the impact of the macro environment..." |

#### 3.2 Commitment Tracking

Extract specific commitments made by management in the prior earnings report / call, and compare with actual results this period:

| Prior Commitment | Actual Outcome This Period | Assessment |
|-----------------|--------------------------|------------|
| "Margin will recover to X% in H2" | Actual Y% | ✅ Met / ❌ Missed / ⚠️ Partially Met |

**Duan Yongping**: "The simplest way to judge whether management is reliable is to check whether they've followed through on what they said before."

#### 3.3 Key Question Identification

Extract the sharpest analyst questions from the earnings call Q&A section, and assess management's answer quality:

| Analyst Question | Management Answer | Answer Quality (1–5) | Avoided? |
|-----------------|------------------|:-------------------:|:--------:|

### Step 4: Footnote and Hidden Information Mining

Earnings report footnotes contain information management does not want you to find easily:

#### 4.1 Required Footnote Checks

- [ ] **Related-party transactions**: Are the terms of transactions with major shareholders / related parties arm's-length?
- [ ] **Stock-based compensation**: How significant is the dilutive effect of options / RSUs? What are the exercise prices?
- [ ] **Contingent liabilities**: Off-balance-sheet risks such as litigation, guarantees, and commitments
- [ ] **Accounting policy changes**: Have revenue recognition methods, depreciation periods, etc. been changed?
- [ ] **Segment information**: Profit margin differences across business segments — is there cross-subsidization from good businesses to bad ones?
- [ ] **Customer / supplier concentration**: Top-five customer / supplier revenue concentration

#### 4.2 Anomaly Signal Detection

- [ ] Accounts receivable growth > revenue growth (possible channel stuffing)
- [ ] Inventory growth > revenue growth (possible pile-up)
- [ ] Operating cash flow < net income and the gap is widening (earnings quality in question)
- [ ] Capitalized expenditures suddenly increase (possible earnings beautification)
- [ ] Non-recurring income as a percentage of earnings suddenly rises

### Step 5: Comparison with Historical Data

#### 5.1 Trend Analysis

Place key metrics for this period into a time series of at least 4 quarters (or 3 years of annual reports):

| Metric | Q-4 | Q-3 | Q-2 | Q-1 | Current | Trend Judgment |
|--------|-----|-----|-----|-----|---------|---------------|

Focus on:
- Are margins improving or deteriorating?
- Is revenue growth accelerating or decelerating?
- Is cash flow quality improving or declining?
- Is capital expenditure intensity increasing or decreasing?

#### 5.2 Comparison with Management Guidance

| Metric | Prior Management Guidance | Actual Result | Deviation | Interpretation |
|--------|--------------------------|--------------|-----------|---------------|

### Step 6: Output Deep Read Report

#### Report Structure

```
I.   Core Data Snapshot (one-page table)
II.  The 3 Most Important Changes This Period (no more than 500 words)
III. Management Tone and Commitment Tracking
IV.  Hidden Information in the Footnotes
V.   Key Questions (Selected Q&A from Earnings Call)
VI.  Relationship to the Investment Thesis (if holding a position)
VII. Conclusion: What Does This Earnings Report Change?
```

#### The Conclusion Must Explicitly Answer

1. **Did this earnings report beat, meet, or miss expectations?** (Cannot say "broadly in line" and then list a bunch of two-sided points)
2. **Impact on the investment thesis**: Strengthened / No impact / Weakened / Broken
3. **What is the next catalyst to watch?**
4. **If you already hold a position, should you add / hold / trim?**

### Step 7: Save the Report

Write the report to `reports/{CompanyName}-earnings-{Period}.md`, e.g. `reports/Tencent-earnings-2025Q4.md`

### Step 8: Data Spot Check (Release Gate)

After writing the report, perform a data spot check; it must pass before publishing:

```bash
# Step 1 — Extract the spot-check list
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report reports/{CompanyName}-earnings-{Period}.md

# Step 2 — For each item on the list, source figures from reliable data sources (see skills/financial-data.md)

# Step 3 — Output pass / reject verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report {report-filename}
```

**[PASS]** All items pass → publish; **[REJECT]** Any item fails → revise and re-audit.

## Core Principles

- **Read original sources, not summaries**: make every effort to obtain primary sources
- **Look for changes, not absolute values**: trends matter more than numbers themselves
- **Listen to the tone, not just the content**: how management speaks is as important as what they say
- **Check the footnotes, not just the main text**: the devil is in the details
- **Deliver conclusions, not summaries**: the purpose of a deep read is to form a judgment, not to paraphrase the report
