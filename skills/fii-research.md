# FII Research: Deep Analysis of Brazilian Real Estate Investment Trusts

Run a comprehensive research analysis on $ARGUMENTS (a FII ticker or name).

**Supported input formats**: FII ticker or name, e.g.: `MXRF11`, `KNRI11`, `HGLG11 XPML11`, `BCFF11`

> "A great investment is one where even if you're wrong about the upside, you still don't lose money." — Buffett
>
> "The most important thing is that the business model actually makes sense, and that the manager is aligned with the investor." — Li Lu

---

## Design Philosophy

FIIs are not stocks. Analyzing them requires a different framework:

- **The primary return driver is the distribution yield (DY)**, not earnings growth
- **The risk is credit (Papel FIIs) or real estate (Tijolo FIIs)**, not competitive dynamics
- **The benchmark is Selic/CDI**, not the Ibovespa — a FII that underperforms Tesouro Selic is destroying investor value
- **Sustainability of dividends** matters more than their current level — a DY of 16% from capital gains disguised as income is a trap

The Four Masters framework applies differently here:
- **Buffett**: Is the distribution truly sustainable cash from real assets/receivables, or financial engineering?
- **Munger**: Invert — what would kill this fund's distribution? Vacancy spike? CDI collapse? Manager fraud?
- **Li Lu**: Is the real estate / credit market this fund operates in at an early or late stage of its cycle?
- **Duan Yongping**: Is the fund manager doing the right things, or optimizing short-term optics?

---

## Execution Flow

### Pre-Step: FII Type Classification

Before any analysis, determine the FII type — it drives the entire research framework:

| Type | Description | Primary Metric | Main Risk |
|------|-------------|---------------|-----------|
| **Tijolo — Logística** | Logistics / warehouse real estate | Physical vacancy, rent/m² | Oversupply, e-commerce demand |
| **Tijolo — Shopping** | Shopping malls | Mall revenue share, vacancy | Consumer spending, online competition |
| **Tijolo — Lajes** | Office buildings | Vacancy, ABL (rentable area) | Remote work, economic cycle |
| **Tijolo — Hospitalar** | Hospitals / healthcare | Lease terms, operator quality | Single-tenant risk |
| **Papel — CRI** | Real estate credit receivables | CDI/IPCA spread, LTV, default rate | Credit default, rate cycle |
| **Papel — CRA** | Agribusiness receivables | Similar to CRI | Agro cycle, political |
| **Híbrido** | Mix of Tijolo + Papel | Weighted analysis of both | Both risks combined |
| **FOF** | Fund of funds (invests in other FIIs) | Portfolio composition, manager quality | Concentration, double fee layer |
| **Desenvolvimento** | Development / construction | Project pipeline, pre-sale coverage | Construction delays, delivery risk |

### Step 1: Data Collection

Use the Task tool to launch parallel agents:

**Agent A — FII Fundamentals (FundsExplorer + Status Invest)**

Collect the following from FundsExplorer and Status Invest:

| Metric | Value | Source |
|--------|-------|--------|
| Tipo de FII | | |
| Gestor / Administrador | | |
| Data de início | | |
| Patrimônio Líquido (R$) | | |
| Número de cotas | | |
| Número de cotistas | | |
| Cotas em circulação | | |
| Preço atual da cota | | |
| P/VP atual | | |
| DY (último mês, anualizado) | | |
| DY (12 meses) | | |
| Vacância física (Tijolo only) | | |
| Vacância financeira (Tijolo only) | | |
| Taxa de gestão (% a.a.) | | |
| Taxa de administração (% a.a.) | | |
| Liquidez média diária | | |

**Agent B — CVM Official Filings (Informe Mensal + Relatório Gerencial)**

