---
name: bottleneck-hunter
description: "AI Berkshire skill: Supply Chain Bottleneck Hunter: AI-driven global supply chain bottleneck arbitrage. Source: skills/bottleneck-hunter.md."
---

## Codex adapter note

This skill is generated from `skills/bottleneck-hunter.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Supply Chain Bottleneck Hunter: AI-Driven Global Supply Chain Bottleneck Arbitrage

Execute a supply chain bottleneck scan and arbitrage opportunity discovery for the $ARGUMENTS mega-trend.

## Core Philosophy

Don't ask "what stocks does AI recommend?" Ask "if this trend keeps expanding, which link will run out first?"

Traditional investment research chases category leaders and well-known sectors. This system inverts that: **starting from the physical chokepoints of the supply chain, find the companies that nobody is watching — companies where a shortage would halt the entire industry.**

Source of alpha: first-layer bottlenecks (GPU, HBM, power) are already fully priced in. The real alpha is in **the second and third layers** — optical modules, lasers, InP substrates, SOI wafers, epitaxy equipment, wafer-level testing, IC substrates, specialty glass fiber, and more.

---

## Step 1: Mega-Trend Confirmation

### 1.1 Trend Screening Criteria

Do not chase illusions in minor themes. Only pursue mega-trends that meet all of the following conditions:

| Criterion | Requirement | Verification Method |
|-----------|-------------|---------------------|
| Durability | At least 3–5 years of certain growth | Search industry forecasts, capex plans |
| Physicality | Requires actual hardware/materials/equipment buildout | Distinguish "software upgrade" from "physical expansion" |
| Scale | Global capex > $50B/year | Search top player capex guidance |
| Acceleration | Demand growth rate > supply expansion rate | Compare demand growth vs. capacity expansion plans |

### 1.2 Current Mega-Trend Tracking List

Update on each run; initial list:

1. **AI Infrastructure Buildout** — data centers, GPU clusters, network interconnects, power
2. **Energy Transition** — nuclear restart, grid upgrades, energy storage
3. **Defense Modernization** — Western defense spending up-cycle, supply chain restructuring
4. **Semiconductor Re-industrialization** — US/EU/Japan subsidized fab construction, equipment/materials bottlenecks
5. **Space Economy** — satellite internet, rapidly increasing launch cadence

If the user specifies a particular trend (e.g., "AI infrastructure"), focus only on that trend.

### 1.3 Trend Validation Output

```
Trend Name:
Core Driver: (one sentence)
Validation Events That Have Already Occurred (at least 3):
  1. [Date] [Event] [Source]
  2.
  3.
Capex Scale: Globally approx. $XX B/year, growth rate YY%
Supply-Demand Gap Assessment: Demand growth > supply expansion rate? Yes / No / Uncertain
Trend Confirmed: ✅ Trackable / ❌ Insufficient evidence, not tracking yet
```

---

## Step 2: Physical Supply Chain Decomposition

### 2.1 Layered Decomposition Framework

**Don't stop at the conceptual level — decompose down to physical entities.**

```
Layer 0 (End Product):  Final product/service
    │
Layer 1 (Core Components):  Core hardware already receiving full market attention
    │                        ⬆ Fully priced, limited alpha
    │─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
    │                        ⬇ Low attention, alpha concentration zone
    │
Layer 2 (Sub-components/Materials):  Parts and materials supporting core components
    │
Layer 3 (Upstream Equipment/Raw Materials):  Equipment and raw materials to manufacture sub-components
    │
Layer 4 (Infrastructure):  Power, cooling, land, talent, certifications
```

### 2.2 Decomposition Template Using AI Infrastructure as Example

```
Layer 0: AI model training/inference services
Layer 1: GPU/accelerators, HBM memory, servers, data centers
Layer 2 (Primary Scan Zone):
  ├─ Network Interconnects: optical modules, fiber, switch chips, copper cable
  ├─ Optical Communications Core: lasers (EML/VCSEL/CW), modulators, photodetectors
  ├─ Semiconductor Materials: InP substrates, GaAs substrates, SOI wafers, SiC substrates
  ├─ Advanced Packaging: CoWoS substrates, HBM TSV, ABF substrate film
  ├─ PCB/Substrates: high-frequency high-speed PCB, IC substrates, specialty glass fiber cloth
  ├─ Testing: wafer-level testing (Probe Card), burn-in testing, ATE
  ├─ Thermal/Cooling: liquid cooling systems, CDU, immersion cooling fluid
  └─ Power Connectivity: bus ducts, UPS, power distribution cabinets, transformers
