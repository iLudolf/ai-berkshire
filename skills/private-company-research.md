# Private Company Research: Multi-Agent Parallel Deep Research Framework

Conduct a team-based deep research analysis on $ARGUMENTS. Designed specifically for private companies such as Nubank (pre-IPO stage), C6 Bank, Mercado Bitcoin, iFood, Rappi Brasil, SpaceX, Stripe, and similar firms.

**Ultimate Goal**: Under conditions of naturally scarce information, reconstruct the **true value** of this company as faithfully as possible — not the market's assigned valuation, but what the business itself is actually worth.

## Framework Characteristics

Core differences between private vs. public company research:
- **No standardized financial reports**: Must piece together information from multiple sources and cross-validate
- **Fewer valuation anchors**: Rely on funding rounds, comparable company analysis, and scenario modeling
- **High information asymmetry**: Requires more "jigsaw puzzle" style research methods
- **Uncertain exit paths**: IPO / acquisition / secondary transfer are all possibilities

## AI Research Bias Awareness (Core Premise of This Framework)

Private companies are the domain where AI research bias is most severe. Always be vigilant against the following traps:

**Core contradiction**: AI excels at structuring existing information, but private company information is naturally scarce. This leads to:
1. **False conservatism**: Because there is less material, AI tends to give conservative/vague conclusions — but less material ≠ a worse company
2. **False precision**: To fill out the report template, AI may disguise "reasonable speculation" as "evidence-based analysis"
3. **Benchmarking trap**: When forcibly comparing to public companies, one inherits public company valuation logic and ignores the unique value of the private company
4. **Survivorship bias**: Company information findable online tends to skew positive (companies proactively spread good news)

**Mitigation principles**:
- Better to leave a blank and say "unknown" than to fill a table with speculation masquerading as certainty
- Every data point must be annotated with a confidence level (🟢 High / 🟡 Medium / 🔴 Low), letting readers judge for themselves
- Distinguish "verifiable facts" from "AI reasoning" using different formatting
- For companies with extremely scarce information, switch to "first-principles mode" — don't chase a complete report, just answer a few core questions:
  1. What real problem does this business solve? Is the demand genuine or artificial?
  2. Why this team? What unique advantages do they have?
  3. If they succeed, how high is the ceiling? If they fail, where are they most likely to die?
  4. What are the key validation milestones at the current stage?

**Exploiting information asymmetry in reverse**: The market has less information on private companies → lower pricing efficiency → which may be precisely the source of excess returns. The goal of AI research is not to eliminate information asymmetry (impossible) but to extract the most critical decision-relevant signals from limited information.

---

## Execution Process

### Step 1: Present Team Framework

Show the user the following team structure and confirm before starting:

| Role | Responsibilities | Core Perspective |
|------|-----------------|-----------------|
| **team-lead** (yourself) | Coordination, information synthesis, cross-validation, final report | Investment decision integration |
| **business-decoder** | Business model decomposition & product/user analysis | "What is the essence of this business" |
| **financial-detective** | Financial data reconstruction & valuation modeling | "Reconstruct the true financial picture despite missing information" |
| **competitive-mapper** | Industry landscape & competitive dynamics & substitution threats | "Who is competing with it, who could disrupt it" |
| **risk-governance-analyst** | Risk panorama & management/governance/investor assessment | "What could go wrong, who is at the helm" |
| **tech-ip-analyst** | Tech stack / patents / R&D capability / technology moat | "Is the technology moat real, and how long can it hold" |
| **signal-miner** | Alternative data mining: hiring / patents / litigation / App data / supply chain | "Beyond standard information, what other clues can be found" |

### Step 2: Create Team

Use TeamCreate to create the team:
- team_name: `{company-name}-private-research` (lowercase English, e.g., `c6-bank-private-research`)
- agent_type: `team-lead`

### Step 3: Create 6 Tasks

Use TaskCreate to create the following 6 tasks (each must have a subject, description, and activeForm):

---

#### Task 1: Business Model & Product/User Deep Analysis
- subject: `Decompose {Company Name} business model, product matrix, and user ecosystem`
- activeForm: `Analyze {Company Name} business model and user ecosystem`
- description contains:

