---
name: industry-research
description: "AI Berkshire skill: Industry investment research: full industry chain panoramic scan + Four Masters individual stock analysis framework. Source: skills/industry-research.md."
---

## Codex adapter note

This skill is generated from `skills/industry-research.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Industry Investment Research: Full Industry Chain Panoramic Scan + Four Masters Individual Stock Analysis Framework

Conduct systematic industry chain investment research on the $ARGUMENTS industry.

## Research Objectives

Starting from an investment theme/logic chain, complete:
1. Validate every link in the investment logic chain
2. Draw a complete industry chain panoramic map
3. Scan all global listed companies (A-shares / Hong Kong / US / International)
4. Execute the Four Masters framework analysis on leading companies in each sub-segment
5. Output industry-level portfolio allocation recommendations

---

## Step 1: Investment Logic Chain Construction and Validation

### 1.1 Draw the Logic Chain
Express the causal relationship from "underlying trend" to "beneficiary targets" using an arrow chain, for example:
```
Underlying Trend A
    → leads to Demand B
        → creates Bottleneck/Core Need C
            → benefits Industry Chain D
```

### 1.2 Validate Each Link
Challenge each arrow in the logic chain and search for evidence:

| Link | Core Assumption | Validation Method | Data Source |
|------|----------------|-------------------|-------------|
| A→B | | Search industry data/forecasts | |
| B→C | | Search supply/demand analysis | |
| C→D | | Search real cases/signed contracts | |

### 1.3 Find "Already-Occurred Validation Events"
List **real, signed/deployed commercial events** (not forecasts) that support this logic chain, such as major corporate procurement agreements, policy documents, and industry reports.

---

## Step 2: Industry Chain Panoramic Map

### 2.1 Draw the Industry Chain Structure
Break the industry into upstream → midstream → downstream → ancillary segments, for example:
```
Upstream: Raw materials/resource extraction → Material processing/refining
Midstream: Core equipment manufacturing → System integration/engineering → New technology R&D
Downstream: Operations/services → End customers
Ancillary: Testing/certification → Maintenance services → Financial instruments (ETF/trusts)
```

### 2.2 Identify the "Business Characteristics" of Each Segment
Annotate each segment:

| Segment | Business Model | Gross Margin Range | Competitive Landscape | Barrier Type | Cyclicality |
|---------|---------------|-------------------|-----------------------|--------------|-------------|
| | Sell resources/equipment/services/collect rent | | Monopoly/Oligopoly/Full competition | Resource/License/Technology/Scale | Strong/Medium/Weak |

### 2.3 Flag "Chokepoint Segments"
Identify the segments with the tightest supply, hardest substitution, and highest profit margins in the industry chain — these are often where the best investment targets are found.

---

## AI Research Bias Awareness: Special Pitfalls in Industry Research

In industry research, AI data bias can be amplified in unique ways:

**Industry-level biases**:
| Bias Type | Manifestation | Countermeasure |
|-----------|--------------|----------------|
| Mature industry preference | Traditional industries (banking/energy/consumer) have abundant data, making AI analysis look "more certain" | Certainty comes from business model, not the volume of research reports |
| Underestimation of emerging industries | New industries (AI applications/synthetic biology, etc.) have less data, causing AI to be more conservative | Use "end-state thinking" rather than "current data" to judge industry value |
| Large-cap bias | Major companies have far more data than smaller ones; AI naturally tends to recommend leaders | Smaller companies may offer better risk/reward ratios — don't overlook them just because AI analysis is shorter |
| Listed-company bias | Scanning only listed companies misses key unlisted players in the industry chain | Must search for unlisted companies and flag them as "future IPO candidates" |
| English-language bias | AI processes English-language material better and may underestimate Chinese/Asian market players | Must search both Chinese and English sources simultaneously |

**Anti-bias measures in industry chain scanning**:
1. For each segment, not only list "companies easy for AI to find," but actively search for "less-known but potentially high-quality targets"
2. For small-cap companies with scarce information, do not reduce their recommendation rating just because the analysis is shorter — evaluate using core questions (business fundamentals, moat, management) rather than report length
3. In the final report, annotate each company's "information adequacy" (Grade A/B/C) so readers know how reliable the AI analysis is

## Step 3: Global Listed Company Scan

Use the Task tool to launch a background Agent to comprehensively search all listed companies in this industry.

### Search Checklist
- US-listed companies (NYSE/NASDAQ/NYSE American)
- A-share companies (Shanghai/Shenzhen)
- Hong Kong-listed companies
- Other international markets (Japan/South Korea/Europe/Australia, etc.)
- Industry ETFs
- Key unlisted companies (potential future IPO candidates)

### Collect for Each Company
- Company name (Chinese and English)
- Ticker symbol and exchange
- Market cap (approximate)
- One-sentence description (position and role in the industry chain)
- Whether it is a pure-play target (pure-play vs. conglomerate with relevant business segment)
- Industry chain segment it belongs to

### Output Format
Organized by industry chain segment, one table per segment containing all scanned companies.
Then tiered by investment certainty:
- **Tier 1**: Large-cap, pure-play, industry leaders
- **Tier 2**: Mid-cap, pure-play or high-segment exposure, sub-sector leaders
- **Tier 3**: Small-cap, development stage, high risk / high upside
- **Tier 4**: Diversified companies with relevant business exposure

---

## Step 4: Four Masters Analysis of Leading Companies in Each Segment

For **Tier 1 and Tier 2 companies** in each industry chain segment, execute the following analysis (Tier 3/4 companies require only a brief commentary):

### 4.1 Business Fundamentals (Duan Yongping)
- One-sentence definition of what this company does in the industry chain
- Revenue structure and growth rate
- Gross margin / net margin level and trend
- Cash flow characteristics
- **Follow-up question**: Is this a good business? Why?

### 4.2 Economic Moat (Buffett)
Score across five moat categories (★1-5):

| Moat | Strength | Evidence |
|------|----------|---------|
| Brand / pricing power | | |
| Switching costs | | |
| Network effects | | |
| Scale economies | | |
| Technology / license barriers | | |

**Follow-up question**: Will the moat still exist in 10 years?

### 4.3 Risks (Munger)
- How is this company most likely to fail?
- What is it worth in the worst-case scenario?
- Why would a smart investor not buy it?

### 4.4 Management (Duan Yongping + Buffett)
- Who is the CEO/founder? Key decision track record
- Ownership percentage and alignment of interests
- Brief rating (Grade A/B/C)

### 4.5 Valuation Snapshot
- Current PE/PS/EV/EBITDA
- Comparison with competitors in the same segment
- Brief commentary: Expensive / Fair / Cheap

### 4.6 Recommendation Rating
Annotated with ★1-5:
- ★★★★★ = Core position candidate
- ★★★★☆ = Satellite position candidate
- ★★★☆☆ = Watch list
- ★★☆☆☆ = High-risk option
- ★☆☆☆☆ = Not recommended

---

## Step 5: Industry-Level Risk Assessment (Munger "Checklist")

### 5.1 Systemic Risk Checklist

| Risk | Probability | Impact | Mitigation Strategy |
|------|-------------|--------|---------------------|
| A link in the investment logic chain is disproven | | | |
| Substitute technology emerges | | | |
| Policy/regulatory black swan | | | |
| Cyclical demand pullback | | | |
| Valuation bubble burst | | | |

### 5.2 Historical Analogies
Find historically similar industry chain investment themes and analyze their ultimate outcomes:
- What was the analogous industry?
- Who were the ultimate winners? (Upstream / Midstream / Downstream?)
- Did most investors make money or lose money?
- What are the implications for the current industry?

### 5.3 Bias Self-Check
- Narrative bias: Is the story too perfect?
- Anchoring effect: Are you anchored to recent price gains?
- Herd effect: Are you buying because "everyone else is buying"?

---

## Step 6: Civilizational Trend Assessment (Li Lu Framework)

- Is the underlying trend supporting this industry a "civilization-level paradigm shift" or a "cyclical boom"?
- What is the closest historical technology revolution analogy?
- What is the end-state of this industry in 10-20 years?
- Which segment in the industry chain is most likely to achieve "winner-take-all"?
- Which segment is most likely to be disrupted?

---

## Step 7: Portfolio Allocation Recommendations

### 7.1 Recommended Portfolio
Output using the following structure:

| Tier | Position Weight | Target | Industry Segment | Core Logic |
|------|----------------|--------|-----------------|------------|
| **Core positions** | 50-60% of theme allocation | | | Most certain, widest moat |
| **Satellite positions** | 25-35% of theme allocation | | | Higher upside, slightly lower certainty |
| **Option positions** | 5-15% of theme allocation | | | High risk / high reward, can go to zero |
| **ETF alternative** | Can replace all of the above | | | "Lazy" solution for those who prefer not to pick stocks |

### 7.2 Buy/Sell Signals

| Signal Type | Specific Conditions |
|-------------|---------------------|
| Add signal | |
| Trim signal | |
| Exit signal | |

### 7.3 Recommended Theme Position Cap
Based on the certainty and risk level of the investment logic chain, recommend the maximum percentage of total portfolio this theme should represent.

---

## Step 8: Comprehensive Decision Memo

### Industry Summary Table

| Dimension | Conclusion | Confidence |
|-----------|-----------|------------|
| Investment logic chain (degree of validation) | | |
| Best segment (Duan Yongping's "right business") | | |
| Widest moat (Buffett) | | |
| Greatest risk (Munger) | | |
| Civilizational trend positioning (Li Lu) | | |
| Overall valuation level | | |

### Four Masters Simulated Commentary
Using quote format, simulate how the Four Masters would each comment on the investment opportunity in this industry.

---

## Output Requirements

1. All analysis must be data-supported with data sources cited
2. Use Markdown tables to present key data
3. Industry chain panoramic map expressed using text diagrams in code blocks
4. Analyze at least 2-3 leading companies per segment
5. Global company scan should be as complete as possible (A-shares / Hong Kong / US / International)
6. Write the complete final report to `~/[industry-name]-industry-chain-investment-research.md`
7. Conclusions must be clear, providing specific targets, position sizes, and price range recommendations
8. Each analysis module ends with the corresponding master's "follow-up question"

## Data Spot-Check (Gate Process)

After the report is written, execute a data spot-check; only pass if approved:

```bash
# Step 1 — Extract spot-check list (15% random sampling)
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report file path>

# Step 2 — For each item on the list, retrieve data from reliable sources (see skills/financial-data.md)

# Step 3 — Output pass/reject verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<filled-in JSON>' \
  --report <report filename>
```

**[PASS]** All items pass → report may be published; **[REJECT]** Any item fails → correct and re-review.
