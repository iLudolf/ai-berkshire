---
name: financial-data
description: "AI Berkshire skill: Financial data retrieval and cross-validation standards. Source: skills/financial-data.md."
---

## Codex adapter note

This skill is generated from `skills/financial-data.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Financial Data Retrieval and Cross-Validation Standards

This standard applies to all research involving corporate financial data. **Every key data point must come from two independent sources; discrepancies > 1% must be flagged.**

---

## Data Source Priority

### US Stocks (PDD, Tencent ADR, NetEase ADR, etc.)

| Priority | Source | URL | Access |
|--------|------|-----|---------|
| 1 (Primary) | **macrotrends** | macrotrends.net/stocks/charts/{ticker} | Direct access, no registration |
| 2 (Secondary) | **stockanalysis** | stockanalysis.com/stocks/{ticker}/financials | Direct access, no registration |
| Raw primary | SEC EDGAR | sec.gov/cgi-bin/browse-edgar | 10-K / 10-Q originals |

### HK Stocks (Tencent 0700, NetEase 9999, Meituan 3690, etc.)

| Priority | Source | URL | Access |
|--------|------|-----|---------|
| 1 (Primary) | **aastocks** | aastocks.com/tc/stocks/analysis/company-fundamental | Direct access |
| 2 (Secondary) | **macrotrends** (ADR ticker) | Tencent uses TCEHY, NetEase uses NTES | Direct access |
| Raw primary | HKEX news | hkexnews.hk | Annual report PDF |

### A-Shares (37Games, Geeglobe, etc.)

| Priority | Source | URL | Access |
|--------|------|-----|---------|
| 1 (Primary) | **East Money** | eastmoney.com → search ticker → financial statements | Direct access |
| 2 (Secondary) | **CNINFO** | cninfo.com.cn | Original annual/quarterly report PDF |

---

## Execution Standards

### Step 1: Retrieve Data

For each financial metric (revenue, net income, gross margin, operating cash flow, leverage ratio, etc.), pull figures separately from **Source 1** and **Source 2**.

### Step 2: Discrepancy Calculation and Flagging

```
Discrepancy rate = |Source 1 value - Source 2 value| / Source 1 value × 100%
```

| Discrepancy | Handling |
|------|---------|
| ≤ 1% | ✅ Consistent — use Source 1 value, cite both sources |
| 1% ~ 5% | ⚠️ Flag "data discrepancy", note both values, explain likely cause (FX / accounting standard) |
| > 5% | ❌ Flag "material data discrepancy" — must verify against original financial report; do not use directly |

### Step 3: Data Presentation Format

Every key data point must be annotated in the following format:

```
Revenue: CNY 123.9B ✅
  - macrotrends: CNY 124.1B
  - stockanalysis: CNY 123.7B
  - Discrepancy: 0.3%
```

Discrepancy example:
```
Net income: CNY 24.5B ⚠️ Data discrepancy
  - macrotrends: CNY 24.5B (GAAP)
  - stockanalysis: CNY 27.8B (Non-GAAP)
  - Discrepancy: 13.5% — Reason: different accounting standards (GAAP vs Non-GAAP)
```

---

## Common Causes of Discrepancy (not necessarily data errors)

| Cause | Explanation |
|------|------|
| GAAP vs Non-GAAP | Most common, especially for profit figures |
| FX conversion | HKD / CNY / USD conversion at different points in time |
| Fiscal year definition | Calendar year vs fiscal year (e.g., Apple FY ends in October) |
| Consolidation scope | Whether minority interest is included |
| Data update lag | A platform has not yet updated the latest reporting period |

---

## Special Rules

1. **Private/unlisted companies** (miHoYo, Lilith Games, etc.): when only one primary source is available, prefix data with `[Estimated]` and skip cross-validation
2. **Quarterly vs annual data**: prefer annual data for cross-validation; quarterly data may be delayed on some platforms
3. **Original report takes precedence**: if both sources diverge from the original financial report (10-K / annual report PDF), the original report is authoritative — flag the source as erroneous

---

## Quick Reference

| Scenario | Primary Source | Backup Source |
|------|---------|---------|
| PDD / Pinduoduo | macrotrends.net/stocks/charts/PDD | stockanalysis.com/stocks/pdd |
| Tencent | macrotrends.net/stocks/charts/TCEHY | aastocks (0700.HK) |
| NetEase | macrotrends.net/stocks/charts/NTES | aastocks (9999.HK) |
| 37Games | eastmoney.com (002555) | cninfo.com.cn |
| Geeglobe | eastmoney.com (603444) | cninfo.com.cn |
| Nintendo | macrotrends.net/stocks/charts/NTDOY | stockanalysis.com/stocks/ntdoy |
| Capcom | macrotrends (CCOEY) | stockanalysis (CCOEY) |