```
## Business Model Deep Decomposition

### 1. Core Business Definition
- Define the essence of this business in one sentence (Duan Yongping style: use the simplest language to explain this business to a smart but uninformed person)
- What problem does the company solve? Who does it create value for?
- Value proposition and differentiation from similar products
- If the company didn't exist, how would users solve this problem? How high is the cost of alternatives?
- Judgment on demand "rigidity": Would users cut this expense during an economic downturn?

### 2. Revenue Model Decomposition
- Revenue composition: advertising / commission / subscription / transaction take rate / financial services / SaaS / hardware / licensing fees, etc.
- Share of each revenue line (if data available) and growth trends
- Monetization efficiency metrics: ARPU, Take Rate, ad load rate, conversion rate, etc.
- Revenue quality assessment:
  - Recurring revenue vs. one-time revenue mix
  - Revenue concentration: top 5 customers/channels as a share
  - Revenue predictability (contract/subscription-based vs. transactional)
  - Whether revenue recognition is reasonable (any signs of early recognition)
- Benchmark monetization efficiency against publicly listed peers

### 3. Unit Economics (UE) Estimation
- CAC (Customer Acquisition Cost) estimation:
  - Share of paid acquisition vs. organic growth
  - CAC by channel (if available)
  - CAC trend: rising or falling as scale grows?
- LTV (Lifetime Value) estimation:
  - ARPU × expected customer lifetime
  - Account for cross-sell and upsell
- LTV/CAC ratio, payback period
- Marginal cost structure: trend in marginal cost per additional user/transaction
- Economies of scale inflection point: when/has the breakeven point been reached?

### 4. Product Matrix & Flywheel Effects
- Core products + extension products + incubation products
- How the flywheel operates: network effects / data flywheel / economies of scale
- Synergies and cross-traffic between products
- Product lifecycle: which stage is each product at?
- Product iteration speed: App/product update frequency, major feature updates in the last 12 months

### 5. Business Model Canvas (BMC)
Describe the business model using the following 9 elements:
| Element | Content |
|---------|---------|
| Value Proposition | |
| Customer Segments | |
| Channels | |
| Customer Relationships | |
| Revenue Streams | |
| Key Resources | |
| Key Activities | |
| Key Partners | |
| Cost Structure | |

### 6. User Deep Analysis
- User scale: MAU/DAU (estimated from Sensor Tower, SimilarWeb, data.ai, App Annie, etc.)
- User growth curve: which stage of the S-curve? (substantiate with specific data)
- User stickiness metrics:
  - DAU/MAU ratio
  - Average session duration, open frequency
  - Day-1 / Day-7 / Day-30 retention rates (if available)
  - Comparison of user growth vs. retention trends (identify false growth)
- User profile: age / geography / purchasing power / occupation distribution
- User reputation:
  - App Store / Google Play rating trends (changes over the last 12 months)
  - Social media sentiment analysis
  - Real user feedback on Reclame Aqui / Reddit Brasil / Twitter/X
  - Main areas of concentration in negative reviews
- User acquisition efficiency:
  - Ratio of paid acquisition vs. organic growth vs. word-of-mouth
  - Whether dependent on a single acquisition channel

### 7. Pricing Power Assessment
- Has there been a price increase in the past 3 years? User churn after the increase?
- Price comparison with competitors: price leader or follower?
- Assessment of user price sensitivity
- Reasonableness of commission/take rate within the industry value chain

### 8. Economic Moat Assessment
Verify and score each of the following 6 dimensions (★1-5):

| Moat Type | Rating | Evidence | Trend | Durability Assessment |
|-----------|--------|----------|-------|-----------------------|
| Network Effects | | More users = more value? Single-sided or multi-sided? | Widening / Stable / Narrowing | |
| Switching Costs | | Cost for users to migrate to a competitor? Data / relationship / habit migration costs? | | |
| Brand Mindshare | | Category = brand? NPS estimate? | | |
| Data Moat | | Has a data flywheel formed? Proprietary data assets? Data volume? | | |
| Regulatory License | | Are there barriers to entry? How hard is it to obtain a license? | | |
| Economies of Scale | | Is the cost advantage from scale significant? | | |

Overall economic moat rating: Wide / Moderate / Narrow / None

### 9. Internationalization Analysis (if applicable)
- Overseas market expansion status
- Share of international revenue
- Localization strategy and challenges
- Differences in overseas competitive landscape
```

---

#### Task 2: Financial Data Reconstruction & Valuation Modeling
- subject: `Reconstruct {Company Name} financial data and conduct valuation analysis`
- activeForm: `Reconstruct {Company Name} financial data and valuation`
- description contains:

```
## Financial Data Reconstruction (Detective-Style Research)

Private companies have no standardized financial reports. Data must be pieced together from multiple sources and cross-validated. Every data point must be traced to a specific source with date and confidence level.

### 1. Data Source Matrix
**Search the following sources in priority order**:

| Priority | Source Type | Specific Source | Credibility | Search Method |
|----------|-------------|-----------------|-------------|---------------|
| 1 | Prospectus / Regulatory Filings | CVM filings (DFP/ITR/FRE), SEC filing (if US-listed), B3 prospectus drafts | 🟢 High | Search "company name + prospecto/IPO/CVM" |
| 2 | Parent / affiliated listed company reports | E.g., data in parent's DFP/ITR filed with CVM, Google Cloud annual report | 🟢 High | Search related disclosures in parent annual reports |
| 3 | Regulatory penalties / compliance disclosures | BACEN, CVM, CADE, ANPD, ANATEL penalty documents | 🟢 High | Search "company name + multa/autuação/processo administrativo" |
| 4 | Bond / CRI / CRA / debenture issuance documents | Underlying data in debt issuance prospectuses filed with CVM | 🟢 High | Search "company name + debenture/CRI/CRA/emissão" |
| 5 | Business registration information | Receita Federal CNPJ data, Junta Comercial filings, Jusbrasil | 🟡 Medium-High | |
| 6 | Funding news | Valuation, funding amounts, investors | 🟡 Medium | Search "company name + rodada/aporte/valuation" |
| 7 | Third-party research reports | XP Investimentos, BTG Pactual Research, Itaú BBA, consulting firms, ABVCAP | 🟡 Medium | Search "company name + relatório/pesquisa" |
| 8 | Deep media coverage | The Information, Pipeline (Valor), Bloomberg Línea, Startups.com.br, Sifted | 🟡 Medium | Search these media + company name directly |
| 9 | Industry data extrapolation | Back-calculate from industry total and market share (ABECS, FEBRABAN, IBGE) | 🔴 Low-Medium | |
| 10 | Former employee / insider leaks | Glassdoor Brasil, LinkedIn, forums | 🔴 Low | For reference only, not a primary basis |

### 2. Key Financial Metric Estimation
Estimate the following data where possible. **Every data point must note**: source, date, confidence level, and estimation method.

**Revenue Side**:
- Total revenue and growth rate (last 3 years, annual/quarterly granularity)
- Revenue structure breakdown (by business line / product line)
- Revenue growth driver decomposition: volume (users/transaction volume) × price (ARPU/average order value)
- Seasonal fluctuation patterns in revenue

**Cost Side**:
- Gross margin estimation (benchmarked against listed peers, explain selection rationale)
- R&D expense ratio estimation (via headcount × average compensation, or R&D headcount share)
- Sales expense ratio estimation (via acquisition channels and advertising data)
- G&A expense ratio estimation

**Profit Side**:
- Operating profit / EBITDA estimation
- Net income / adjusted net income estimation
- Profitability timeline: when did/will it achieve profitability?

**Cash Flow Side**:
- Operating cash flow judgment (positive/negative, self-sustaining?)
- CapEx level and trend
- Free cash flow estimation
- Cash on hand / burn rate (estimated from funding amounts, funding intervals, headcount)
- Cash runway: how long at the current burn rate?

**Efficiency Metrics**:
- Headcount and per-employee productivity (revenue per employee, profit per employee)
- Capital efficiency: revenue generated per dollar of capital raised
- Benchmark efficiency metrics against listed peers

### 3. Financial Data Cross-Validation
- If the same metric has multiple sources, list all and explain discrepancies
- Use different methods to estimate the same metric and check if results converge
- Flag unverifiable "single-source" data points

| Metric | Source A (Data / Date) | Source B (Data / Date) | Discrepancy | Adopted Judgment |
|--------|------------------------|------------------------|-------------|-----------------|

### 4. Funding History & Valuation Evolution
Compile a complete funding timeline:

| Round | Date | Amount | Pre-Money Valuation | Post-Money Valuation | Lead Investor | Co-Investors | Valuation Multiple Growth | Notes |
|-------|------|--------|---------------------|----------------------|---------------|--------------|--------------------------|-------|

Analysis:
- Is the valuation growth curve healthy? (Is the multiple increase per round reasonable?)
- Is the funding interval reasonable? (Too frequent = burning fast? Too sparse = difficulty fundraising?)
- Has a down round occurred?
- Are existing shareholders continuing to invest? (Confidence signal)
- Estimated investment terms of the latest round:
  - Liquidation preference (1x / 2x / participating)
  - Anti-dilution protection (full ratchet / weighted average)
  - Earn-out clauses (performance / listing timeline)
  - Impact of these terms on common stock value

### 5. Valuation Analysis (Multi-Method Cross-Check)

**Method 1: Latest Funding Round Valuation**
- Most recent round valuation and date
- "Common stock equivalent valuation" after adjusting for liquidation preference and other terms (typically requires a 20-40% discount)
- Adjustment for time elapsed since the last round
- Analysis of this round's investor motivations (financial vs. strategic; strategic investors may pay a premium)

**Method 2: Comparable Public Company Analysis**
- Select 3-5 listed comparable companies and explain the selection rationale
- Key multiple comparison:

| Comparable Company | P/S | P/E | EV/EBITDA | EV/Revenue | Growth Rate | Profit Margin |
|--------------------|-----|-----|-----------|------------|-------------|---------------|

- Applied adjustments:
  - Liquidity discount: 20-30% (note specific value and rationale)
  - Growth premium/discount
  - Size discount
  - Regulatory/policy risk discount

**Method 3: DCF Scenario Analysis**
Three scenarios, each with key assumptions listed:

| Assumption | Bear Case | Base Case | Bull Case |
|------------|-----------|-----------|-----------|
| Revenue CAGR (next 5 years) | | | |
| Terminal operating margin | | | |
| Terminal growth rate | | | |
| WACC | | | |
| Terminal multiple (EV/EBITDA) | | | |

Every assumption must be supported by evidence — no assumption pulled from thin air.

**Method 4: Terminal Value Back-Calculation**
- Assume the market position of this business in its terminal state in 5 / 10 years
- Terminal revenue and margin assumptions
- Reasonable terminal multiple (reference mature companies in the same industry)
- Back-calculate the current reasonable valuation range
- Implied annualized return

**Method 5: Transaction Comparable Analysis**
- M&A / funding transactions in the same industry in the last 2 years
- Transaction multiples (P/S, P/E)
- Transaction context and premium/discount factors

### 6. Valuation Synthesis

| Method | Valuation Range | Confidence | Weight | Weighted Valuation |
|--------|-----------------|------------|--------|--------------------|

- Do the different methods converge? If the discrepancy is large, analyze the reason
- The final valuation range should distinguish "fair value" from "conservative value" (margin of safety valuation)
```