Layer 3:
  ├─ Epitaxy Equipment: MOCVD, MBE
  ├─ Lithography/Etch: specialty-wavelength lithography, InP etching
  ├─ Raw Materials: high-purity metals (indium, gallium, germanium), specialty gases, sputtering targets
  └─ Certifications/Standards: MSA standards, Telcordia certification
Layer 4:
  ├─ Power: nuclear, natural gas generation, transmission and distribution
  ├─ Cooling water/thermal infrastructure
  └─ Data center land/permits
```

### 2.3 Decomposition for Other Trends

Execute a similar decomposition for each confirmed mega-trend. Use WebSearch to search:
- "{trend} supply chain bottleneck 2026"
- "{trend} shortage critical component"
- "{trend} capacity constraint"
- "{trend} sole source supplier"

---

## Step 3: Bottleneck Identification — Finding the "Chokepoints"

### 3.1 Six Bottleneck Criteria

For each node in Layers 2–3, evaluate each criterion:

| # | Criterion | Question | Score |
|---|-----------|----------|-------|
| 1 | **Supply Concentration** | ≤3 global suppliers? | 🔴 ≤2 / 🟡 3–5 / 🟢 >5 |
| 2 | **Expansion Lead Time** | How long to add new capacity? | 🔴 >2 years / 🟡 1–2 years / 🟢 <1 year |
| 3 | **Substitution Difficulty** | Can it be replaced by another technology/material? | 🔴 Irreplaceable / 🟡 Partially substitutable / 🟢 Easily substituted |
| 4 | **Capacity Utilization** | Current utilization rate? | 🔴 >90% / 🟡 70–90% / 🟢 <70% |
| 5 | **Demand Growth Rate** | Downstream demand growth? | 🔴 >50%/year / 🟡 20–50% / 🟢 <20% |
| 6 | **Customer Qualification Lead Time** | How long for a new supplier to qualify? | 🔴 >1 year / 🟡 6–12 months / 🟢 <6 months |

**Bottleneck Rating**:
- 🔴🔴🔴 ≥4 red flags → **S-grade Bottleneck** (single-point-of-failure level, highest priority)
- 🔴🔴 3 red flags → **A-grade Bottleneck** (severely constrained)
- 🔴 1–2 red flags → **B-grade Bottleneck** (under pressure but manageable)
- No 🔴 → Not a bottleneck, skip

### 3.2 Bottleneck Map Output

```
Supply Chain Bottleneck Map — {Trend Name}
Updated: YYYY-MM-DD

S-grade Bottlenecks (Single Point of Failure):
  1. [Node Name] — [One-line reason] — Suppliers: [Company List]
  2.

A-grade Bottlenecks (Severely Constrained):
  1.
  2.

B-grade Bottlenecks (Under Pressure):
  1.
  2.

Recent Changes (vs. last scan):
  - [New / Upgraded / Downgraded / Resolved] [Node Name] — [Reason]
