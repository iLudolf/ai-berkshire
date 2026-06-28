# Supply Chain Bottleneck Hunter: AI-Driven Global Supply Chain Bottleneck Arbitrage

Execute a supply chain bottleneck scan and arbitrage opportunity discovery for $ARGUMENTS super-trend.

## Core Philosophy

Don't ask "what stock does AI recommend?" — ask "if this trend keeps expanding, which link will run short first?"

Traditional investment research chases leaders and known sectors. This system inverts that: **start from the chokepoint of the physical supply chain and find companies that nobody is watching — but the moment they go out of stock, the entire industry grinds to a halt and waits.**

Source of excess returns: first-layer bottlenecks (GPU, HBM, power) are already fully priced in. The real alpha lies in **the second and third layers** — optical transceivers, lasers, InP substrates, SOI wafers, epitaxy equipment, wafer-level testing, IC substrates, specialty glass fiber, and more.

---

## Step 1: Super-Trend Confirmation

### 1.1 Trend Screening Criteria

Don't chase illusions in minor tailwinds — only pursue super-trends that meet all of the following conditions:

| Criterion | Requirement | Verification Method |
|-----------|-------------|---------------------|
| Durability | At least 3–5 years of certain growth | Search industry forecasts, CapEx plans |
| Physical nature | Requires actual hardware / materials / equipment buildout | Distinguish "software upgrade" from "physical expansion" |
| Scale | Global CapEx > $50B/year | Search leading players' capex guidance |
| Acceleration | Demand growth rate > supply expansion rate | Compare demand growth vs. capacity expansion plans |

### 1.2 Current Super-Trend Tracking List

Update on each run; initial list:

1. **AI Infrastructure Buildout** — data centers, GPU clusters, network interconnects, power
2. **Energy Transition** — nuclear restart, grid upgrades, energy storage
3. **Defense Modernization** — Western defense spending upcycle, supply chain restructuring
4. **Semiconductor Re-industrialization** — US/EU/Japan subsidized fab construction, equipment/materials bottlenecks
5. **Space Economy** — satellite internet, rapidly increasing launch cadence

If the user specifies a particular trend (e.g., "AI infrastructure"), focus solely on that trend.

### 1.3 Trend Validation Output

```
Trend Name:
Core Driver: (one sentence)
Validation Events (at least 3):
  1. [Date] [Event] [Source]
  2.
  3.
CapEx Scale: Globally ~$XX billion/year, growth rate YY%
Supply-Demand Gap Assessment: Demand growth > supply expansion rate? Yes / No / Uncertain
Trend Confirmed: ✅ Trackable / ❌ Insufficient evidence, not tracking for now
```

---

## Step 2: Physical Supply Chain Decomposition

### 2.1 Layered Decomposition Framework

**Don't stay at the concept level — decompose down to physical entities.**

```
Layer 0 (End Product): Final product / service
    │
Layer 1 (Core Components): Core hardware already receiving full market attention
    │                 ⬆ Fully priced, limited alpha
    │─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
    │                 ⬇ Low attention, alpha concentration zone
    │
Layer 2 (Sub-components / Materials): Parts and materials supporting core components
    │
Layer 3 (Upstream Equipment / Raw Materials): Equipment and raw materials for manufacturing sub-components
    │
Layer 4 (Infrastructure): Power, cooling, land, talent, certifications
```

### 2.2 Decomposition Template Using AI Infrastructure as an Example

```
Layer 0: AI model training / inference services
Layer 1: GPU / accelerators, HBM memory, servers, data centers
Layer 2 (Primary scan zone):
  ├─ Network interconnects: optical transceivers, fiber, switch chips, copper cables
  ├─ Optical communication core: lasers (EML/VCSEL/CW), modulators, photodetectors
  ├─ Semiconductor materials: InP substrates, GaAs substrates, SOI wafers, SiC substrates
  ├─ Advanced packaging: CoWoS substrates, HBM TSV, ABF substrate film
  ├─ PCB / substrates: high-frequency high-speed PCB, IC substrates, specialty glass fiber cloth
  ├─ Testing: wafer-level testing (Probe Card), burn-in testing, ATE
  ├─ Thermal / cooling: liquid cooling systems, CDUs, immersion cooling fluid
  └─ Power distribution: busway, UPS, distribution cabinets, transformers
Layer 3:
  ├─ Epitaxy equipment: MOCVD, MBE
  ├─ Lithography / etching: special-wavelength lithography, InP etching
  ├─ Raw materials: high-purity metals (indium, gallium, germanium), specialty gases, sputtering targets
  └─ Certifications / standards: MSA standards, Telcordia certification
Layer 4:
  ├─ Power: nuclear, natural gas generation, transmission and distribution
  ├─ Cooling water / thermal infrastructure
  └─ Data center land / permits
```