---

#### Task 3: Industry Landscape & Competitive Dynamics Analysis
- subject: `Analyze the competitive landscape and substitution threats in {Company Name}'s industry`
- activeForm: `Analyze {Company Name} industry landscape and competitive dynamics`
- description contains:

```
## Industry Landscape & Competitive Dynamics

### 1. Industry Positioning & Market Size
- Definition of the company's core track (note: the track the company defines for itself may be embellished — make an independent judgment)
- TAM / SAM / SOM three-tier market size:
  - TAM (Total Addressable Market): the entire macro industry
  - SAM (Serviceable Addressable Market): what the company's technology/model can cover
  - SOM (Serviceable Obtainable Market): what the company can actually capture today
- Comparison of market size data sources (different research firms' forecasts may differ greatly)
- Market penetration rate: current vs. ceiling
- Industry stage: nascent / growth / mature / decline (with supporting evidence)
- Industry growth drivers: what forces are propelling/impeding industry growth

### 2. Industry Value Chain Map
Draw the complete value chain structure (text diagram):

```
Upstream suppliers (who? bargaining power?)
    ↓
Company's position (which link in the value chain? share of profit pool?)
    ↓
Downstream customers/users (concentration? alternatives?)
    ↕
Competitors / Substitutes / Potential entrants
```

- Profit pool analysis: profit distribution across each link of the value chain
- Company's bargaining power in the value chain (upstream/downstream)
- Upstream/downstream dependency analysis: is there single-supplier or single-customer dependency?
- Structural changes occurring in the value chain

### 3. Porter's Five Forces Analysis (Quantitative Scoring)

| Force | Intensity (★1-5) | Key Factors | Impact on Company |
|-------|-----------------|-------------|-------------------|
| Industry rivalry | | Concentration, degree of differentiation, exit barriers | |
| Threat of new entrants | | Capital barriers, technology barriers, regulatory barriers, brand barriers | |
| Threat of substitutes | | Price-performance of substitutes, switching costs | |
| Supplier bargaining power | | Supplier concentration, switching costs | |
| Buyer bargaining power | | Customer concentration, information transparency | |

Overall industry attractiveness score: ★1-5

### 4. Competitive Landscape Deep Scan

| Competitor | Type | Market Share (est.) | Revenue Scale | Funding/Market Cap | Core Strengths | Key Weaknesses | Threat Level |
|------------|------|---------------------|---------------|--------------------|----------------|----------------|--------------|
| Direct competitor 1 | Direct | | | | | | |
| Direct competitor 2 | Direct | | | | | | |
| Indirect competitor 1 | Cross-sector | | | | | | |
| Potential entrant 1 | Tech giant | | | | | | |

Key analyses:
- **Direct competitors**: Same-track direct rivals — analyze each one's strategic intent and resource allocation
- **Indirect competitors**: Cross-sector potential competition, especially adjacent businesses from large tech companies
- **Substitution threat**: Different technology paths/models, especially AI-driven disruption
- **Potential entrants**: Probability and method of large-platform entry (build / acquire / invest)

### 5. Competitor Deep Comparison
Select 2-3 most direct competitors (both listed and private) for multi-dimensional comparison:

| Dimension | {Company Name} | Competitor A | Competitor B | Competitor C |
|-----------|---------------|--------------|--------------|--------------|
| Founded | | | | |
| User scale (MAU) | | | | |
| Revenue scale | | | | |
| Revenue growth | | | | |
| Total funding / Market cap | | | | |
| Valuation / Revenue multiple | | | | |
| Monetization efficiency (ARPU) | | | | |
| Gross margin | | | | |
| Profitability status | | | | |
| Headcount | | | | |
| Technology capability | | | | |
| Differentiated positioning | | | | |
| Degree of internationalization | | | | |

### 6. Competitive Dynamics & Trends
- Key changes in the competitive landscape over the past 12 months (funding, M&A, product launches, executive changes)
- Inferred strategic direction of competitors (from hiring, patents, product updates)
- Structural shifts occurring in the industry
- Impact of technology changes on the competitive landscape (especially AI/LLMs)
- Impact of regulatory policy on the competitive landscape
- Does the industry have "winner-takes-all" characteristics? Or will a stable oligopoly form?

### 7. Competitive Scenario Modeling
- Scenario A: Company wins — what conditions are needed? Probability?
- Scenario B: Balanced coexistence — each party's survival space?
- Scenario C: Disruption — the most likely disruptor and path?

### 8. Global Benchmarking
Find overseas/domestic comparable companies (already listed) and analyze:

| Dimension | Comparable A | Comparable B | Insights for {Company Name} |
|-----------|-------------|-------------|----------------------------|
| Development path | | | |
| Current valuation level | | | |
| Time from similar stage to listing | | | |
| Post-IPO stock performance | | | |
| Key success/failure factors | | | |

- Note the limitations of benchmarking (Brazilian market specifics, regulatory differences, user behavior differences, Selic/interest rate environment impact on valuations)
```