```

---

## Step 4: Company Screening — From Bottleneck to Investment Target

### 4.1 For Each S-grade and A-grade Bottleneck, Identify All Related Listed Companies

Search methods:
- WebSearch "{bottleneck node} supplier listed company"
- WebSearch "{bottleneck node} manufacturer stock"
- WebSearch "{bottleneck product} market share company"

### 4.2 Initial Screening Criteria (Quick Filter)

| Criterion | Requirement | Rationale |
|-----------|-------------|-----------|
| Listing Status | Already listed (A-share / HK / US / Japan / Taiwan / Europe) | Tradeable |
| Bottleneck Revenue Share | >30% of revenue from the bottleneck node | Purity of exposure |
| Market Cap | Prefer <$10B | Large market caps are already fully priced |
| Liquidity | Average daily volume >$1M | Can enter and exit |

### 4.2.1 Valuation Check (Must Execute — Cannot Skip)

**A real bottleneck ≠ an investment opportunity.** Calculate PS and PE for each company and include them in the report. Use the following combined conditions to judge whether valuation is stretched:

#### Valuation Red Light (Any one condition → signal strength capped at ★★, mark "⚠️ Valuation Overstretched")

1. **Market cap > 20% of TAM**: The company's market cap already exceeds 20% of its total addressable market, meaning growth expectations are already overly internalized
2. **PS > 30x and revenue growth < 100%**: High valuation but insufficient growth to support it. Companies with growth >100% may be exempt from the PS red line, but must still be marked "⚠️ High valuation requires sustained high growth for verification"
3. **Market cap > 10x 5-year optimistic revenue forecast**: Even if all optimistic assumptions are met, current pricing is still excessive
4. **Share price doubled within 60 days of equity issuance**: Clear sentiment-driven characteristic; lower signal strength by one grade

#### Valuation Yellow Light (Requires additional explanation, otherwise downgraded)

1. **Unprofitable + PS > 15x**: May enter ★★★ but must explain path to profitability and timeline
2. **PS is 5x+ that of profitable peers**: Must explain the source of the premium (market share, growth differential, moat differential)
3. **PE > 80x**: Must calculate PEG and explain whether the growth rate supports it

#### Valuation Green Light (Bonus Points)

- PS < 10x and revenue is growing → signal strength may increase by one grade
- PE < 30x and company has a moat → mark "Valuation has margin of safety"

#### Valuation Reasonableness Test (Required)

For each target, answer: "Buying at the current market cap, assuming all optimistic scenarios are realized, and exiting in 10 years at 25x PE — what is the annualized return?" If annualized return < 10% → mark "Current price lacks margin of safety."

**Note**: The purpose of the valuation check is to prevent recommending "a loss-making company at 100x PS" — an obvious mistake — not to exclude all high-valuation early-stage companies. The key question is whether growth rate, TAM, and competitive landscape can support the current valuation; this requires specific analysis rather than blanket exclusion.

### 4.3 Deep Screening Dimensions

For each company that passes initial screening, evaluate individually:

```
## {Company Name} ({Ticker})

**Bottleneck Positioning**:
- Specific position in the supply chain
- Market share: #X globally, XX% share
- Known customer list

**Capacity & Expansion**:
- Current capacity / utilization
- Expansion plan / timeline
- Capital required for expansion vs. existing cash

**Financial Snapshot**:
- Market cap / revenue / net income / growth rate
- Bottleneck business as % of revenue
- Gross margin trend (tighter bottleneck should drive gross margin higher)

**Risk Checklist**:
- [ ] Substitution technology risk: Can it be bypassed?
- [ ] Dilution risk: Significant equity issuance / convertibles?
- [ ] Geopolitical risk: Located in sensitive region / subject to export controls?
- [ ] Management risk: Any negative track record?
- [ ] Customer concentration risk: Excessively dependent on one customer?
- [ ] Valuation overstretched: Does current valuation already reflect 3 years of growth?

**Bottleneck Sustainability Assessment**:
- When will this bottleneck be resolved?
- What does this company have after the bottleneck is resolved?
- Is it a one-time event or sustained?
```

---

## Step 5: Cross-Validation — Don't Just Hear One Story

### 5.1 Positive Validation

| Validation Item | Question | Search Method |
|-----------------|----------|---------------|
| Customer Validation | Have top customers signed / begun qualification? | Search company announcements, customer earnings call mentions |
| Revenue Validation | Is the bottleneck already reflected in revenue growth? | Search last 2–3 quarters of earnings |
| Price Validation | Are product prices rising? | Search industry quotes, analyst reports |
| Capacity Validation | Is capacity actually tight? | Search lead time data, customer complaints |
| Capex Validation | Is there expansion capex? | Search company capex guidance |

### 5.2 Reverse Validation (Munger-style Inversion)

| Reverse Question | Significance |
|-----------------|--------------|
| Why won't smart investors buy this stock? | Find known bearish arguments |
| Can this bottleneck be bypassed? Are there alternative routes? | Technology substitution risk |
| Can China / other players quickly replicate capacity? | Supply shock risk |
| If end demand slows 50%, what happens to this company? | Downside sensitivity |
| Has management previously diluted shareholders at peak prices? | Management trustworthiness |
| What growth assumptions are implied by the current valuation? | Valuation reasonableness |

### 5.3 Signal Cross-Validation

- Are multiple companies in the same bottleneck all rising? (industry validation)
- Is the downstream customer mentioning supply tightness in earnings calls? (customer validation)
- Does an industry association / research institution have relevant data? (third-party validation)

---

## Step 6: Output — Bottleneck Opportunity Dashboard

### 6.1 Bottleneck Opportunity Rankings Table

| Rank | Company | Ticker | Market Cap | Annual Revenue | PS | PE | Bottleneck Node | Bottleneck Grade | Market Share | Revenue Growth | Signal Strength | Valuation Judgment |
|------|---------|--------|------------|---------------|-----|-----|----------------|-----------------|-------------|---------------|----------------|-------------------|
| 1 | | | | | x | x | | S/A | | | ★1–5 | Reasonable / High / Overstretched |

**Required Fields**: Market cap, annual revenue, PS, PE are required — cannot be skipped with "to be verified." If financial data cannot be obtained, signal strength may not exceed ★★.

Signal Strength Rating (valuation check directly affects the rating):
- ★★★★★ Multiple cross-validations, customer qualified, revenue already reflected, valuation green light (reasonable PS + profitable or near profitable)
- ★★★★ Most validations passed, valuation green or yellow light (explanation required)
- ★★★ Logic holds but some items pending verification, valuation yellow light acceptable (e.g., high-growth early-stage company)
- ★★ Early signal, or bottleneck logic holds but valuation red light (market cap > 20% of TAM, PS > 30x with insufficient growth, market cap far exceeds 5-year forecast, etc.)
- ★ Pure concept, unverified

### 6.2 One-Page Summary for Each Opportunity

```
🎯 {Company Name} ({Ticker}) — {One-line bottleneck positioning}

