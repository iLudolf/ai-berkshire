# Financial Data: Source Priority & Cross-Validation Standards

This standard applies to all research involving company financial data. **Every key data point must come from two independent sources; deviations > 1% must be flagged.**

---

## Data Source Priority

### US Stocks (PDD, Tencent ADR, NetEase ADR, etc.)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **Macrotrends** | macrotrends.net/stocks/charts/{ticker} | Direct, no login |
| 2 (Secondary) | **Stock Analysis** | stockanalysis.com/stocks/{ticker}/financials | Direct, no login |
| Primary source | SEC EDGAR | sec.gov/cgi-bin/browse-edgar | 10-K / 10-Q originals |

### Hong Kong Stocks (Tencent 0700, NetEase 9999, Meituan 3690, etc.)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **AAStocks** | aastocks.com/tc/stocks/analysis/company-fundamental | Direct |
| 2 (Secondary) | **Macrotrends** (ADR ticker) | Tencent → TCEHY; NetEase → NTES | Direct |
| Primary source | HKEX Disclosure Easy | hkexnews.hk | Annual report PDFs |

### China A-Shares (e.g., 37Games, GigaMedia, etc.)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **Eastmoney** | finance.eastmoney.com → search ticker → financials | Direct |
| 2 (Secondary) | **CNINFO** | cninfo.com.cn | Official annual/quarterly report PDFs |

---

## Execution Protocol

### Step 1: Fetch Data

For each financial metric (revenue, net income, gross margin, operating cash flow, debt ratio, etc.), pull figures separately from **Source 1** and **Source 2**.

### Step 2: Calculate and Flag Deviations

```
Deviation = |Source 1 value − Source 2 value| / Source 1 value × 100%
```

| Deviation | Action |
|-----------|--------|
| ≤ 1% | ✅ Consistent — use Source 1 value, cite both sources |
| 1%–5% | ⚠️ Flag as "data discrepancy" — show both values, note likely cause (FX / accounting scope) |
| > 5% | ❌ Flag as "material data discrepancy" — must verify against original filing before use |

### Step 3: Data Presentation Format

Every key data point must be annotated in the following format:

```
Revenue: $12.39B ✅
  - Macrotrends: $12.41B
  - Stock Analysis: $12.37B
  - Deviation: 0.3%
```

Discrepancy example:
```
Net income: $2.45B ⚠️ Data discrepancy
  - Macrotrends: $2.45B (GAAP)
  - Stock Analysis: $2.78B (Non-GAAP)
  - Deviation: 13.5% — Reason: different accounting scope (GAAP vs. Non-GAAP)
```

---

## Common Reasons for Discrepancies (not necessarily data errors)

| Reason | Explanation |
|--------|-------------|
| GAAP vs. Non-GAAP | Most common, especially for earnings metrics |
| Currency conversion | Different FX rates or conversion dates for HKD/CNY/USD |
| Fiscal year definition | Calendar year vs. fiscal year (e.g., Apple's fiscal year ends in October) |
| Consolidation scope | Whether minority interests are included |
| Data update lag | A platform hasn't yet updated for the latest report period |

---

## Special Rules

1. **Private companies** (e.g., miHoYo, Lilith Games): When only one primary data source is available, mark data as `[Est.]` and do not execute cross-validation
2. **Quarterly vs. annual data**: Prefer annual data for cross-validation; some sources may lag on quarterly data
3. **Primary filing takes precedence**: If both sources conflict with the original filing (10-K / annual report PDF), use the original filing and flag the source as incorrect

---

## Quick Reference

| Scenario | Primary Source | Backup Source |
|----------|---------------|--------------|
| PDD / Pinduoduo | macrotrends.net/stocks/charts/PDD | stockanalysis.com/stocks/pdd |
| Tencent | macrotrends.net/stocks/charts/TCEHY | aastocks (0700.HK) |
| NetEase | macrotrends.net/stocks/charts/NTES | aastocks (9999.HK) |
| A-share company | finance.eastmoney.com ({ticker}) | cninfo.com.cn |
| Nintendo | macrotrends.net/stocks/charts/NTDOY | stockanalysis.com/stocks/ntdoy |
| Capcom | macrotrends (CCOEY) | stockanalysis (CCOEY) |