---

#### Task 4: Risk Panorama & Governance Assessment
- subject: `Assess {Company Name}'s full-spectrum risks and management/governance structure`
- activeForm: `Assess {Company Name} risks and governance structure`
- description contains:

```
## Risk Panorama & Governance Assessment

### 1. Founder/CEO Deep Assessment

> "Buying a stock is buying a person." — Duan Yongping

- **Background & track record**: education, career history, entrepreneurial experience
  - Any serial entrepreneurship? Result of the last venture?
  - Years of industry-relevant experience
  - Largest team/business previously managed
- **Strategic vision**: search for the CEO's public statements over the past 3 years (speeches, interviews, internal letters, social media)
  | Date | CEO's judgment/prediction | Actual outcome | Accuracy |
  |------|--------------------------|----------------|----------|
  - Any judgments that were ahead of the market and correct?
  - Any instances of staying calm when everyone else was bullish?
- **Execution**: were key milestones delivered on time?
  | Commitment | Commitment date | Context | Delivery | Assessment |
  |------------|----------------|---------|----------|------------|
- **Character & values**:
  - Attitude toward users/employees/society (judge from specific events, not slogans)
  - Choices made in adversity (layoff approach, crisis handling, trade-offs in conflicts of interest)
  - Short-term profit vs. long-term value trade-offs
- **Controversy**: any negative track record? (Search "CEO name + controversy/scandal/issue")
- **Rating**: ★1-5 (with detailed justification)

### 2. Core Team Assessment
- List of key executives and background (CTO / CFO / COO / VP, etc.)
  | Name | Title | Background | Tenure | Previous experience |
  |------|-------|------------|--------|---------------------|
- Key talent flow analysis:
  - Significant executive departures in the past 2 years (who left? went where? why?)
  - Significant executive arrivals in the past 2 years (poached from where? what does it signal?)
  - Net talent inflow or outflow?
- Team complementarity: does the founding team have complementary capabilities? Any obvious gaps?
- Team culture signals:
  - Glassdoor Brasil / LinkedIn rating and trend (direction of change over the last 12 months matters more than the absolute value)
  - Employee willingness to recommend (Would recommend to a friend)
  - CEO approval rating
  - Sentiment around overtime culture and organizational atmosphere
- Key person dependency: what happens if the CEO/CTO leaves?

### 3. Shareholding Structure & Governance

**Equity Structure**:
| Shareholder | Ownership % | Voting rights % | Type | Notes |
|-------------|------------|-----------------|------|-------|

- Founder control structure: dual-class shares / concert parties / VIE structure
- Trend in founder equity stake (dilution per funding round)
- Employee stock ownership plan: coverage, vesting conditions, tied to listing

**Governance Structure**:
- Board composition (independent director ratio, investor board seats)
- Major decision-making mechanisms
- Potential conflicts of interest:
  - Related-party transactions (transactions between the founder's other companies and this company)
  - Competition in the same business
  - Points of conflict between controlling shareholder and minority shareholder interests

### 4. Investor Roster Deep Analysis

| Investor | Round | Amount | Estimated Stake | Type | Strategic Value | Exit Pressure |
|----------|-------|--------|-----------------|------|----------------|---------------|

Analysis:
- Brand endorsement significance of lead institution (top-tier VC vs. unknown fund)
- Strategic synergy value of industrial capital (does it bring resources/channels?)
- Investor exit pressure assessment:
  - How much time remains in the fund's life?
  - Has it sold secondary shares already?
  - Are earn-out clauses approaching expiry?
- Red flags in the investor roster:
  - Are there investors with poor reputations?
  - Have early investors already fully exited?
  - Follow-on participation in the most recent round (existing investors not participating = lack of confidence?)

### 5. Full-Spectrum Risk Checklist

| Risk Type | Specific Risk | Probability (H/M/L) | Impact (H/M/L) | Severity | Hedgeable? | Monitoring Metric |
|-----------|---------------|---------------------|----------------|----------|------------|-------------------|
| Regulatory risk | Antitrust, data security, industry crackdown, license risk | | | | | |
| Competitive risk | Big tech entry, new model disruption, price war | | | | | |
| Technology risk | Platform migration, AI disruption, technology path failure | | | | | |
| Talent risk | Founder/core team departure | | | | | |
| Funding risk | Capital shortage, down round, difficulty fundraising | | | | | |
| IPO risk | Listing window, regulatory approval, market conditions | | | | | |
| Geopolitical risk | Brazil-US relations, currency (BRL/USD) exposure, cross-border data, sanctions | | | | | |
| Monetization risk | Monetization below expectations, user backlash | | | | | |
| Governance risk | Related-party transactions, information opacity, investor conflicts | | | | | |
| Compliance risk | Data privacy (LGPD / GDPR), content compliance, BACEN regulations | | | | | |
| Macro risk | Economic cycle, interest rate environment, capital market sentiment | | | | | |
| ESG risk | Environmental / social / governance related risks | | | | | |

### 6. Exit Path Analysis

| Exit Method | Likelihood (★1-5) | Estimated Time Window | Expected Valuation Range | Key Prerequisites | Main Obstacles |
|-------------|-------------------|-----------------------|--------------------------|-------------------|----------------|
| B3 IPO (Novo Mercado) | | | | | |
| US IPO (NYSE/Nasdaq) | | | | | |
| CVM-registered offering | | | | | |
| Acquisition | | Potential acquirers? | | | |
| Secondary market transfer | | Liquidity? | | | |
| SPAC | | | | | |
| Long-term no exit | | | | | |

- Most likely exit path and rationale
- Exit timeline modeling
- Expected return analysis under each exit path

### 7. Worst-Case Scenario Analysis (Munger-Style Inversion)

> "Invert, always invert." — Munger

- How is this company most likely to **fail**? List 3 specific failure paths
- Probability assessment and trigger conditions for each failure path
- In the worst case, how much can investors recover? (Liquidation value analysis)
- Why would a smart person **not** invest in this company? (List at least 5 reasons)
- Historically, which companies with a similar positioning/stage failed? Why?
- What signal, if it appears, means "the thesis is broken" and it's time to cut losses?
```