Why It's a Bottleneck:
(2–3 sentences explaining why this node is a chokepoint)

Why This Company:
(2–3 sentences explaining why this company rather than others)

Catalyst Timeline:
- Near-term (1–3 months): [Specific event, e.g., earnings, capacity ramp, customer qualification]
- Medium-term (3–12 months): [Industry trend, expansion milestones]

Key Risks:
1.
2.

Key Data: Market cap $XX / Annual revenue $XX / PS Xx / PE Xx / Revenue growth XX% / Bottleneck business share XX%

Valuation Margin of Safety Test: Buying at current market cap, exiting in 10 years at 25x PE, requires net income of $XX, implying annual revenue of $XX (X times today's figure), for an annualized return of XX%. Conclusion: Margin of safety exists / does not exist.

Cross-Validation Status: ✅ Customer validated / ✅ Revenue validated / ✅ Valuation reasonable / ⚠️ Valuation overstretched / ❌ Unverified items

Conclusion: Worth deeper research / Add to watchlist / Not tracking for now
```

### 6.3 Action Recommendations

| Target | Recommended Action | Rationale |
|--------|--------------------|-----------|
| A | Run `/investment-team` for deep research | S-grade bottleneck + multiple validations |
| B | Add to watchlist, wait for next quarterly earnings | Logic holds but revenue not yet reflected |
| C | Not tracking for now | Substitution technology risk too high |

---

## Step 7: Inventory Update — Dynamic Maintenance of the Bottleneck Map

### 7.1 Incremental Updates on Each Run

1. Check whether previously identified bottlenecks still hold
   - Have new suppliers entered?
   - Has capacity expanded enough to resolve the bottleneck?
   - Have alternative technologies seen a breakthrough?

2. Scan for newly emerged bottlenecks
   - Search supply chain / shortage / bottleneck news from the past 7 days
   - Check supply-chain-related disclosures from the current earnings season

3. Update bottleneck ratings (upgrade / downgrade / resolved)

### 7.2 Status Files

Maintain in the `reports/bottleneck-map/` directory:
- `master-map.md` — Master bottleneck map (continuously updated)
- `watchlist.md` — Watchlist (continuously updated)
- `YYYY-MM-DD/` — One folder per day, containing all scan reports for that day
- `deep-dive/` — Separate files for companies receiving in-depth analysis

---

## Hourly Scan Mode (For Scheduled Tasks)

Run once per hour using a "report only when there's something to report" approach:

### Scan Workflow (Hourly)

1. **News Scan**: Search supply-chain-related news from the past 1–2 hours
   - Keywords: supply chain bottleneck, shortage, capacity constraint, allocation, lead time, sole source, bottleneck, out of stock, capacity, price increase
   - Coverage: English + Chinese sources
2. **Market Signals**: Check price movements of tracked companies (pay particular attention to abnormal moves >5%)
3. **Earnings/Announcements**: Check whether any bottleneck-related companies have released earnings or major announcements
4. **Valuation Opportunities**: Check whether companies on the watchlist have entered a buy range due to broad market declines or other reasons
5. **Determine Whether to Publish a Report**:
   - New bottleneck signal, clear investable target, major status change → **publish report**
   - No new findings → **no report**; log "No new signals this round" only

### Report Output Rules

**One folder per day**: `reports/bottleneck-map/YYYY-MM-DD/`

**File naming convention** (the filename should make it clear at a glance whether there are actionable targets):

| Situation | Filename Format | Example |
|-----------|-----------------|---------|
| Clear target found | `HH-MM-Ticker1-Ticker2.md` | `09-00-FORM-IBDN.md` |
| Bottleneck signal but no clear target | `HH-MM-signal-scan.md` | `14-00-signal-scan.md` |
| No new findings | No file generated | — |

**Tickers in the filename = companies that passed the valuation check and are worth deeper research.** Companies that appeared only in the signal scan phase but failed valuation are not included in the filename.

### Report Template (When a Target Is Found)

```markdown
# Bottleneck Hunter — YYYY-MM-DD HH:MM

## Clear Targets

### {Company Name} ({Ticker}) — {One-line bottleneck positioning}

**Why It Warrants Attention Now**: (Specific event/data change that triggered this alert)

**Bottleneck Positioning**: Layer X, {node name}, bottleneck grade S/A/B
**Financial Snapshot**: Market cap $XX / Annual revenue $XX / PS Xx / PE Xx / Revenue growth XX%
**Valuation Check**: Red / Yellow / Green light (specific explanation)
**Valuation Margin of Safety**: 10-year 25x PE exit method, annualized return XX%

**Bull Case** (2–3 points):
1.
2.

**Bear Case** (2–3 points):
1.
2.

**Recommendation**: Proceed with deep research / Add to watchlist / Wait for better price

---

## Other Signals (No Clear Target)

| Node | Signal | Source | Preliminary Assessment |
|------|--------|--------|----------------------|

## Watchlist Status Changes

(Upgraded / downgraded / added / removed; if no changes write "No changes")
```

### Report Template (Signal Scan Only)

```markdown
# Bottleneck Hunter Signal Scan — YYYY-MM-DD HH:MM

## New Signals

| Node | Signal Description | Source | Investable Target? | Next Step |
|------|--------------------|--------|--------------------|-----------|

## Watchlist Status

No changes / Changes (list them)
```

---

## AI Research Bias Awareness

| Bias | Manifestation | Countermeasure |
|------|---------------|----------------|
| Large-cap preference | Search results dominated by large-cap companies | Deliberately search for small-cap suppliers; add "small cap" keyword |
| English-language preference | Missing Japanese, Korean, Taiwanese companies | Must search suppliers in Japan / Korea / Taiwan markets |
| Narrative preference | Attracted by "AI concept" labels | Look only at actual supply chain position, not market labels |
| Confirmation bias | After finding a bottleneck, only seek supporting evidence | Enforce reverse validation (Step 5) |
| Recency bias | Relying on outdated information | Prioritize data from the past 30 days |

---

## Core Principles (Highest Priority)

1. **Don't ask AI to recommend stocks — ask AI to decompose the supply chain** — the question matters more than the answer
2. **Physical first** — focus only on nodes requiring actual physical products/materials/equipment
3. **Second and third layers** — don't chase leaders that are already fully priced
4. **Cross-validate** — every conclusion requires at least 2 independent sources
5. **Be honest about uncertainty** — if data is unavailable, write "insufficient data"; don't fill uncertainty with speculation
6. **Bottlenecks have an expiry date** — every bottleneck will eventually be resolved; the key is judging the time window
7. **Small market cap ≠ good opportunity** — small caps can also be poor businesses; must pass the financial quality test
8. **Real bottleneck ≠ investment opportunity** — a company can sit atop the tightest bottleneck, but if PS > 30x or it is still unprofitable, the current price is not a buy. **Valuation is a hard threshold; it cannot be overridden by bottleneck purity, signal strength, or narrative appeal.** Better to miss a bottleneck stock that has already run than to buy a loss-making company at 100x PS
9. **Follow CLAUDE.md objectivity principles** — do not preset a bullish stance; present data first, then draw conclusions

---

## Output Requirements

1. **Report Locations**:
   - Full scan: `reports/bottleneck-map/{trend-name}-bottleneck-{YYYYMMDD}.md`
   - Daily scan: `reports/bottleneck-map/daily/{YYYY-MM-DD}-{am/pm}.md`
   - Master bottleneck map: `reports/bottleneck-map/master-map.md`
   - Watchlist: `reports/bottleneck-map/watchlist.md`
2. **Language**: English
3. **Style**: Direct, sharp, no filler
4. **Data**: All data must cite sources; estimated values labeled "estimated"
5. **No predetermined stance**: Present data → reason through logic → draw conclusions
6. **Both sides**: Every core judgment must include a counter-argument
