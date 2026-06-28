---
name: industry-funnel
description: "AI Berkshire skill: Industry funnel screening: a value investing selection process from the full market down to 3 final picks. Source: skills/industry-funnel.md."
---

## Codex adapter note

This skill is generated from `skills/industry-funnel.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Industry Funnel Screening: A Value Investing Selection Process from the Full Market to 3 Final Picks

Execute a funnel-style value investing screen on the $ARGUMENTS industry/theme, narrowing from a full-market scan down to 3 final candidates layer by layer.

## Use Cases

When you name an industry or investment theme (e.g., "AI compute", "innovative drugs", "robotics") and want to:
1. Miss no important candidates (including A-shares, HK stocks, US stocks, and unlisted candidates)
2. Filter out "story stocks" and low-quality companies using a uniform standard
3. Focus attention on the 3 leading companies truly worth deep research
4. Have clear keep/reject criteria at each layer for traceability and review

Difference from `industry-research`:
- `industry-research` focuses on industry chain structure and panoramic view, slicing by segment
- `industry-funnel` focuses on the individual stock screening funnel, narrowing from the full market to 3 names

The two are complementary: use `industry-research` first to understand the industry chain landscape, then use `industry-funnel` to select the best picks.

---

## Funnel Structure Overview

```
Layer 1: Full-market scan      30-60 companies   (union of top 30 by activity + returns + market cap)
         ↓ 5 hard value-investing criteria
Layer 2: Coarse screen            ≤ 10 companies  (all 5 criteria pass + moat ★★★ or above)
         ↓ Detailed analysis
Layer 3: Detailed analysis        ≤ 10 companies  (300-500 word structured analysis per company)
         ↓ Final selection
Layer 4: Four Masters deep dive    3 companies    (800-1200 words each, Buffett/Munger/Duan/Li Lu perspectives)
         ↓
Output: Investment recommendation + action signal + position sizing
```

Companies filtered out at each layer must have documented elimination reasons — no black boxes.

---

## Step 1: Full-Market Scan Entry

### 1.1 Active Stock Definition (Union of Three Categories)

**Category A — Trading Activity**:
- Ranked among the top in the industry by average daily turnover over the past 30 days (top 30 for A-shares, HK, and US markets respectively)

**Category B — Return Leaderboard**:
- Top 20 by return over the past 30 days
- Top 20 by return over the past 90 days
- Union of both

**Category C — Market Cap Anchor**:
- Top 30 by market cap within the industry (regardless of price movement)

Final scan pool = A ∪ B ∪ C, expected 30-60 companies.

### 1.2 Markets to Search

| Market | Recommended Sources |
|--------|-------------------|
| A-shares (Shanghai/Shenzhen) | Tonghuashun / Eastmoney industry sectors, Tongdaxin |
| HK stocks | Futu / Tonghuashun HK, HKEX industry classification |
| US stocks | NASDAQ/NYSE industry ETF holdings, Yahoo Finance |
| International markets | Do not miss related companies in Japan, Korea, Taiwan, and Europe (especially semiconductors, electronics) |
| Unlisted companies | List separately in an "Future IPO Candidates" subsection, noting latest valuation and potential IPO timeline |

### 1.3 Output Format

| Company Name | Ticker | Market | Market Cap | Core Business (one sentence) | Industry Revenue % | Category (A/B/C) |
|-------------|--------|--------|------------|-----------------------------|--------------------|------------------|

**Key Self-Check**:
- "Peripheral exposure" companies with industry revenue % < 30% should be flagged as "not pure-play"
- Do not miss Chinese/Asian market companies due to limited English-language coverage
- Do not miss small-cap companies due to AI preference for market leaders

---

## Step 2: 5 Hard Value-Investing Criteria — Coarse Screen → ≤ 10 Companies

Apply 5 hard criteria to each of the 30-60 companies from Step 1.

### 2.1 The 5 Hard Criteria

| # | Criterion | Pass Standard | Relaxation Condition | Data Source |
|---|-----------|--------------|---------------------|-------------|
| 1 | PE valuation | Reasonable (vs. historical range and peer comparison) | High-growth companies: PEG < 1.5 | Earnings reports + Wind/Tonghuashun |
| 2 | ROE | > 15%, or improving trend over the past 3 years | Heavy-asset industries: relaxed | Earnings reports |
| 3 | Operating cash flow | Positive and > 70% of net income | — | Earnings reports |
| 4 | Debt-to-asset ratio | < 60% | Utilities/power: relaxed to 70% | Earnings reports |
| 5 | Moat quick score | ★★★ or above | — | Qualitative judgment |

**5 Moat Categories**:
- Brand / pricing power
- Switching costs / user stickiness
- Network effects
- Scale economies
- Technology / license / resource barriers

### 2.2 Output Format

| Company | PE | ROE | Cash Flow/Net Income | Debt Ratio | Moat | Overall | Keep/Reject | Elimination Reason |
|---------|----|----|---------------------|------------|------|---------|------------|-------------------|

**Retention Rules**:
- All 5 criteria pass → retain directly
- 4 criteria pass + 1 borderline → retain but flag yellow
- Fewer than 4 pass → eliminate, note reason

**Target**: retain ≤ 10 companies. If too many remain (> 12), raise the moat standard to ★★★★ and screen again.

---

## Step 3: Detailed Analysis (≤ 10 Companies, 300-500 Words Each)

For companies retained from the coarse screen, conduct structured analysis for each.

### 3.1 Per-Company Analysis Template

```
## {Company Name} ({Ticker})