---

#### Task 5: Technology Capability & Intellectual Property Analysis
- subject: `Analyze {Company Name}'s tech stack, patent portfolio, and R&D capability`
- activeForm: `Analyze {Company Name} technology capability and intellectual property`
- description contains:

```
## Technology Capability & Intellectual Property Deep Analysis

> For technology companies, the authenticity and durability of the technology moat directly determines the reasonableness of the valuation.

### 1. Tech Stack Analysis
- Core technology architecture inference (from hiring data, tech blogs, open-source projects, conference talks)
- Whether the tech stack choices are appropriate (right tools for the right problems)
- Technical debt signals:
  - Are many "refactoring/migration" roles being hired?
  - Is a large-scale tech stack switch underway?
  - Frequent bug/outage complaints on the user side?

### 2. Patent Portfolio Analysis
Search patent databases (Google Patents, INPI Brasil, USPTO):

| Patent Metric | Data | Source |
|---------------|------|--------|
| Total patents (granted) | | |
| Patents pending | | |
| New patents added in last 2 years | | |
| Distribution of core technology areas | | |
| Citation count of key patents | | |
| International coverage of patent portfolio | | |

- Patent quality assessment (not just quantity):
  - Are there core/foundational patents?
  - Do patents cover technology areas consistent with the core business?
  - Is there patent litigation (being sued or actively suing)?
- Patent trends: is the application rate accelerating or slowing? Any shift in technology direction?
- Patent comparison with competitors

### 3. R&D Capability Assessment
- **R&D investment**:
  - R&D headcount and share (estimated from job boards, LinkedIn)
  - R&D expense estimation (headcount × average compensation + infrastructure)
  - R&D expense ratio (compared to peers)
  - R&D investment trend: increasing or decreasing?
- **R&D output**:
  - Academic paper publications (search Google Scholar, arXiv)
  - Technical conference presentations (search top venues: KDD, NeurIPS, SIGIR, etc.)
  - Open-source contributions (search GitHub organization accounts)
  - Technical blog / official account output
- **R&D efficiency**:
  - Speed from technical R&D to product deployment
  - Commercialization rate of technical achievements

### 4. Technical Talent Assessment
- **Core technical leaders**: CTO / VP Eng / Chief Scientist background and capability
  | Name | Title | Education | Previous company | Technical influence |
  |------|-------|-----------|-----------------|---------------------|
- **Technical talent density**:
  - Which companies/labs do they come from? (Share from Google / Meta / Microsoft / Nubank / TOTVS / CI&T / Itaú / XP and other top institutions)
  - Compensation competitiveness of technical roles (estimated from job listings)
  - Attrition signals for the tech team (departure activity on LinkedIn)
- **Hiring signals**:
  - What technical roles are currently being hired? (Reflects technology strategy direction)
  - Difficulty and fill speed for technical roles
  - Is a new tech team/lab being built?

### 5. Technology Moat Assessment

| Technology Barrier Dimension | Rating (★1-5) | Evidence | Durability |
|------------------------------|---------------|----------|------------|
| Algorithm / model barrier | | Is there a proprietary algorithm? Can it be replicated? | |
| Data barrier | | Data volume, proprietary data, data flywheel speed | |
| Engineering barrier | | System complexity, long-accumulated engineering capability | |
| Talent barrier | | Are core technical talents irreplaceable? | |
| Ecosystem barrier | | Developer ecosystem, API/SDK coverage, technical standards | |

- Overall technology moat rating: Strong / Moderate / Weak
- Assessment of how quickly the technology moat is eroding (in the AI era, technology barriers may have a short half-life)

### 6. AI / New Technology Impact Assessment
- The company's AI capabilities and positioning
- Impact of AI on the company's core business (enhancing / threatening / neutral)
- Is the company a beneficiary or a disruption target of the AI revolution?
- Impact assessment of other emerging technologies (Web3 / AR / VR / quantum computing, etc.)

### 7. Technology Risk Checklist
| Risk | Specific Description | Probability | Impact |
|------|---------------------|-------------|--------|
| Technology path failure | The chosen technology direction is proven wrong | | |
| Open-source substitution | Core technology replaced by an open-source solution | | |
| Platform dependency | Dependency on a specific cloud / chip / OS | | |
| Security vulnerability | Data breach / system attack | | |
| Talent attrition | Core technical staff departure | | |
```