### 2.3 Decomposition for Other Trends

Perform a similar decomposition for each confirmed super-trend. Use WebSearch to search:
- "{trend} supply chain bottleneck 2026"
- "{trend} shortage critical component"
- "{trend} capacity constraint"
- "{trend} sole source supplier"

---

## Step 3: Bottleneck Identification — Finding the "Chokepoint"

### 3.1 Six Criteria for Bottleneck Assessment

Evaluate each Layer 2–3 segment against every criterion:

| # | Criterion | Question | Score |
|---|-----------|----------|-------|
| 1 | **Supply concentration** | ≤3 global suppliers? | 🔴 ≤2 / 🟡 3–5 / 🟢 >5 |
| 2 | **Capacity expansion lead time** | How long to add new capacity? | 🔴 >2 years / 🟡 1–2 years / 🟢 <1 year |
| 3 | **Substitutability** | Can other technology / material substitute? | 🔴 Irreplaceable / 🟡 Partially substitutable / 🟢 Easily substituted |
| 4 | **Capacity utilization** | Current utilization rate? | 🔴 >90% / 🟡 70–90% / 🟢 <70% |
| 5 | **Demand growth rate** | Downstream demand growth? | 🔴 >50%/year / 🟡 20–50% / 🟢 <20% |
| 6 | **Customer qualification lead time** | How long for a new supplier to qualify? | 🔴 >1 year / 🟡 6–12 months / 🟢 <6 months |

**Bottleneck Rating**:
- 🔴🔴🔴 ≥4 → **S-tier Bottleneck** (single point of failure, highest priority)
- 🔴🔴 3 → **A-tier Bottleneck** (severely constrained)
- 🔴 1–2 → **B-tier Bottleneck** (under pressure but manageable)
- No 🔴 → Not a bottleneck, skip

### 3.2 Bottleneck Map Output

```
Supply Chain Bottleneck Map — {Trend Name}
Updated: YYYY-MM-DD

S-tier Bottlenecks (Single Points of Failure):
  1. [Segment Name] — [One-sentence reason] — Suppliers: [Company list]
  2.

A-tier Bottlenecks (Severely Constrained):
  1.
  2.

B-tier Bottlenecks (Under Pressure):
  1.
  2.

Recent Changes (vs. previous scan):
  - [New / Upgraded / Downgraded / Resolved] [Segment Name] — [Reason]
```

---

## Step 4: Company Screening — From Bottleneck to Investment Target

### 4.1 For Each S-tier and A-tier Bottleneck, Identify All Relevant Listed Companies

Search methods:
- WebSearch "{bottleneck segment} supplier listed company"
- WebSearch "{bottleneck segment} manufacturer stock"
- WebSearch "{bottleneck product} market share company"

### 4.2 Initial Screening Criteria (Quick Filter)

| Criterion | Requirement | Rationale |
|-----------|-------------|-----------|
| Listing status | Already listed (B3 / US / Europe / Japan / Taiwan) | Tradable |
| Bottleneck revenue exposure | >30% of revenue from the bottleneck segment | Purity |
| Market cap | Prefer <$10B | Large caps already fully priced |
| Liquidity | Average daily trading volume >$1M | Can enter and exit |

### 4.2.1 Valuation Check (Mandatory — Cannot Be Skipped)

**A real bottleneck does not equal an investment opportunity.** PS and PE must be calculated for every company and labeled in the report. Use the following combination of conditions to assess whether valuation is stretched:

#### Valuation Red Light (Any one condition → Signal strength capped at ★★, labeled "⚠️ Valuation Stretched")

1. **Market cap > 20% of TAM**: The company's market cap already exceeds 20% of its total addressable market, meaning growth expectations are already over-internalized.
2. **PS > 30x and revenue growth < 100%**: High valuation without sufficient growth to support it. Companies with growth >100% may be exempt from the PS red line, but must still be labeled "⚠️ High valuation requires sustained high growth for validation."
3. **Market cap > 10x the five-year optimistic revenue forecast**: Even if every optimistic assumption materializes, the current price is still too high.
4. **Stock price doubled within 60 days of a secondary offering**: Clear signs of sentiment-driven action; signal strength reduced by one grade.

