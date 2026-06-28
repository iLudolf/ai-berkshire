# Earnings Deep Read: Primary Source Analysis

Perform an earnings deep read analysis on $ARGUMENTS.

**Supported input formats**: `Company Quarter`, e.g.: `PETR4 2025Q4`, `VALE3 FY2025`, `MXRF11 latest`, `ITUB4 2025Q3` (defaults to most recent period)

> "I never read sell-side research. I only read the original filings." — Li Lu
>
> "I read 500 pages a day. That's how knowledge builds — like compound interest." — Buffett

## Design Philosophy

Most AI investment research tools rely on secondary information (news, research summaries, data websites). But Buffett and Li Lu's core edge is **reading primary sources** — annual reports, quarterly reports, earnings call transcripts.

The problem with secondary information:
- It's filtered — analysts selectively present data that supports their view
- It's delayed — by the time others have digested it, the alpha is gone
- It lacks context — "revenue grew 15%" strips away management's discussion of growth quality

This Skill reads primary sources directly, focusing on what Buffett and Li Lu actually look for.

## Execution Flow

### Pre-Step: Data Availability Rating

| Grade | Characteristics | Impact |
|-------|----------------|--------|
| A | Full original text obtained (10-K / annual report / earnings call transcript) | Execute all steps normally |
| B | Only partial original text or third-party summary obtained | Label "non-primary source," reduce weight of footnote analysis |
| C | Only news coverage and data website summaries available | Focus on core financial data changes, skip footnote mining, label "insufficient primary sources" |

### Step 1: Obtain Primary Sources

Use the Task tool to launch multiple background Agents **in parallel** to retrieve the following original materials:

**For Brazilian equities (B3):**
1. **DFP** (Demonstrações Financeiras Padronizadas) — annual report filed with CVM; obtain from cvmweb.cvm.gov.br or the company's RI (Relações com Investidores) page
2. **ITR** (Informações Trimestrais) — quarterly report filed with CVM; same sources
3. **Release de Resultados** — earnings press release, typically PDF on the RI page
4. **Teleconferência de Resultados** (earnings call): transcript or audio from the company's RI page; some companies post on YouTube or publish a transcript
5. **Carta aos Acionistas** (shareholder letter, if annual): read in full