---

#### Task 6: Alternative Data Signal Mining
- subject: `Mine unconventional data signals and hidden clues for {Company Name}`
- activeForm: `Mine {Company Name} alternative data signals`
- description contains:

```
## Alternative Data Signal Mining

> Private companies have limited conventional information. Alternative data often provides more authentic operating signals than news coverage.
> The goal of this task is: beyond conventional information sources, mine every potentially useful clue.

### 1. Hiring Signal Analysis
Search LinkedIn, Indeed Brasil, Glassdoor Brasil, Catho, InfoJobs for job listings:

**Hiring scale & trends**:
- Current total open positions
- Hiring trend over the past 6 months (accelerating / stable / contracting)
- Comparison of hiring scale vs. competitors

**Hiring structure analysis**:
| Job Category | Count | Share | Signal Interpretation |
|--------------|-------|-------|-----------------------|
| R&D / Engineering | | | Technology direction |
| Product | | | Product strategy |
| Sales / BD | | | Monetization stage |
| Marketing / Operations | | | Growth strategy |
| Data / AI | | | AI positioning |
| International | | | Overseas expansion plans |
| Compliance / Legal | | | Regulatory response / IPO prep |
| Finance / IR | | | IPO preparation signal |

**Key signal capture**:
- Hiring IR (Investor Relations) = IPO signal
- Hiring Compliance / Data Security = regulatory pressure or IPO preparation
- Hiring overseas roles = international expansion
- Salary range for senior roles = company's financial strength and talent competitiveness
- Tech stack / business direction mentioned in JDs = strategic direction

### 2. App / Product Data Analysis
Search App Store, Google Play, SimilarWeb, data.ai (App Annie):

| Metric | Data | Source | Trend |
|--------|------|--------|-------|
| App Store ranking | | | 6-month trend |
| User rating | | | Direction of change |
| Rating count | | | Growth rate |
| Download volume estimate | | | |
| App update frequency | | | |
| Major features in recent updates | | | |

- High-frequency keywords and sentiment analysis in App Store reviews
- Main focus areas of recent negative reviews (bugs? fees? deteriorating experience?)
- Web traffic data (SimilarWeb): UV, PV, session duration, bounce rate

### 3. Social Media & Sentiment Signals
Search Twitter/X, Reddit, LinkedIn, Facebook Brasil, Instagram, Reclame Aqui:

- Engagement data for official company accounts (follower / repost / comment trends)
- Volume and sentiment of organic user discussion (positive / negative / neutral)
- Industry KOL/influencer assessments of the company
- Hot sentiment events in the past 3 months
- List of negative sentiment events and the company's response approach
- Any leaks from insiders (former/current employees)

### 4. Corporate Registration & Legal Signals
Search Receita Federal (CNPJ), Junta Comercial (JUCESP/JUCERJA), Jusbrasil, CVM EDGAR Brasil:

**Business registration information**:
- Capital social (registered capital) and history of changes
- Capital integralizado (paid-in capital)
- Shareholder / equity change records (alterações contratuais)
- List of subsidiaries / affiliated companies (new = new business? dissolved = business contraction?)
- Changes in object social / business scope (newly added = new business direction)

**Legal information**:
| Type | Count | Summary of Important Cases |
|------|-------|---------------------------|
| Litigation as plaintiff | | |
| Litigation as defendant | | |
| Intellectual property disputes | | |
| Labor arbitration | | |
| Administrative penalties | | |
| Enforcement records | | |

- Details and potential financial impact of major litigation/arbitration
- Administrative penalty records (environmental / tax / labor / data security, etc.)

### 5. Supply Chain & Partner Signals
- List of known core suppliers/partners
- Are suppliers listed? Do their financial reports mention collaboration data with this company?
- Tender/procurement information (government procurement portals, corporate bidding platforms)
- Partner assessments and depth of collaboration

### 6. Domain & Digital Footprint
Search domain/subdomain information:
- List of domains registered by the company (newly registered domains may hint at new businesses/products)
- Subdomain analysis (api.xx.com, pay.xx.com, etc. hint at business architecture)
- SSL certificate information
- Trademark registration status (new trademark registrations = new brand/product line)

### 7. Industry Conference & Exposure Signals
- Conference speeches / attendance records by company executives in the past 12 months
- Industry awards / media rankings (has it appeared on "Unicorn," "Most Innovative," etc. lists?)
- Interaction with government / industry associations (policy consultation, standards body participation)
- Trend in frequency and quality of media coverage

### 8. Secondary Market Trading Signals (if applicable)
- Is there a secondary market for old shares? (SharesPost, EquityZen, Brazilian secondary platforms, private WhatsApp/Telegram investor groups, etc.)
- Implied valuation from secondary share trades vs. latest funding round valuation
- Supply/demand conditions for buyers and sellers
- Are large numbers of employees selling options/RSUs?

### 9. Signal Synthesis Score

| Signal Category | Direction (Positive / Negative / Neutral) | Strength (Strong / Medium / Weak) | Confidence | Key Finding |
|-----------------|-------------------------------------------|-----------------------------------|------------|-------------|
| Hiring signals | | | | |
| Product data | | | | |
| Sentiment signals | | | | |
| Legal signals | | | | |
| Supply chain signals | | | | |
| Digital footprint | | | | |
| Industry exposure | | | | |
| Secondary trading | | | | |

**Combined signal judgment**: Do all signals point in the same direction? Are there contradictory signals?

### 10. Anomalous Signal Checklist (Most Important)
List all "unusual" findings — these are often the most valuable information:
- Signals inconsistent with the company's public narrative
- Data that contradicts industry common sense
- Sudden changes (rapid hiring contraction/expansion, concentrated executive departures, etc.)
- Unexplained phenomena
```

---

### Step 4: Launch 6 Parallel Agents

Use the Agent tool to simultaneously launch 6 agents (**must be called in parallel in the same message**):

Configuration for each agent:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`

Prompt template for each agent:

```
You are the "{role name}" on the private company research team for {Company Name}.