#### Valuation Yellow Light (Requires additional explanation, otherwise downgraded)

1. **Unprofitable + PS > 15x**: May enter ★★★ but must explain the path to profitability and timeline.
2. **PS is >5x that of profitable peers**: Must explain the premium source (market share, growth differential, moat differential).
3. **PE > 80x**: Must calculate PEG and explain whether growth supports it.

#### Valuation Green Light (Positive factors)

- PS < 10x and revenue is growing → Signal strength may be raised by one grade.
- PE < 30x and there is an economic moat → Label "Valuation has margin of safety."

#### Valuation Sanity Check (Mandatory)

For each target, answer: "If bought at today's market cap, assuming the most optimistic scenario fully plays out, and exited at 25x PE in 10 years, what is the annualized return?" If annualized return < 10% → label "Current price lacks margin of safety."

**Note**: The purpose of the valuation check is to prevent recommending obviously flawed cases such as "a loss-making company at PS 100x" — not to exclude all high-valuation early-stage companies. The key question is whether growth rate, TAM, and competitive landscape can support the current valuation. This requires case-by-case analysis, not a blanket rule.

### 4.3 Deep Screening Dimensions

For companies passing the initial screen, evaluate each one:

```
## {Company Name} ({Ticker})

**Bottleneck Positioning**:
- Specific position in the supply chain
- Market share: Globally #X, XX% share
- Customer list (known)

**Capacity and Expansion**:
- Current capacity / utilization rate
- Expansion plans / timeline
- Capital required for expansion vs. cash on hand

**Financial Snapshot**:
- Market cap / revenue / net income / growth rate
- Bottleneck segment revenue as % of total
- Gross margin trend (the tighter the bottleneck, the higher margins should be)

**Risk Checklist**:
- [ ] Substitute technology risk: Can it be bypassed?
- [ ] Dilution risk: Any large secondary offerings / convertible bonds?
- [ ] Geopolitical risk: Is it in a sensitive region / subject to export controls?
- [ ] Management risk: Any adverse track record?
- [ ] Customer concentration risk: Overly dependent on a single customer?
- [ ] Valuation stretch: Does current valuation already reflect 3 years of growth?

**Bottleneck Durability Assessment**:
- When will this bottleneck be resolved?
- What does this company have left after resolution?
- Is this a one-time event or persistent?
```

---

## Step 5: Cross-Validation — Don't Rely on a Single Narrative

### 5.1 Positive Validation

| Validation Item | Question | Search Method |
|-----------------|----------|---------------|
| Customer validation | Have top customers signed contracts / adopted the product? | Search company announcements, mentions in customer earnings reports |
| Revenue validation | Is the bottleneck already reflected in revenue growth? | Search the last 2–3 quarters of earnings reports |
| Pricing validation | Is the product experiencing price increases? | Search industry pricing data, analyst reports |
| Capacity validation | Is capacity truly tight? | Search lead time data, customer complaints |
| Capital validation | Is there expansion-related CapEx? | Search company capex guidance |

### 5.2 Reverse Validation (Munger-Style Inversion)

| Reverse Question | Significance |
|------------------|--------------|
| Why would a smart investor NOT buy this stock? | Find known bearish arguments |
| Can this bottleneck be bypassed? Is there an alternative technology path? | Technology substitution risk |
| Can China / other players quickly replicate capacity? | Supply shock risk |
| If end demand slows 50%, what happens to this company? | Downside sensitivity |
| Has management historically diluted shareholders at peaks? | Management trustworthiness |
| What growth assumption is embedded in the current valuation? | Valuation reasonableness |

### 5.3 Signal Cross-Validation

- Are multiple companies in the same bottleneck all rising? (Industry validation)
- Are downstream customers mentioning supply tightness in their earnings reports? (Customer validation)
- Do industry associations / research institutions have relevant data? (Third-party validation)

---

## Step 6: Output — Bottleneck Opportunity Dashboard

### 6.1 Bottleneck Opportunity Ranking Table

| Rank | Company | Ticker | Market Cap | Annual Revenue | PS | PE | Bottleneck Segment | Bottleneck Rating | Market Share | Revenue Growth | Signal Strength | Valuation Assessment |
|------|---------|--------|------------|----------------|----|----|-------------------|-------------------|--------------|----------------|-----------------|----------------------|
| 1 | | | | | x | x | | S/A | | | ★1–5 | Reasonable / Elevated / Stretched |