From cvmweb.cvm.gov.br and the fund manager's official monthly report:
- Most recent Informe Mensal (past 3 months)
- Most recent Relatório Gerencial (manager's own report)
- Any Fatos Relevantes in the past 6 months

**Agent C — Historical Distribution Track Record**

From FundsExplorer or Status Invest, collect the last 12–24 months of monthly distributions:
- Monthly dividend per share (historical)
- Identify any one-time events (sale of assets, capital gains distributed as income)
- Trend: Is DY rising, stable, or falling?

#### Data Cross-Validation (Mandatory)

```bash
python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
  --price {current_price} --shares {total_shares} --reported {reported_PL} --currency BRL
```

Flag if P/VP calculated from verified data differs from reported P/VP by >1%.

---

### Step 2: Distribution Sustainability Analysis

This is the most important analysis for any FII. **A high DY is only valuable if it is recurring and sustainable.**

#### 2.1 Income Quality Breakdown

Identify the source of each distribution:

| Source Type | Sustainable? | Red Flag? |
|-------------|:------------:|:---------:|
| Rental income (Tijolo) — contractual rents | ✅ Yes | No |
| Interest income from CRIs/CRAs (Papel) | ✅ Yes | Check default rate |
| Capital gains from asset sales | ❌ One-time | ⚠️ If recurring = fund selling assets |
| Amortization of book losses | ❌ One-time | |
| Income from cash reserves | Partial | Reduces over time |

**Flag**: If the fund has been paying distributions above the income it generates from its assets, it is either: (a) distributing capital gains from asset sales, or (b) depleting its cash reserve. Both inflate DY artificially.

#### 2.2 DY vs. Selic/CDI Spread

The critical benchmark:

```
Real DY spread = DY (annualized, 12M) − Selic rate
```

| Spread | Interpretation |
|--------|----------------|
| < 0% | Destroying value vs. risk-free — requires extraordinary reason to hold |
| 0%–2% | Barely compensates for illiquidity and real estate risk — likely a hold, not a buy |
| 2%–5% | Reasonable risk premium for a stable, quality FII |
| > 5% | Attractive — but investigate why the market prices it this cheap |

**Munger inversion**: Why is the DY so high relative to Selic? Is it mispricing, or is the market pricing in real risk?

#### 2.3 For Tijolo FIIs: Vacancy and Lease Analysis

| Metric | Current | 3M Ago | 6M Ago | Trend |
|--------|---------|--------|--------|-------|
| Vacância física (%) | | | | |
| Vacância financeira (%) | | | | |
| ABL total (m²) | | | | |
| Renda por m² (R$/m²/mês) | | | | |

**Key questions:**
- What is the market vacancy rate in the fund's property type and location?
- Are leases expiring soon? What are the renewal or renegotiation prospects?
- Are leases indexed to IPCA (inflation protection) or fixed?
- What is the weighted average remaining lease term (WAULT)?

#### 2.4 For Papel FIIs: Credit Portfolio Analysis

| Metric | Value |
|--------|-------|
| Composição: % CRI / CRA / outros | |
| Indexação: % CDI / IPCA / IGPM / prefixado | |
| LTV médio (Loan to Value) | |
| Prazo médio dos CRIs | |
| Devedores concentrados? (% no maior devedor) | |
| Histórico de inadimplência | |

**Key questions:**
- If CDI drops 300bps, how much does the DY fall (for CDI-indexed Papel FIIs)?
- What is the LTV — if real estate collateral is foreclosed, does it cover the CRI balance?
- Is there concentration risk (one devedor = 20%+ of portfolio)?

---

### Step 3: Management and Governance Assessment

#### 3.1 Manager Quality

| Criterion | Assessment |
|-----------|-----------|
| Gestor's track record (years operating FIIs) | |
| AUM under management (other funds managed) | |
| Relatório Gerencial quality: transparent and detailed, or vague? | |
| Recent Fatos Relevantes: any controversies or conflicts of interest? | |
| Manager's skin in the game (do key people hold units of this fund?) | |
| History of related-party transactions | |

**Duan Yongping test**: "Is the manager doing the right things — maximizing long-term unit holder value — or optimizing short-term optics (inflating DY with one-time gains, delaying vacancy disclosure)?"

#### 3.2 Fee Structure

```
All-in annual cost = taxa de gestão + taxa de administração + other fees
```

| Fee Level | Assessment |
|-----------|-----------|
| < 0.5% a.a. | Very competitive |
| 0.5%–1.0% a.a. | Market average — acceptable if justified by performance |
| > 1.0% a.a. | High — requires exceptional track record to justify |
| Performance fee | Check the hurdle rate — CDI+ hurdle is investor-aligned; absolute return hurdle is not |

---

### Step 4: Portfolio / Asset Quality Assessment

#### For Tijolo FIIs:

| Criterion | Assessment |
|-----------|-----------|
| Location quality of properties | |
| Property age and condition | |
| Tenant quality (credit rating, contract terms) | |
| Property concentration (single asset vs. diversified) | |
| Replacement cost vs. current market valuation | |

**Buffett test**: "If you had to sell this real estate portfolio today in a distressed scenario, what would you get? Does that cover the fund's current market cap?"

#### For Papel FIIs:

| Criterion | Assessment |
|-----------|-----------|
| Guarantor quality for CRIs | |
| Underlying asset quality (commercial, residential, agro) | |
| Geographic diversification | |
| Term diversification | |
| Indexation mix risk | |

---

### Step 5: Valuation — P/VP Analysis

P/VP (Preço / Valor Patrimonial) is the primary valuation metric for FIIs:

| P/VP | Interpretation |
|------|----------------|
| < 0.85 | Significant discount to NAV — attractive if quality is confirmed |
| 0.85–0.95 | Moderate discount — fair entry point |
| 0.95–1.05 | Near fair value |
| 1.05–1.20 | Premium to NAV — justified only by exceptional management or irreplaceable assets |
| > 1.20 | Expensive — market pricing in significant future growth (rare for FIIs) |

**Critical caveat**: P/VP is only meaningful if the VP (Valor Patrimonial) is credible. For Tijolo FIIs, check when the properties were last independently appraised. For Papel FIIs, verify that CRIs are marked to market and not at face value with unrealized impairment.

#### Peer Comparison

Compare the FII against 3–5 peers of the same type:

| FII | DY 12M | P/VP | Vacância | Taxa Gestão | DY Spread vs. Selic | Quality Score |
|-----|:------:|:----:|:--------:|:-----------:|:-------------------:|:------------:|
| {Subject} | | | | | | |
| Peer A | | | | | | |
| Peer B | | | | | | |
| Peer C | | | | | | |

---

### Step 6: Risk Assessment — Munger's "Think It Through Backwards"

**The three scenarios that would destroy this FII's distribution:**

| Scenario | Probability | Impact | Mitigation |
|----------|:-----------:|:------:|-----------|
| Selic rises to 18%+ | | | |
| Major tenant defaults / exits (Tijolo) | | | |
| CRI debtor defaults (Papel) | | | |
| BRL depreciation + IPCA spike | | | |
| Regulatory change (IR isento status removed) | | | |
| Manager conflict of interest / governance failure | | | |

**Structural risk check:**
- [ ] FII has 50+ shareholders? (Required for IR isento status — check CVM)
- [ ] Fund is listed on B3? (Required for IR isento)
- [ ] Are there any open CVM investigations against the manager?
- [ ] Is there a concentrated institutional holder (> 20%) who could force a liquidation?

---

### Step 7: Final Verdict

#### Summary Scorecard

| Dimension | Score (★1–5) | Key Finding |
|-----------|:-----------:|------------|
| Distribution sustainability | | |
| DY vs. Selic spread | | |
| Asset / credit quality | | |
| Management trustworthiness | | |
| Valuation (P/VP) | | |
| Liquidity | | |
| **Overall** | | |

#### Four Masters' Simulated Commentary

> **Buffett**: {Is the distribution truly cash from durable assets, or financial engineering?}

> **Munger**: {What's the worst that could happen? Is the market properly pricing that risk?}

> **Duan Yongping**: {Is the manager doing the right things, or just the things that look good short-term?}

> **Li Lu**: {Is the underlying real estate or credit market at a favorable point in its cycle?}

#### Investment Decision

| Scenario | Recommendation |
|----------|---------------|
| No position today | Buy / Wait / Avoid + specific condition or price |
| Currently holding | Add / Hold / Reduce / Exit + rationale |
| Sell signal | What specific event triggers a sale? |

---

### Step 8: Save the Report

Write the full report to `reports/{FII-ticker}/{FII-ticker}-research-{YYYYMMDD}.md`

Example: `reports/MXRF11/MXRF11-research-20260701.md`

### Step 9: Data Spot-Check (Release Gate)

```bash
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report reports/{FII-ticker}/{FII-ticker}-research-{YYYYMMDD}.md

python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report {report-filename}
```

---

## Core Principles

- **DY is not income until verified sustainable**: The most common FII trap is chasing a 16% DY that's 30% capital gains in disguise
- **Selic is the real benchmark**: Any FII that doesn't clearly beat CDI with a risk premium is a failed investment
- **Manager alignment matters more than in stocks**: FII investors are passive — you cannot vote the manager out
- **P/VP discount is not always value**: A Tijolo FII with 30% vacancy at 0.70x P/VP may be fair value — not cheap
- **Liquidity is a real cost**: Low-liquidity FIIs (< R$ 500K/day) should only be held as long-term positions, not tactical trades