You are researching a **private company**, which means:
- No standardized public financial reports — information must be pieced together from multiple sources
- Data may be incomplete or contradictory — confidence levels must be noted
- More inference and reasonable estimation is required, but the estimation process must be transparent
- Unable to find information ≠ information doesn't exist; information found may be biased

Please complete the following research task: {task subject}

Specific requirements:
{task description content}

**Research methodology**:
1. Use WebSearch to search for the latest public information. Search at least 3-5 times per dimension using different keyword combinations
2. Keyword strategy:
   - Portuguese: company name + receita/valuation/rodada/usuários/IPO/prospecto/demissões/autuação/fusão
   - English: Company Name + revenue/valuation/funding/users/IPO/filing/acquisition
   - Specific person name + company name (for management-related information)
   - Company name + specific competitor name (for competitive dynamics)
3. Priority information sources:
   - High credibility: CVM filings (DFP/ITR/FRE), prospectuses, related disclosures in listed company annual reports
   - Medium credibility: Pipeline (Valor Econômico), Bloomberg Línea, The Information, Startups.com.br, Reuters, TechCrunch, NeoFeed
   - Supplemental validation: Reclame Aqui, Glassdoor Brasil, LinkedIn, Jusbrasil, Receita Federal CNPJ
4. Use WebFetch to retrieve full text of key articles (don't rely only on search snippets)
5. For important data, cross-validate with at least 2 different sources

**Data annotation standards (strictly enforced)**:
- Note the source for every key data point (specific media name and article title)
- Note the data date (accurate to year and month)
- Note confidence level: 🟢 High (prospectus/CVM filing/official disclosure) / 🟡 Medium (credible media/research report) / 🔴 Low (estimate/rumor)
- When data from different sources conflicts, **list all** and explain the discrepancy and your judgment
- Distinguish "facts" from "reasoning": facts in normal text, reasoning/estimates in *italics* with the estimation method noted
- Explicitly label unavailable information as "data missing" — do not fabricate

**Output requirements**:
- Report should be thorough, using Markdown tables to present key data
- Each analytical dimension should have a clear conclusion and rating
- Estimation processes must be fully transparent (show calculation logic and every assumption step)
- At the end of the report, provide:
  1. Overall rating for this dimension (★1-5) and core judgment
  2. Self-assessment of information completeness for this dimension (Sufficient / Moderate / Insufficient / Severely insufficient)
  3. The 3 most important findings
  4. The biggest information blind spot (what missing information most affects the judgment)
```

### Step 5: Receive Reports & Track Progress

- Show the user a real-time progress table (which agents have completed, which are still researching)
- When each report is received, update progress and show the key points of that report (3-5 bullets)
- Wait for all 6 reports

### Step 6: Cross-Validation & Information Synthesis

**This is the most critical new step in the enhanced framework**. Before consolidating, the team-lead must:

1. **Data conflict arbitration**:
   - Extract key data from each agent's report
   - Identify whether the same data cited by different agents is consistent
   - Arbitrate conflicting data: list all sources, state which one is adopted and why

2. **Signal consistency check**:
   - Business growth signals (business-decoder) vs. hiring signals (signal-miner) — are they consistent?
     (If claiming rapid business growth but hiring is contracting, an explanation is needed)
   - Technology leadership narrative (tech-ip) vs. patent/talent data (signal-miner) — is it supported?
   - Valuation level (financial-detective) vs. competitive position (competitive-mapper) — does it match?
   - Management's public narrative (risk-governance) vs. actual action signals (signal-miner) — are they consistent?

3. **Information jigsaw reconstruction**:
   - Piece together information fragments from all 6 reports to see if a more complete picture emerges
   - Annotate information as "white zones" (confirmed known), "gray zones" (clues but uncertain), or "black zones" (completely unknown)

4. **Anti-bias check**:
   - Check whether reports exhibit a bias of "positive information detailed, negative information brief"
   - Confirm every positive judgment has a corresponding counter-check

### Step 7: Consolidate Final Report

Synthesize the 6 analysis reports and output a final report with the following structure:

---

#### 1. One-Sentence Conclusion
> Summarize in a paragraph (50-100 words) the **true value judgment** of this private company: what the business is worth and why.

#### 2. Company Profile Snapshot
| Item | Content | Confidence |
|------|---------|------------|
| Company name | | |
| Founded | | |
| Headquarters | | |
| Founder / CEO | | |
| Core business | | |
| Headcount | | |
| Latest valuation | | |
| Latest funding round | | |
| Estimated revenue | | |
| Estimated profitability | | |
| Estimated user scale | | |
| Key investors | | |
| VIE / Red-chip structure | | |

#### 3. Six-Dimension Score Summary
| Dimension | Analyst | Rating (★1-5) | Core Judgment | Confidence | Information Completeness |
|-----------|---------|---------------|---------------|------------|--------------------------|
| Business model & users | business-decoder | | | | |
| Finance & valuation | financial-detective | | | | |
| Industry & competition | competitive-mapper | | | | |
| Risk & governance | risk-governance-analyst | | | | |
| Technology & IP | tech-ip-analyst | | | | |
| Alternative data signals | signal-miner | | | | |

Overall score: ★X / 5

#### 4. Key Data Jigsaw (Post Cross-Validation)
Integrate data pieced together by all analysts. **Only retain cross-validated data**:

| Metric | Data | No. of Sources | Source Details | Confidence | Notes |
|--------|------|----------------|----------------|------------|-------|

#### 5. Signal Consistency Matrix
| Check Item | Signal A | Signal B | Consistency | Interpretation |
|------------|---------|---------|-------------|----------------|
| Growth narrative vs. hiring trends | | | ✅/⚠️/❌ | |
| Technology leadership narrative vs. patent data | | | | |
| Valuation level vs. competitive position | | | | |
| Management narrative vs. actual actions | | | | |

#### 6. Dimension-by-Dimension Analysis Summary
Extract 3-5 most important findings per dimension (with source and confidence noted)

#### 7. True Value Assessment

**Business essence judgment**:
- What kind of business is this? (One sentence)
- How high is the "certainty" of this business?
- Duan Yongping style judgment: Is this a "right business"?

**Economic Moat Scorecard**:
| Moat Type | Rating (★1-5) | Core Evidence | Trend | Durability |
|-----------|---------------|---------------|-------|------------|
| Network effects | | | Widening / Stable / Narrowing | |
| Switching costs | | | | |
| Brand mindshare | | | | |
| Data barrier | | | | |
| Regulatory license | | | | |
| Economies of scale | | | | |
| Technology barrier | | | | |

**Valuation judgment**:
| Valuation Method | Valuation Range | Confidence | Notes |
|-----------------|-----------------|------------|-------|
| Latest funding round (adjusted) | | | |
| Comparable company analysis | | | |
| DCF scenario analysis | | | |
| Terminal value back-calculation | | | |
| Transaction comparable analysis | | | |

**Consolidated true value range**:
- Conservative valuation (margin of safety valuation): $XXB
- Fair valuation (base case assumptions): $XXB
- Optimistic valuation (best-case scenario): $XXB
- Current market valuation: $XXB
- **Margin of safety**: current valuation vs. conservative valuation = XX%

#### 8. Investment Thesis (Bull vs. Bear)
- 🟢 Bull case (5-7 points, each with source cited)
- 🔴 Bear case (5-7 points, each with source cited)
- ⚖️ Which side's argument is more convincing? Why?

#### 9. Risk Matrix
| Risk | Probability | Impact | Combined Severity | Hedgeable? | Monitoring Metric |
|------|-------------|--------|-------------------|------------|-------------------|

Top 3 core risks and mitigation strategies

#### 10. Exit Path Assessment
Most likely exit method, time window, and expected return

#### 11. Investment Decision Table

**One-page decision table**:
```
┌──────────────────────────────────────────────┐
│  Company: XXX    Latest valuation: $XXB       │
│  Stage: [Seed / Growth / Mature / Pre-IPO]   │
│  Information completeness: [Sufficient / Moderate / Insufficient / Severely insufficient] │
├──────────────────────────────────────────────┤
│  Core investment thesis (3 sentences max):   │
│  1. ________________________________________  │
│  2. ________________________________________  │
│  3. ________________________________________  │
├──────────────────────────────────────────────┤
│  True value judgment:                         │
│  Fair valuation range: $XXB - $XXB           │
│  Current valuation vs. fair value: Expensive / Fair / Cheap │
│  Margin of safety: ____%                      │
├──────────────────────────────────────────────┤
│  Key assumptions & validation:               │
│  Assumption 1 → Tracking metric → Validation node → Validation date │
│  Assumption 2 → Tracking metric → Validation node → Validation date │
│  Assumption 3 → Tracking metric → Validation node → Validation date │
├──────────────────────────────────────────────┤
│  Fatal risks & "thesis broken" signals:      │
│  Risk 1 → If X happens, conclusion flips → Stop-loss strategy │
│  Risk 2 → If Y happens, conclusion flips → Stop-loss strategy │
├──────────────────────────────────────────────┤
│  Conclusion: Invest / Watch / Avoid          │
│  If watching: what trigger condition prompts re-evaluation? │
│  Expected exit: IPO / Acquisition / Secondary transfer │
│  Expected return multiple: X - Y x           │
│  Expected time horizon: X - Y years          │
│  Annualized return: X% - Y%                  │
└──────────────────────────────────────────────┘
```

**Tiered recommendation**:
| Investor Type | Recommendation | Rationale |
|---------------|----------------|-----------|
| PE/VC institution (lead investor) | | |
| PE/VC institution (co-investor) | | |
| Secondary market transfer | | |
| Post-IPO buyer | | |
| Not recommended | | |

**Key catalysts**:
| Bull catalyst | Estimated timing | Bear catalyst | Estimated timing |
|---------------|-----------------|---------------|-----------------|
| | | | |

#### 12. Information Blind Spot Map
| Dimension | Known Information | Missing Information | Impact of Missing Info | Acquisition Suggestion |
|-----------|-----------------|--------------------|-----------------------|------------------------|

Do these information blind spots affect the reliability of core conclusions? If so, explicitly state: "With X information missing, the confidence level of the above conclusions is Y."

#### 13. Ongoing Monitoring Checklist
| Tracking Item | Frequency | Information Source | Key Metric | Warning Threshold |
|---------------|-----------|-------------------|------------|-------------------|

#### 14. Summary Paragraph
150-250 word final summary, including:
- The essence of the business
- True value judgment
- Reasonableness of current valuation
- Greatest certainty and uncertainty
- Final recommendation and core rationale

---

### Step 8: Save Report

Write the complete final report to `reports/{Company Name}/{Company Name}-private-{YYYYMMDD}.md`.

### Step 9: Clean Up Team

Use TeamDelete to clean up team resources.

---

## Important Notes

1. **6 agents must be launched in parallel** — call the Agent tool 6 times in a single message
2. **Annotate data confidence** — private company data sources vary in quality; every key data point must note source and confidence level
3. **Estimation must be transparent** — all estimation processes must show calculation logic; no numbers out of thin air
4. **Cross-validation** — key data must be cross-validated with at least 2 sources; list all sources when they conflict
5. **Signal consistency check** — the consolidation phase must include cross-dimension signal consistency checks
6. **Conclusions must be clear** — do not shy away from giving an Invest / Watch / Avoid recommendation, but also state the confidence level of the conclusion
7. **Be patient** — research by 6 agents takes several minutes; update progress to the user in real time
8. **Search in both Portuguese and English** — private company information may be distributed across Portuguese and English media; search in both languages
9. **Anti-bias core principle** — less material ≠ worse company; shorter AI analysis ≠ lower investment certainty. For companies with extremely scarce information, switch to "first-principles mode" and focus on core questions without chasing a formally complete report
10. **Honest blanks** — clearly distinguish "evidence-based analysis" from "speculative fill-in" in the report; it is acceptable to state "insufficient data in this dimension to reach a meaningful conclusion"
11. **Alternative data is not noise** — hiring, patents, litigation, App data, and other alternative data may be closer to the true operating reality than news coverage
12. **True value orientation** — the ultimate goal is to judge what the business is actually worth, not to produce an impressive-looking report. If information is insufficient for a reliable valuation judgment, simply state "insufficient information; unable to provide a reliable valuation"
