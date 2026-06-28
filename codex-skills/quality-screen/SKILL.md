---
name: quality-screen
description: "AI Berkshire skill: Quality screen — 7 metrics to quickly eliminate non-first-rate companies. Source: skills/quality-screen.md."
---

## Codex adapter note

This skill is generated from `skills/quality-screen.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Quality Screen: 7 Metrics to Quickly Eliminate Non-First-Rate Companies

Run the quality screen on $ARGUMENTS to quickly eliminate candidates that do not meet first-rate company standards.

**Supported input formats**:

| Input type | Example | Notes |
|-----------|---------|-------|
| Individual stock | `Tencent, Meituan, Nvidia` | Screen each company individually |
| Industry | `China beer industry` `Global cloud computing` `HK-listed sportswear brands` | Search for the industry's major listed companies (10–20) first, then screen each |
| Market / index | `Hang Seng Index constituents` `CSI 300` `Nasdaq 100` | Pull the constituent list, then screen each |
| Theme | `China high-dividend top 50` `Global AI compute chain` | Search for theme-related companies first, then screen each |

In industry / market / theme mode, the output additionally includes: pass-rate statistics, intra-industry ranking, and sector comparison summary.

## Design Principles

- **Goal**: Never mistakenly eliminate any genuinely first-rate company, while reliably excluding confirmed non-first-rate companies
- **Logic**: 7 hard metrics + 3 exemption rules — better to let one slip through than to wrongly discard one
- **Scope**: All listed companies (banks / insurers are exempt from Metric 3 — interest coverage)

---

## 7 Quality-Screen Metrics

| # | Metric | Elimination condition | What it measures |
|---|--------|-----------------------|-----------------|
| 1 | 10-year average ROE | < 8% | Capital efficiency — can shareholder capital beat its opportunity cost? |
| 2 | 5-year cumulative free cash flow | Negative | Real cash — are reported profits just "paper wealth"? |
| 3 | Interest coverage ratio (EBIT / interest) | < 2× | Debt safety — ability to service interest payments |
| 4 | Long-term gross margin | < 15% | Pricing power — is the product / service differentiated? |
| 5 | Operating cash flow / net income (5-year average) | < 0.7 | Earnings quality — can reported profits actually be collected in cash? |
| 6 | Long-term net profit margin | < 5% | Resilience — does profit go to zero when revenue fluctuates? |
| 7 | 5-year share-count dilution | > 20% (excluding M&A) | Shareholder alignment — is management diluting your equity? |

## 3 Exemption Rules

### Exemption A: Strategic Investment Phase (applies to Metric 1)

If all 3 of the following conditions are met, Metric 1 (ROE below threshold) may be waived:
1. Listed for fewer than 10 years
2. Gross margin > 30% (proving the business model itself has pricing power)
3. Operating cash flow positive in the most recent 2 years (proving cash-generation capability exists)

**Rationale**: High gross margin + positive cash flow signals that the business model is sound; the low ROE simply reflects an ongoing investment phase. Typical example: Meituan.

### Exemption B: Deliberate Low-Margin Strategy (applies to Metric 6)

If both of the following conditions are met, Metric 6 (net profit margin below threshold) may be waived:
1. Gross margin > 30% (the company is capable of earning but chooses not to at this stage)
2. Net profit margin has recovered above 5% in the past 2 years, or shows a clear upward trend

**Rationale**: A high gross margin confirms pricing power; the low net margin is a strategic reinvestment choice, not a capability deficit. Typical example: Amazon.

### Exemption C: High-Turnover Thin-Margin Model (applies to Metrics 4 and 6)

If all 3 of the following conditions are met, Metrics 4 (gross margin) and 6 (net margin) may be waived:
1. ROE > 20% (proving that despite thin margins, return on capital is outstanding)
2. Operating cash flow / net income > 1.0 (earnings quality is not in question)
3. Business model is of the "membership fee / platform commission / high-turnover thin-margin" type (profits are not reflected in product markup)

**Rationale**: Some first-rate companies hide their profits not in gross margins but in membership fees, turnover efficiency, or platform take rates. Their gross and net margins are naturally low, yet their extremely high ROE signals world-class capital efficiency. Typical example: Costco (gross margin ~12%, net margin ~2.5%, but ROE 25%+ and membership renewal rate 90%+).

---

## Execution Workflow

### Step 1: Parse input and define the screening universe

**Mode determination**:
- If the input is a specific company name / ticker → **individual-stock mode**: proceed directly to Step 2
- If the input is an industry / market / theme → **batch mode**: first perform the following:
  1. Use WebSearch to find major listed companies in the industry / market / theme
  2. Industry mode: cover the top 15–20 listed companies by market cap in that industry
  3. Index mode: pull the complete constituent list
  4. Theme mode: search for related companies, covering 15–30
  5. List the complete company roster for confirmation (if >30 companies, process in parallel batches)

Confirm the full name, ticker, and exchange for each company.

### Step 2: Parallel data collection

Launch an independent background Agent for each company and use WebSearch to gather the following data:

1. **ROE**: Annual ROE for the past 10 years (or since listing), compute the average
2. **Free cash flow**: Operating cash flow and capex for the past 5 years, compute cumulative 5-year FCF
3. **Interest coverage**: Most recent fiscal year EBIT and interest expense, compute the ratio
4. **Gross margin**: Gross margin trend over the past 5 years
5. **Operating cash flow / net income**: Annual ratio for the past 5 years, compute the average
6. **Net profit margin**: Net margin trend over the past 10 years, compute the average
7. **Share count change**: Total shares 5 years ago vs. current, compute the dilution percentage

Data source priority: company annual reports > broker research reports > financial data platforms

### Step 3: Check each metric

For each company, check all 7 metrics one by one:
- ✅ Pass
- ❌ Fail
- ⚠️ Borderline (include numerical explanation)

If a metric is failed, check whether the corresponding exemption conditions are met.

### Step 4: Output results

#### Output format

```markdown
# Quality Screen Results

