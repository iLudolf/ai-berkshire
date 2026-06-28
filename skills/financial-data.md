# Financial Data: Source Priority & Cross-Validation Standards

This standard applies to all research involving company financial data. **Every key data point must come from two independent sources; deviations > 1% must be flagged.**

---

## Data Source Priority

### Brazilian Equities — B3 (e.g., PETR4, VALE3, ITUB4, ABEV3, WEGE3)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **Fundamentus** | fundamentus.com.br/detalhes.php?papel={ticker} | Direct, no login |
| 2 (Secondary) | **Status Invest** | statusinvest.com.br/acoes/{ticker} | Direct, no login |
| Official filings | **CVM** | cvmweb.cvm.gov.br (DFP / ITR / FRE forms) | Free, searchable |
| Official exchange | **B3** | b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel | Direct |
| Investor relations | **Company RI** | ri.{company}.com.br | Annual reports, earnings releases |

**Key metrics for B3 equities**: P/L (PE), P/VPA (P/B), ROE, Dividend Yield, Dívida Líquida/EBITDA, Margem Líquida, CAGR Receita 5 anos

### FIIs — Fundos de Investimento Imobiliário (e.g., MXRF11, KNRI11, HGLG11, BCFF11)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **FundsExplorer** | fundsexplorer.com.br/funds/{ticker} | Direct, no login |
| 2 (Secondary) | **Status Invest** | statusinvest.com.br/fundos-imobiliarios/{ticker} | Direct, no login |
| 3 (Supporting) | **Investidor10** | investidor10.com.br/fiis/{ticker} | Direct, no login |
| Official filings | **CVM — Informe Mensal** | cvmweb.cvm.gov.br → Fundos → Informes Mensais | Free, standardized |
| Fund reports | **Relatório Gerencial** | Fund manager's official monthly report (PDF) | Fund website |

**Key FII metrics**:
| Metric | Description |
|--------|-------------|
| DY (Dividend Yield) | Monthly distribution ÷ current price × 12 (annualized) |
| P/VP | Price ÷ Net Asset Value per share (< 1 = discount to book) |
| Vacância Física | % of physical area unoccupied |
| Vacância Financeira | % of potential revenue lost to vacancies |
| Taxa de Gestão | Annual management fee (% of AUM) |
| Taxa de Administração | Annual administration fee |
| Liquidez Diária | Average daily trading volume (BRL) |
| Tipo | Papel (CRI/CRA), Tijolo (physical real estate), Híbrido, FOF |

**FII types — key differences**:
- **Tijolo**: Physical assets (logistics, office, retail malls, hospitals). Revenue = rent. Analyze vacancy + lease renewals.
- **Papel**: Invests in CRIs/CRAs (real estate receivables). Revenue = interest. Analyze credit risk + CDI/IPCA indexation.
- **Híbrido**: Mix of tijolo and papel.
- **FOF (Fund of Funds)**: Invests in other FIIs. Analyze portfolio composition + management quality.

### US Stocks (e.g., Berkshire, Visa, Apple)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **Macrotrends** | macrotrends.net/stocks/charts/{ticker} | Direct, no login |
| 2 (Secondary) | **Stock Analysis** | stockanalysis.com/stocks/{ticker}/financials | Direct, no login |
| Official filings | **SEC EDGAR** | sec.gov/cgi-bin/browse-edgar | 10-K / 10-Q originals |

### BDRs — Brazilian Depositary Receipts (US/global stocks traded on B3)

| Priority | Source | URL | Access |
|----------|--------|-----|--------|
| 1 (Primary) | **Status Invest** | statusinvest.com.br/bdrs/{ticker} | Direct |
| 2 (Secondary) | **Fundamentus** (BDR section) | fundamentus.com.br/detalhes.php?papel={ticker} | Direct |
| Underlying stock | Use US stock sources above for the underlying company's financials | | |

---

## Execution Protocol

### Step 1: Fetch Data

For each financial metric (revenue, net income, gross margin, operating cash flow, debt ratio, etc.), pull figures separately from **Source 1** and **Source 2**.

For FIIs, additionally verify the **CVM Informe Mensal** as the authoritative official source.

### Step 2: Calculate and Flag Deviations

```
Deviation = |Source 1 value − Source 2 value| / Source 1 value × 100%
```

| Deviation | Action |
|-----------|--------|
| ≤ 1% | ✅ Consistent — use Source 1 value, cite both sources |
| 1%–5% | ⚠️ Flag as "data discrepancy" — show both values, note likely cause |
| > 5% | ❌ Flag as "material data discrepancy" — must verify against official filing before use |

### Step 3: Data Presentation Format

Every key data point must be annotated in the following format:

```
Receita Líquida 2024: R$ 539.2B ✅
  - Fundamentus: R$ 539.2B
  - Status Invest: R$ 539.1B
  - Deviation: 0.02%
```

Discrepancy example:
```
DY MXRF11 (12M): 14.2% ⚠️ Data discrepancy
  - FundsExplorer: 14.2% (trailing 12 months)
  - Status Invest: 13.8% (different calculation window)
  - Reason: different trailing period definition
```

---

## Brazilian Market — Special Considerations

| Issue | Explanation |
|-------|-------------|
| IPCA indexation | Many FII CRIs and debentures are indexed to IPCA — distinguish nominal vs. real yield |
| CDI spread | Papel FIIs often quoted as CDI + X%; verify current CDI rate (≈ Selic - 0.1%) |
| Selic sensitivity | Rising Selic compresses FII P/VP and competes with DY as risk-free alternative |
| JCP (Juros sobre Capital Próprio) | Brazilian tax-efficient dividend substitute — counts as deductible expense for companies |
| IR isento | FII distributions to individuals are tax-exempt if fund has 50+ shareholders and is listed on B3 |
| Fiscal year | Brazilian companies report by calendar year (Jan–Dec); quarterly ITRs in Mar/Jun/Sep/Dec |

---

## Special Rules

1. **FII Informe Mensal is authoritative**: For FII metrics (DY, vacancy, AUM), the CVM Informe Mensal beats any aggregator — use it to cross-check if sources disagree > 5%
2. **Quarterly vs. annual data**: Prefer annual DFP for cross-validation; ITRs (quarterly) may be restated
3. **Private companies** (e.g., pre-IPO Brazilian startups): When only one source is available, mark data as `[Est.]` and do not execute cross-validation
4. **Official filing takes precedence**: If both sources conflict with the DFP/ITR/FRE filing, use the filing and flag the source as incorrect

---

## Quick Reference

| Scenario | Primary Source | Backup Source |
|----------|---------------|--------------|
| B3 equity (PETR4, VALE3, WEGE3) | fundamentus.com.br | statusinvest.com.br/acoes |
| B3 equity (ITUB4, BBDC4 banks) | fundamentus.com.br | statusinvest.com.br/acoes |
| FII — Tijolo (HGLG11, XPML11) | fundsexplorer.com.br | statusinvest.com.br/fundos-imobiliarios |
| FII — Papel (MXRF11, KNCR11) | fundsexplorer.com.br | investidor10.com.br/fiis |
| FII — FOF (BCFF11, RBFF11) | fundsexplorer.com.br | statusinvest.com.br/fundos-imobiliarios |
| Official filing (any B3 asset) | cvmweb.cvm.gov.br | ri.{company}.com.br |
| BDR (AAPL34, MSFT34) | statusinvest.com.br/bdrs | fundamentus.com.br |
| US equity (Berkshire, Visa) | macrotrends.net/stocks/charts/{ticker} | stockanalysis.com/stocks/{ticker} |