**For FIIs:**
1. **Informe Mensal** (monthly CVM filing) — most critical primary source; cvmweb.cvm.gov.br → Fundos → Informes Mensais
2. **Relatório Gerencial** — monthly management report published by the fund manager (PDF on fund's website or FundsExplorer)
3. **Fato Relevante** — material fact disclosure (extraordinary events); cvmweb.cvm.gov.br

**For US stocks:**
1. **10-K / 10-Q**: SEC EDGAR (sec.gov/cgi-bin/browse-edgar)
2. **Earnings call transcript**: Seeking Alpha or company IR page

If the full original text cannot be obtained, piece together from standard data sources per `skills/financial-data.md` (B3 stocks: Fundamentus + Status Invest; FIIs: FundsExplorer + CVM Informe Mensal; US stocks: Macrotrends + Stock Analysis), but must label "not original filing, sourced from third-party aggregator," and flag key data points where two sources diverge by >1%.

### Step 2: Core Financial Data Extraction and Validation

#### 2.1 Revenue and Income Statement

| Metric | Current Period | Prior Period | YoY Change | Management Guidance | Beat/Miss |
|--------|---------------|-------------|-----------|--------------------:|:--------:|

Must cover:
- Total revenue and breakdown by business segment / geography
- Gross profit and gross margin changes
- Operating profit and operating margin changes (distinguish GAAP vs Non-GAAP)
- Net income (note impact of non-recurring items)
- EPS (basic vs diluted)

#### 2.2 Cash Flow Statement (Buffett's Top Priority)

| Metric | Current Period | Prior Period | Change | Key Watch |
|--------|---------------|-------------|--------|-----------|

Must cover:
- Operating cash flow vs net income ratio (>100% preferred; <80% warrants caution)
- Capital expenditure and its composition (maintenance vs expansion)
- Free cash flow = operating cash flow − CapEx
- Buyback amount, dividend amount
- Cash and equivalents ending balance

#### 2.3 Balance Sheet Health

Must cover:
- Cash + short-term investments vs interest-bearing debt
- Net cash / net debt trend
- Accounts receivable days change (is the company loosening credit terms to boost revenue?)
- Inventory days change (is inventory building up?)
- Goodwill and intangible assets as a share of total assets (impairment risk?)

**Data Validation**: Use `tools/financial_rigor.py` to verify key data:

```bash
# Cross-validate revenue and net income (at least 2 sources)
python3 tools/financial_rigor.py cross-validate \
  --metric "revenue" --values 108.3e9 107.9e9 --sources "Company Filing" "Yahoo Finance"

# Market cap verification
python3 tools/financial_rigor.py verify-market-cap \
  --price 101 --shares 1.488e9 --reported 1.44e11 --currency USD

# Valuation metrics verification
python3 tools/financial_rigor.py verify-valuation \
  --price 101 --eps 9.6 --bvps 26.5 --fcf-per-share 10.2
```

### Step 3: Deep Read of Management Discussion (MD&A)

This is where Buffett and Li Lu spend the most time. It is not about reading the numbers — it is about **listening to how management speaks**.

#### 3.1 Management Tone Analysis

Read through management discussion / earnings call remarks paragraph by paragraph and flag the following signals:

| Signal Type | Specific Manifestation | Example |
|------------|----------------------|---------|
| 🟢 **Candor signal** | Proactively acknowledges problems, provides specific reasons | "Margin compression this quarter was primarily due to our investment in X exceeding expectations" |
| 🟢 **Clarity signal** | Strategic narrative is specific, with quantified targets | "We plan to grow X segment's market share from 15% to 20% over the next 12 months" |
| 🔴 **Vagueness signal** | Heavy use of "we believe," "over the long term," and other content-free phrases | "We are very confident about the future" |
| 🔴 **Deflection signal** | Avoids direct questions, pivots to other topics | Asked about margins, pivots to revenue growth |
| 🔴 **External attribution** | Blames all problems on macro / industry / competitors | "Due to macro headwinds..." |

#### 3.2 Commitment Tracking

Extract specific commitments management made in the prior period's report / call, and compare with actual results this period:

| Prior Commitment | Current Period Outcome | Assessment |
|-----------------|----------------------|-----------|
| "Margins will recover to X% in H2" | Actual Y% | ✅ Achieved / ❌ Missed / ⚠️ Partially achieved |

**Duan Yongping**: "The simplest way to judge whether management is reliable is to check whether they did what they said they would do."

#### 3.3 Key Question Identification

Extract the sharpest analyst questions from the earnings call Q&A, and assess the quality of management's responses:

| Analyst Question | Management Response | Response Quality (1–5) | Evasive? |
|----------------|--------------------|-----------------------:|:-------:|

### Step 4: Footnotes and Hidden Information Mining

Footnotes contain information management would prefer you not find easily:

#### 4.1 Must-Check Footnote Items

- [ ] **Related-party transactions**: Are the terms of transactions with major shareholders / related parties fair?
- [ ] **Equity compensation**: How large is the dilution from options / RSUs? What are the strike prices?
- [ ] **Contingent liabilities**: Off-balance-sheet risks — litigation, guarantees, commitments
- [ ] **Accounting policy changes**: Has the company changed revenue recognition methods, depreciation useful lives, etc.?
- [ ] **Segment information**: Margin differences across business lines — is a "good business" subsidizing a "bad business"?
- [ ] **Customer / supplier concentration**: Top five customers / suppliers as a share of totals

#### 4.2 Anomaly Signal Detection

- [ ] Accounts receivable growth > revenue growth (possible channel stuffing)
- [ ] Inventory growth > revenue growth (possible inventory buildup)
- [ ] Operating cash flow < net income with a widening gap (earnings quality questionable)
- [ ] Capitalized expenditures suddenly increase (possible earnings beautification)
- [ ] Non-recurring income as a share of total suddenly rises

### Step 5: Historical Comparison

#### 5.1 Trend Analysis

Place key metrics for the current period into a time series of at least 4 quarters (or 3 years of annual reports):

| Metric | Q-4 | Q-3 | Q-2 | Q-1 | Current | Trend Judgment |
|--------|-----|-----|-----|-----|---------|---------------|

Focus areas:
- Are margins improving or deteriorating?
- Is revenue growth accelerating or decelerating?
- Is cash flow quality improving or declining?
- Is CapEx intensity increasing or decreasing?

#### 5.2 Comparison with Management Guidance

| Metric | Prior Management Guidance | Actual Result | Variance | Interpretation |
|--------|--------------------------|--------------|---------|----------------|

### Step 6: Output the Deep Read Report

#### Report Structure

```
I.   Core Data Snapshot (one-page table)
II.  The 3 Most Important Changes This Period (500 words max)
III. Management Tone and Commitment Tracking
IV.  Hidden Information in Footnotes
V.   Key Questions (Selected Earnings Call Q&A)
VI.  Relationship to Investment Thesis (if position held)
VII. Conclusion: What Did This Earnings Report Change?
```

#### Conclusion Must Clearly Answer

1. **Did this report beat, meet, or miss expectations?** (Cannot say "broadly in line" then list both sides of the argument)
2. **Impact on investment thesis**: Reinforces / No impact / Weakens / Thesis broken
3. **What is the next catalyst to watch?**
4. **If you already hold a position, should you add / hold / reduce?**

### Step 7: Save the Report

Write the report to `reports/{CompanyName}/{CompanyName}-earnings-{Period}.md`, e.g. `reports/Petrobras/Petrobras-earnings-2025Q4.md` or `reports/MXRF11/MXRF11-results-2025-06.md`

### Step 8: Data Spot-Check (Release Gate)

After writing the report, run the data spot-check. The report may only be published after passing:

```bash
# Step 1 — Extract spot-check checklist
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report reports/{CompanyName}-earnings-{Period}.md

# Step 2 — For each item on the checklist, retrieve the figure from a reliable source (see skills/financial-data.md)

# Step 3 — Output pass/fail verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report {report-filename}
```

**[PASS]** All items pass → publish; **[FAIL]** Any item fails → correct and re-review.

## Core Principles

- **Read the original, not the summary**: Make every effort to obtain primary sources
- **Watch for changes, not absolute values**: Trends matter more than the numbers themselves
- **Listen to tone, not just content**: How management says something matters as much as what they say
- **Check the footnotes, not just the main text**: The devil is in the details
- **Give a verdict, not a summary**: The purpose of a deep read is to form a judgment, not to restate the filing