**Screen date**: {today's date}
**Companies screened**: {N}

## Summary table

| Company | ①ROE | ②FCF | ③Interest cov. | ④Gross margin | ⑤OCF/NI | ⑥Net margin | ⑦Dilution | Result |
|---------|------|------|----------------|--------------|---------|-------------|-----------|--------|
| xxx | ✅ 24% | ✅ | ✅ | ✅ 56% | ✅ | ✅ 30% | ✅ | **Pass** |
| yyy | ❌ 3% | ❌ | ❌ | ✅ 20% | ✅ | ❌ 2% | ✅ | **Eliminated** |
| zzz | ⚠️→✅ | ✅ | ✅ | ✅ 35% | ✅ | ⚠️→✅ | ✅ | **Exemption pass** |

## Companies that passed (N)
[List]

## Companies eliminated (N)
| Company | Failed metrics | Specific data | Reason for elimination |
|---------|---------------|---------------|----------------------|

## Companies passing via exemption (N)
| Company | Exemption clause | Specific data | Exemption rationale |
|---------|-----------------|---------------|---------------------|

## Borderline cases (if any)
[Additional notes for companies near the threshold]

## Sector summary (industry / market mode only)

**Pass rate**: {passed}/{total} = {percentage}
**Industry quality assessment**: [Overall quality assessment of the industry based on pass rate]

| Quality tier | Companies | Common characteristics |
|-------------|-----------|----------------------|
| First-rate (all pass + high ROE) | xxx, yyy | ... |
| Qualified (all pass but metrics are mediocre) | aaa, bbb | ... |
| Eliminated | ccc, ddd | ... |

**Industry stock-selection conclusion**: [One sentence summarizing whether this industry is worth deeper research, and the 2–3 most noteworthy companies]
```

---

## Notes

1. **Banks / insurers**: Metric 3 (interest coverage) does not apply — their business model is inherently based on interest rate spread
2. **REITs**: ROE may fluctuate significantly due to property revaluations; use "core operating profit ROE" instead
3. **Insufficient data**: If a data point cannot be obtained, label it "data unavailable" rather than defaulting to pass or fail
4. **Cyclical industries**: Use averages over a complete cycle (covering at least one peak and one trough), not a single year
5. **Short listing history**: For companies listed fewer than 5 years, use all available data but note "insufficient data window" in the results

## Limitations

These metrics can eliminate companies that are "certainly bad," but passing the screen does not mean "certainly good." Companies that pass still require further research:
- Is the business model sustainable?
- Is management trustworthy?
- Is the current valuation reasonable?
- Is the competitive landscape deteriorating?

Eliminating the inferior is the first step, not the last.