**Business Model in One Sentence**:
(What they sell, to whom, and how they monetize)

**Financial Quality**:
- Revenue growth / earnings growth / gross margin / ROE / cash flow
- Key changes (most important financial inflection points in the past 1-2 years)

**Moat Depth**:
- Primary moat type(s) + specific evidence
- Brief judgment on whether the moat will still be intact in 5 years

**Top 3 Risks**:
1.
2.
3.

**Valuation Quick Assessment**:
- Current PE/PS/EV/EBITDA + position within historical range
- Peer comparison
- One-sentence conclusion: Expensive / Fair / Cheap

**Advance to Final 3?**: Yes / No (reason)
```

### 3.2 Criteria for Selecting the Final 3

Rather than ranking by score and taking the top 3, select based on "portfolio complementarity":
- At least 1 "high certainty, low upside" company (Buffett type)
- At least 1 "moderate certainty, moderate upside" company (growth type)
- Optionally 1 "high upside, high risk" company (option type)

If a sub-segment cannot yield 3 sufficiently good candidates, write "Final 2 + 1 on watch" rather than padding the list.

---

## Step 4: Four Masters Deep Dive (3 Companies, 800-1200 Words Each)

Conduct a Four Masters perspective deep dive on the 3 final picks.

### 4.1 Duan Yongping Perspective: Business Essence

- Define in one sentence what business this company is actually in
- Is this a good business? Why?
- What is its "ben fen" (core duty / first principles)? Has management deviated from it?
- Where does the business model's "sustainability" lie?

### 4.2 Buffett Perspective: Moat Depth

- Score on the five moat categories (★1-5) with specific evidence
- Will the moat still be intact in 10 years?
- Where is the margin of safety for buying now?

| Moat | Strength | Specific Evidence |
|------|----------|------------------|
| Brand / pricing power | | |
| Switching costs | | |
| Network effects | | |
| Scale economies | | |
| Technology / license barriers | | |

### 4.3 Munger Perspective: Risks and Failure Modes

- What is the most likely way this company fails? (List top 3 failure paths)
- What is it worth in the worst-case scenario? (Simplified valuation)
- Why wouldn't a smart person buy this? (Reverse argument)
- Are there ethical / compliance / management risks?

### 4.4 Li Lu Perspective: Civilizational Trend Positioning

- Is this company's track a "civilizational paradigm shift" or a "cyclical hype"?
- What is the closest historical technology revolution analogy?
- What is this company's end state in 10-20 years?
- Is this a winner-takes-all dynamic?

### 4.5 Composite Recommendation

```
Recommendation: ★★★★☆
Position Type: Core / Satellite / Option / Watch
Suggested Buy Range: Current price / N% pullback / patient wait
Suggested Position Size: X% of this theme allocation
Key Monitoring Indicators: (what signals would invalidate the thesis for this company)
```

---

## Step 5: Consolidated Output

At the end of the report, integrate:

### 5.1 Final 3 Portfolio Table

| Company | Type | Recommendation | Suggested Position | Core Thesis | Key Risk |
|---------|------|---------------|--------------------|-------------|----------|
| A | Core | ★★★★★ | 50-60% | | |
| B | Satellite | ★★★★☆ | 25-35% | | |
| C | Option | ★★★☆☆ | 5-15% | | |

### 5.2 Industry-Level ETF Alternative

If stock-picking is not desired, list 1-3 relevant ETFs (A-shares / HK / US).

### 5.3 Overall Industry Positioning

- Industry PE/PB historical percentile
- Capital flows (northbound, ETF subscriptions/redemptions, sell-side coverage density)
- Overall stage: "Early / Expansion / Mature / Declining"

### 5.4 Information Sufficiency Self-Assessment (Required)

| Dimension | Grade | Notes |
|-----------|-------|-------|
| Company financial data completeness | A/B/C | |
| Valuation data timeliness | A/B/C | |
| Competitive landscape assessment | A/B/C | |
| Management information | A/B/C | |

A = Data sufficient and credible; B = Partially missing but core conclusion unaffected; C = Significant gaps, conclusions require caution.

### 5.5 Data Points Pending Update

Explicitly list: which data points are estimates, which require follow-up verification, and which quarterly earnings reports require close tracking.

### 5.6 Source List

Source links for each data point/conclusion, organized by category (earnings reports, research notes, news, industry reports).

---

## AI Research Bias Awareness (Important)

Biases AI commonly falls into during funnel screening:

| Bias | Manifestation | Countermeasure |
|------|--------------|----------------|
| Large-cap preference | More data on large-cap companies; longer analysis makes them look "better" | Score on hard criteria and moat, not by report length |
| English-language preference | US stocks have richer coverage; A-shares and HK stocks tend to be underweighted | Must search in both Chinese and English; A/H companies cannot be missed |
| Story preference | High returns + media hype = looks like a better "AI concept stock" | Distinguish "AI revenue %" vs. "AI story %"; focus on actual business |
| Recency preference | Companies with strong current financials get selected easily; may miss turnaround dark horses | Layer 2 coarse screen allows "improving trend" as a relaxation condition |
| Listed-company preference | Focusing only on listed companies may miss the best players in a segment | Must list "Future IPO Candidates" with valuation and timing window |

---

## Output Requirements

1. **Report location**: `reports/{industry-name}-funnel-{YYYYMMDD}.md` (industry reports go in the reports/ root directory)
2. **Language**: English
3. **Style**: Direct, sharp, no filler
4. **Data**: All data points cite sources; estimated values labeled "estimated"
5. **No predetermined stance**: Present data first → reason through logic → draw conclusions
6. **Both sides**: Every core judgment includes a counter-argument
7. **Elimination records at each layer**: Eliminated companies must be named with reasons

---

## Data Audit (Gate-Keeping Process)

After the report is written, run a data audit before publishing:

```bash
# Step 1 — Extract audit checklist (15% random sample)
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report-file-path>

# Step 2 — For each item on the checklist, retrieve data from a reliable source (see skills/financial-data.md)

# Step 3 — Output pass/fail verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report <report-file-name>
```

**[PASS]** All items pass → report may be published; **[FAIL]** Any item fails → correct and re-audit.

---

## Follow-on Actions

After the funnel selects the final 3, each can be individually processed with:
- `/investment-team` — Full Four Masters parallel deep research (separate subdirectory + 5 documents)
- `/investment-checklist` — Run through the Buffett pre-buy checklist systematically
- `/management-deep-dive` — In-depth management research

`industry-funnel` is the entry point; the follow-on skills are for deeper dives.