**Required Fields**: Market cap, annual revenue, PS, and PE are mandatory — cannot be skipped with "to be confirmed." If financial data is unavailable, signal strength must not exceed ★★.

Signal Strength Rating (valuation check result directly affects the rating):
- ★★★★★ Multiple cross-validations, customer adoption confirmed, revenue reflected, valuation green light (reasonable PS + profitable or near profitable)
- ★★★★ Majority of validations passed, valuation green or yellow light (with explanation attached)
- ★★★ Logic holds but some items pending validation, valuation yellow light acceptable (e.g., high-growth early-stage company)
- ★★ Early-stage signal, or bottleneck logic holds but valuation red light (market cap > 20% TAM, PS > 30x with insufficient growth, market cap far exceeds 5-year forecast, etc.)
- ★ Pure concept, unvalidated

### 6.2 One-Page Summary for Each Opportunity

```
🎯 {Company Name} ({Ticker}) — {One-sentence bottleneck positioning}

Why it's a bottleneck:
(2–3 sentences explaining why this segment is the chokepoint)

Why this company:
(2–3 sentences explaining why this company rather than others)

Catalyst Timeline:
- Near-term (1–3 months): [Specific events, e.g., earnings, capacity ramp, customer qualification]
- Medium-term (3–12 months): [Industry trend, expansion milestones]

Key Risks:
1.
2.

Key Data: Market cap $XX / Annual revenue $XX / PS Xx / PE Xx / Revenue growth XX% / Bottleneck segment revenue XX%

Valuation Margin of Safety Check: Bought at today's market cap, exited at 25x PE in 10 years — net income must reach $XX, implying annual revenue of $XX (X times today's figure), annualized return XX%. Conclusion: Has / Does not have margin of safety.

Cross-Validation Status: ✅ Customer validated / ✅ Revenue validated / ✅ Valuation reasonable / ⚠️ Valuation stretched / ❌ Items not validated

Conclusion: Worth deep research / Add to watchlist / Not tracking for now
```

### 6.3 Action Recommendations

| Target | Recommended Action | Rationale |
|--------|--------------------|-----------|
| A | Run `/investment-team` for deep research | S-tier bottleneck + multiple validations |
| B | Add to watchlist, wait for next quarterly earnings | Logic holds but revenue not yet reflected |
| C | Not tracking for now | Substitute technology risk too high |

---

## Step 7: Incremental Updates — Dynamic Maintenance of the Bottleneck Map

### 7.1 Incremental Updates on Each Run

1. Check whether previously identified bottlenecks still hold
   - Have any new suppliers entered?
   - Has capacity expanded enough to resolve the bottleneck?
   - Has there been a breakthrough in substitute technology?

2. Scan for newly emerging bottlenecks
   - Search supply chain / shortage / bottleneck news from the past 7 days
   - Check supply chain-related disclosures during earnings season

3. Update bottleneck ratings (upgraded / downgraded / resolved)

### 7.2 Status Files

Maintain in the `reports/bottleneck-map/` directory:
- `master-map.md` — Master bottleneck map (continuously updated)
- `watchlist.md` — Watchlist (continuously updated)
- `YYYY-MM-DD/` — One folder per day containing all scan reports for that day
- `deep-dive/` — Individual files for companies under deep analysis

---

## Hourly Scan Mode (For Scheduled Tasks)

Run once per hour using a "report only when there's something worth reporting" approach:

### Scan Workflow (Every Hour)

1. **News scan**: Search supply chain-related news from the past 1–2 hours
   - Keywords: supply chain bottleneck, shortage, capacity constraint, allocation, lead time, sole source, bottleneck, out of stock, capacity, price increase
   - Coverage: English + Portuguese sources
2. **Market signals**: Check price movements of tracked companies (pay special attention to abnormal moves >5%)
3. **Earnings / announcements**: Check whether any bottleneck-related companies have released earnings or major announcements
4. **Valuation opportunities**: Check whether watchlist companies have entered buy zones due to broad market declines or other reasons
5. **Determine whether to generate a report**:
   - New bottleneck signal, clear target opportunity, or major status change → **Generate report**
   - No new findings → **Do not generate report**; log only "No new signals this round"

### Report Output Rules

**One folder per day**: `reports/bottleneck-map/YYYY-MM-DD/`

**File naming rules** (tell at a glance whether there are targets):

| Situation | File Name Format | Example |
|-----------|-----------------|---------|
| Clear target(s) found | `HH-MM-ticker1-ticker2.md` | `09-00-FORM-IBDN.md` |
| Bottleneck signal but no clear target | `HH-MM-signal-scan.md` | `14-00-signal-scan.md` |
| No new findings | No file generated | — |

**Tickers in the file name = companies that have passed the valuation check and are worth deep research.** Companies that appear only in the signal scan stage but fail valuation are not included in the file name.

### Report Template (When Targets Are Found)

```markdown
# Bottleneck Hunter — YYYY-MM-DD HH:MM

## Clear Targets

### {Company Name} ({Ticker}) — {One-sentence bottleneck positioning}

**Why it deserves attention now**: (Specific event / data change that triggered this alert)

**Bottleneck Positioning**: Layer X, {Segment Name}, Bottleneck Rating S/A/B
**Financial Snapshot**: Market cap $XX / Annual revenue $XX / PS Xx / PE Xx / Revenue growth XX%
**Valuation Check**: Red / Yellow / Green light (specific explanation)
**Valuation Margin of Safety**: 10-year 25x PE exit method, annualized return XX%

**Bull Case** (2–3 points):
1.
2.

**Bear Case** (2–3 points):
1.
2.

**Recommendation**: Execute deep research / Add to watchlist / Wait for better price

---

## Other Signals (No Clear Targets)

| Segment | Signal | Source | Preliminary Assessment |
|---------|--------|--------|------------------------|

## Watchlist Status Changes

(Upgraded / Downgraded / Added / Removed — write "No changes" if unchanged)
```

### Report Template (Signal Scan Only)

```markdown
# Bottleneck Hunter Signal Scan — YYYY-MM-DD HH:MM

## New Signals

| Segment | Signal Description | Source | Investable Target Available | Next Step |
|---------|--------------------|--------|-----------------------------|-----------|

## Watchlist Status

No changes / Changes (list them)
```

---

## AI Research Bias Awareness

| Bias | Manifestation | Countermeasure |
|------|---------------|----------------|
| Large-cap preference | Search results dominated by large-cap companies | Deliberately search small-cap suppliers; add "small cap" keyword |
| Portuguese-language bias | Missing Brazilian and Latin American companies | Must search suppliers on B3 and in Brazilian trade press (Valor Econômico, InfoMoney, Broadcast) |
| Narrative bias | Attracted by "AI concept" labels | Look only at actual supply chain position, ignore market labels |
| Confirmation bias | Only seeking positive evidence after finding a bottleneck | Enforce reverse validation (Step 5) |
| Recency bias | Relying on outdated information | Prioritize data from the past 30 days |

---

## Core Principles (Highest Priority)

1. **Don't ask AI to recommend stocks — ask AI to decompose the supply chain** — the question matters more than the answer
2. **Physical first** — focus only on segments that require actual physical products / materials / equipment
3. **Second and third layers** — don't chase leaders that are already fully priced in
4. **Cross-validation** — every conclusion requires at least 2 independent sources
5. **Be honest about uncertainty** — if data cannot be found, write "insufficient data"; do not fill gaps with speculation
6. **Bottlenecks have expiration dates** — every bottleneck eventually gets resolved; the key is assessing the time window
7. **Small cap ≠ good opportunity** — small-cap companies can still be poor businesses; must clear the financial quality bar
8. **Real bottleneck ≠ investment opportunity** — a company may sit atop the tightest bottleneck, but if PS > 30x or it is still unprofitable, the current price is not a buy. **Valuation is a hard threshold that cannot be overridden by bottleneck purity, signal strength, or narrative appeal.** It is better to miss a bottleneck stock that has already run than to buy a loss-making company at PS 100x.
9. **Follow the CLAUDE.md objectivity principles** — do not preset a bullish stance; present data first, then draw conclusions

---

## Output Requirements

1. **Report locations**:
   - Full scan: `reports/bottleneck-map/{trend-name}-bottleneck-{YYYYMMDD}.md`
   - Daily scan: `reports/bottleneck-map/daily/{YYYY-MM-DD}-{am/pm}.md`
   - Master bottleneck map: `reports/bottleneck-map/master-map.md`
   - Watchlist: `reports/bottleneck-map/watchlist.md`
2. **Language**: English
3. **Style**: Direct, sharp, no filler
4. **Data**: All data labeled with sources; estimated values labeled "estimated"
5. **No predetermined stance**: Present data first → reason through logic → draw conclusions
6. **Present both sides**: Every core judgment includes a counter-argument
