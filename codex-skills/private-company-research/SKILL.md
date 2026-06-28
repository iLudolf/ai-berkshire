---
name: private-company-research
description: "AI Berkshire skill: Private company research — multi-agent parallel deep research framework. Source: skills/private-company-research.md."
---

## Codex adapter note

This skill is generated from `skills/private-company-research.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Private Company Research: Multi-Agent Parallel Deep Research Framework

Conduct a team-based deep research analysis of $ARGUMENTS. Designed specifically for private companies such as Ant Group, Xiaohongshu, SpaceX, and Stripe.

**Ultimate goal**: Under conditions of naturally scarce information, reconstruct the **true value** of this business as faithfully as possible — not the valuation the market assigns, but what the business itself is actually worth.

## Framework Characteristics

Core differences between private vs. public company research:
- **No standardized financial reports**: must piece together information from multiple sources and cross-validate
- **Fewer valuation anchors**: relies on funding rounds, comparable company analysis, and scenario modeling
- **High information asymmetry**: requires more "puzzle-piece" research methods
- **Uncertain exit paths**: IPO / M&A / secondary transfer are all possibilities

## AI Research Bias Awareness (Core Premise of This Framework)

Private companies are the domain where AI research bias is most severe. The following traps must be guarded against at all times:

**Core contradiction**: AI excels at structuring existing information, but private company information is naturally scarce. This leads to:
1. **False conservatism**: Because source material is thin, AI tends toward conservative/vague conclusions — but thin sources do not equal a bad company
2. **False precision**: To fill out report templates, AI may dress up "reasonable speculation" as "evidence-based analysis"
3. **Benchmarking trap**: Forcing comparisons against public companies inherits public-company valuation logic, ignoring the unique value of private companies
4. **Survivorship bias**: Company information findable online tends to skew positive (companies actively broadcast good news)

**Mitigation principles**:
- Leave blanks and say "unknown" rather than filling tables with speculation that mimics certainty
- Every data point must be labeled with a confidence level (🟢High / 🟡Medium / 🔴Low) so readers can judge for themselves
- Distinguish "verifiable facts" from "AI reasoning" using different formatting
- For companies with extremely scarce information, switch to "first-principles mode" — don't chase report completeness; only answer a few core questions:
  1. What real problem does this business solve? Is the demand genuine or artificial?
  2. Why this team? What unique advantages do they have?
  3. If they succeed, how high is the ceiling? If they fail, where are they most likely to die?
  4. What are the key validation milestones at the current stage?

**Turning information asymmetry to advantage**: The market has less information on private companies → lower pricing efficiency → this is precisely where excess returns may originate. The goal of AI research is not to eliminate information asymmetry (impossible), but to extract the most critical judgment inputs from limited information.

---

## Execution Flow

### Step 1: Present the Team Framework

Show the user the following team structure and confirm before starting:

| Role | Responsibilities | Core Perspective |
|------|-----------------|-----------------|
| **team-lead** (you) | Coordination, information integration, cross-validation, final report | Investment decision synthesis |
| **business-decoder** | Business model breakdown & product/user analysis | "What is the essence of this business" |
| **financial-detective** | Financial data reconstruction & valuation modeling | "Reconstruct the true financial picture under conditions of missing data" |
| **competitive-mapper** | Industry landscape, competitive dynamics & substitution threats | "Who is competing with it, who might disrupt it" |
| **risk-governance-analyst** | Full risk panorama & management/governance/investor assessment | "What could go wrong, who is at the helm" |
| **tech-ip-analyst** | Tech stack / patents / R&D capability / technology moat | "Is the technology barrier real, and how long will it last" |
| **signal-miner** | Alternative data mining: hiring / patents / litigation / app data / supply chain | "Beyond conventional information, what other clues exist" |

### Step 2: Create the Team

Use TeamCreate to create the team:
- team_name: `{CompanyName}-private-research` (lowercase English, e.g. `ant-group-private-research`)
- agent_type: `team-lead`

### Step 3: Create 6 Tasks

Use TaskCreate to create the following 6 tasks (each must have a subject, description, and activeForm):

---

#### Task 1: Business Model and Product/User Deep Analysis
- subject: `Deconstruct {CompanyName} business model, product portfolio, and user ecosystem`
- activeForm: `Analyze {CompanyName} business model and user ecosystem`
- description contains:

```
## Business Model Deep Breakdown

### 1. Core Business Definition
- Define the essence of this business in one sentence (Duan Yongping style: use plain language to explain the business to a smart person unfamiliar with the industry)
- What problem does the company solve? For whom does it create value?
- Value proposition and differentiation from comparable products
- If the company didn't exist, how would users solve this problem? How costly are the alternatives?
- "Stickiness" judgment on demand: would users cut this expense during an economic downturn?

### 2. Revenue Model Breakdown
- Revenue composition: advertising / commissions / subscriptions / transaction take rates / financial services / SaaS / hardware / licensing fees, etc.
- Share of each revenue line (if data available) and growth trends
- Monetization efficiency metrics: ARPU, Take Rate, ad load rate, conversion rate, etc.
- Revenue quality assessment:
  - Recurring revenue vs. one-time revenue ratio
  - Revenue concentration: top 5 customers/channels share
  - Revenue predictability (contract/subscription-type vs. transaction-type)
  - Whether revenue recognition method is reasonable (any signs of premature recognition)
- Benchmark monetization efficiency against listed industry peers

### 3. Unit Economics (UE) Modeling
- CAC (Customer Acquisition Cost) estimation:
  - Paid acquisition vs. organic growth ratio
  - CAC by channel (if available)
  - CAC trend: rising or falling as scale grows?
- LTV (Lifetime Value) estimation:
  - ARPU × expected customer lifetime
  - Consider cross-sell and upsell
- LTV/CAC ratio, payback period
- Marginal cost structure: trend in marginal cost per new user/transaction
- Scale economy inflection point: when/has the breakeven point been passed?

### 4. Product Portfolio and Flywheel Effect
- Core products + extension products + incubation products
- How the flywheel operates: network effects / data flywheel / scale economies
- Synergies and cross-traffic among products
- Product lifecycle: which stage is each product in?
- Product iteration speed: app/product update frequency, major feature updates in the past 12 months

### 5. Business Model Canvas (BMC)
Describe the business model fully using these 9 elements:
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
- User scale: MAU/DAU (estimated from QuestMobile, Sensor Tower, SimilarWeb, etc.)
- User growth curve: which stage of the S-curve? (support with concrete data)
- User engagement metrics:
  - DAU/MAU ratio (daily active / monthly active ratio)
  - Average session duration, open frequency
  - D1/D7/D30 retention rates (if available)
  - User growth vs. retention trend comparison (fake growth identification)
- User profile: age / geography / purchasing power / occupation distribution
- User sentiment:
  - App Store / Google Play rating trends (changes over the past 12 months)
  - Social media sentiment analysis
  - Genuine user feedback on Zhihu / Weibo / Xiaohongshu
  - Main focal points of negative reviews
- User acquisition efficiency:
  - Paid acquisition vs. organic growth vs. word-of-mouth ratio
  - Whether acquisition is concentrated in a single channel

### 7. Pricing Power Assessment
- Has there been a price increase in the past 3 years? What was the user churn after the increase?
- Price comparison with competitors: price leader or follower?
- Assessment of user price sensitivity
- Reasonableness of commission/take rate within the value chain

### 8. Moat Assessment
Verify and score each of the following 6 dimensions (★1-5):

| Moat Type | Score | Evidence | Trend | Durability Assessment |
|-----------|-------|---------|-------|----------------------|
| Network Effects | | The more users, the more valuable? Single-sided or multi-sided? | Widening/Stable/Narrowing | |
| Switching Costs | | Cost for users to migrate to a competitor? Data/relationship/habit migration cost? | | |
| Brand Mindshare | | Category = brand? NPS estimate? | | |
| Data Moat | | Has a data flywheel formed? Proprietary data assets? Data scale? | | |
| Regulatory Licenses | | Are there entry barriers? How difficult to obtain a license? | | |
| Scale Economies | | Are scale-driven cost advantages significant? | | |

Overall moat rating: Wide / Moderate / Narrow / None

### 9. Internationalization Analysis (if applicable)
- Progress in overseas market expansion
- International revenue share
- Localization strategy and challenges
- Differences in competitive landscape abroad
```

---

#### Task 2: Financial Data Reconstruction and Valuation Modeling
- subject: `Reconstruct {CompanyName} financial data and conduct valuation analysis`
- activeForm: `Reconstruct {CompanyName} financial data and valuation`
- description contains:

```
## Financial Data Reconstruction (Detective-Style Research)

Private companies have no standard financial reports; data must be pieced together from multiple sources and cross-validated. Every data point must be traced to a specific source with time and confidence level noted.

### 1. Data Source Matrix
**Search the following sources in priority order**:

| Priority | Source Type | Specific Source | Credibility | Search Method |
|----------|------------|----------------|-------------|---------------|
| 1 | Prospectus / Regulatory Filings | SEC Filing, HKEX, CSRC-disclosed draft prospectuses | 🟢High | Search "company name + prospectus/IPO filing" |
| 2 | Parent / affiliated listed company financials | e.g., Ant data in Alibaba annual report, Google Cloud annual report | 🟢High | Search parent company annual reports for related-party disclosures |
| 3 | Regulatory penalties / compliance disclosures | PBOC, CSRC, SAMR penalty documents | 🟢High | Search "company name + penalty/fine/rectification" |
| 4 | Bond / ABS issuance documents | e.g., underlying data in Ant Huabei ABS prospectus | 🟢High | Search "company name + bond/ABS/trust" |
| 5 | Business registry information | Annual reports and paid-in capital from Tianyancha / Qichacha | 🟡Medium-High | |
| 6 | Funding news | Valuation, funding amount, investors | 🟡Medium | Search "company name + funding/valuation" |
| 7 | Third-party research reports | Broker, consulting firm, industry association reports | 🟡Medium | Search "company name + research report" |
| 8 | In-depth media coverage | LatePost, The Information, 36Kr, Bloomberg | 🟡Medium | Search these outlets directly with company name |
| 9 | Industry data back-calculation | Reverse-calculated from total industry size and market share | 🔴Low-Medium | |
| 10 | Ex-employees / insiders | Blind, Maimai, forums | 🔴Low | For reference only, not as primary basis |

### 2. Key Financial Metric Estimation
Estimate the following data where possible. **Every data point must specify**: source, date, confidence level, and estimation method.

**Revenue side**:
- Total revenue scale and growth rate (past 3 years, annual/quarterly granularity)
- Revenue structure breakdown (by business line / product line)
- Revenue growth driver decomposition: volume (users/transactions) × price (ARPU/ticket size)
- Seasonal revenue fluctuation patterns

**Cost side**:
- Gross margin estimate (benchmarked against listed industry peers, explain selection logic)
- R&D expense ratio estimate (via headcount × average compensation, or R&D headcount share)
- Sales expense ratio estimate (via acquisition channels and advertising data)
- G&A expense ratio estimate

**Profit side**:
- Operating profit / EBITDA estimate
- Net income / adjusted net income estimate
- Profitability timeline: when did/will the company reach profitability? If not yet profitable, when is the expectation?

**Cash flow side**:
- Operating cash flow assessment (positive/negative, self-sustaining or not)
- Capex level and trend
- Free cash flow estimate
- Cash on hand / burn rate (estimated via funding amounts, funding intervals, headcount)
- Cash runway: at the current burn rate, how long can the company survive?

**Efficiency metrics**:
- Headcount and revenue/profit per employee
- Capital efficiency: revenue generated per dollar raised
- Benchmark efficiency metrics against listed industry peers

### 3. Financial Data Cross-Validation
- If multiple sources exist for the same metric, list all and explain discrepancies
- Use different methods to estimate the same metric; check whether results converge
- Flag any data that cannot be verified as a "single-source finding"

| Metric | Source A (data/date) | Source B (data/date) | Discrepancy | Adoption Judgment |
|--------|---------------------|---------------------|-------------|-------------------|

### 4. Funding History and Valuation Evolution
Compile a complete funding timeline:

| Round | Date | Amount | Pre-money Valuation | Post-money Valuation | Lead Investor | Co-investors | Valuation Multiple Growth | Notes |
|-------|------|--------|--------------------|--------------------|--------------|-------------|--------------------------|-------|

Analysis:
- Is the valuation growth curve healthy (is the multiple increase per round reasonable)?
- Is the funding interval reasonable (too frequent = burning cash fast? too sparse = difficulty raising?)
- Has there been a down round?
- Have existing investors continued to participate (confidence signal)?
- Inferred investment terms for the latest round:
  - Liquidation preference (1x / 2x / participating)
  - Anti-dilution protection (full ratchet / weighted average)
  - Ratchet clauses (performance / IPO timing)
  - Impact of these terms on common stock value

### 5. Valuation Analysis (Multi-Method Cross-Check)

**Method 1: Latest Funding Round Valuation**
- Most recent round valuation and date
- "Common stock equivalent valuation" after adjusting for liquidation preference and other terms (typically needs a 20–40% discount)
- Adjustment for time elapsed since that round
- Analysis of that round's investor motivations (financial vs. strategic investor; strategic investors may pay a premium)

**Method 2: Comparable Public Company Method**
- Select 3–5 listed comparable companies and explain the selection rationale
- Key multiples comparison:

| Comparable Company | P/S | P/E | EV/EBITDA | EV/Revenue | Growth Rate | Margin |
|--------------------|-----|-----|-----------|------------|------------|--------|

- Adjustments applied:
  - Illiquidity discount: 20–30% (specify the value used and rationale)
  - Growth premium/discount
  - Size discount
  - Regulatory/policy risk discount

**Method 3: DCF Scenario Analysis**
Three scenarios, each with key assumptions stated:

| Assumption | Bear | Base | Bull |
|------------|------|------|------|
| Revenue CAGR next 5 years | | | |
| Terminal operating margin | | | |
| Terminal growth rate | | | |
| WACC | | | |
| Terminal value multiple (EV/EBITDA) | | | |

Every assumption must be supported by evidence; no assumptions from thin air.

**Method 4: Reverse Engineering from Terminal Market Cap**
- Assume the market position of this business at terminal state in 5/10 years
- Terminal revenue and margin assumptions
- Reasonable terminal multiple (reference mature companies in the same industry)
- Back-calculate current fair valuation range
- Implied annualized return

**Method 5: Transaction Comparable Method**
- M&A / funding transactions in the same industry over the past 2 years
- Transaction multiples (P/S, P/E)
- Transaction context and premium/discount factors

### 6. Composite Valuation Judgment

| Method | Valuation Range | Confidence | Weight | Weighted Valuation |
|--------|----------------|------------|--------|-------------------|

- Do the different methods converge? If there is a large divergence, analyze the reasons
- The final valuation range should distinguish "fair value" from "conservative value" (margin of safety valuation)
```

---

#### Task 3: Industry Landscape and Competitive Dynamics Analysis
- subject: `Analyze the competitive landscape and substitution threats in {CompanyName}'s industry`
- activeForm: `Analyze {CompanyName} industry landscape and competitive dynamics`
- description contains:

```
## Industry Landscape and Competitive Dynamics

### 1. Industry Positioning and Market Size
- Define the core segment the company operates in (note: the segment the company itself defines may be embellished — make an independent judgment)
- TAM / SAM / SOM three-layer market sizing:
  - TAM (Total Addressable Market): the entire macro industry
  - SAM (Serviceable Addressable Market): what the company's technology/model can cover
  - SOM (Serviceable Obtainable Market): what can actually be captured today
- Comparison of market size data sources (different research firms' projections may diverge significantly)
- Market penetration: current vs. ceiling
- Industry lifecycle stage: nascent / growth / mature / decline (with supporting evidence)
- Industry growth drivers: what forces are pushing/restraining industry growth

### 2. Full Value Chain Map
Draw the complete value chain structure (text diagram):

```
Upstream suppliers (who? bargaining power?)
    ↓
Company's position (where in the value chain? profit pool share?)
    ↓
Downstream customers/users (concentration? substitute options?)
    ↕
Competitors / substitutes / potential entrants
```

- Profit pool analysis: profit distribution across value chain layers
- Company's bargaining power (upstream/downstream)
- Upstream/downstream dependency analysis: any single-supplier/single-customer concentration
- Structural changes occurring in the value chain

### 3. Porter's Five Forces Analysis (Quantified Scoring)

| Force | Intensity (★1-5) | Key Factors | Impact on Company |
|-------|-----------------|-------------|------------------|
| Intra-industry rivalry | | Concentration, differentiation, exit barriers | |
| Threat of new entrants | | Capital barriers, tech barriers, regulatory barriers, brand barriers | |
| Threat of substitutes | | Substitute price-performance, switching costs | |
| Supplier bargaining power | | Supplier concentration, switching costs | |
| Buyer bargaining power | | Customer concentration, information transparency | |

Overall industry attractiveness score: ★1-5

### 4. Competitive Landscape Deep Scan

| Competitor | Type | Market Share (estimated) | Revenue Scale | Funding/Market Cap | Core Strengths | Key Weaknesses | Threat Level |
|------------|------|------------------------|--------------|-------------------|---------------|---------------|-------------|
| Direct Competitor 1 | Direct | | | | | | |
| Direct Competitor 2 | Direct | | | | | | |
| Indirect Competitor 1 | Cross-sector | | | | | | |
| Potential Entrant 1 | Big Tech | | | | | | |

Key analysis:
- **Direct competitors**: same-segment head-on rivals; analyze each one's strategic intent and resource commitment
- **Indirect competitors**: cross-sector potential competition, especially big tech's adjacent businesses
- **Substitution threat**: different technology pathways/models, especially disruption AI may bring
- **Potential entrants**: probability and method of big tech entry (build / acquire / invest)

### 5. Deep Competitor Comparison
Select 2–3 most direct competitors (including public and private), conduct multi-dimensional comparison:

| Dimension | {CompanyName} | Competitor A | Competitor B | Competitor C |
|-----------|--------------|-------------|-------------|-------------|
| Founded | | | | |
| User Scale (MAU) | | | | |
| Revenue Scale | | | | |
| Revenue Growth | | | | |
| Total Funding / Market Cap | | | | |
| Valuation/Revenue Multiple | | | | |
| Monetization Efficiency (ARPU) | | | | |
| Gross Margin | | | | |
| Profitability Status | | | | |
| Headcount | | | | |
| Technology Capability | | | | |
| Differentiated Positioning | | | | |
| Degree of Internationalization | | | | |

### 6. Competitive Dynamics and Trends
- Key competitive landscape changes in the past 12 months (funding, M&A, product launches, executive changes)
- Inferred strategic direction of competitors (from hiring, patents, product updates)
- Structural shifts occurring in the industry
- Impact of technological change on competitive landscape (especially AI/LLMs)
- Impact of regulatory policy on competitive landscape
- Does the industry exhibit "winner-take-all" characteristics? Or will a stable oligopoly form?

### 7. Competitive Scenario Modeling
- Scenario A: Company wins — what conditions are needed? Probability?
- Scenario B: Coexistence — what are each player's survival spaces?
- Scenario C: Company is disrupted — most likely disruptors and pathways?

### 8. Global Benchmark Analysis
Identify overseas/domestic benchmark companies (listed), analyze:

| Dimension | Benchmark Company A | Benchmark Company B | Insights for {CompanyName} |
|-----------|--------------------|--------------------|--------------------------|
| Development path | | | |
| Current valuation level | | | |
| Time from similar stage to IPO | | | |
| Post-IPO stock performance | | | |
| Key success/failure factors | | | |

- Limitations of the benchmark (China market uniqueness, regulatory differences, user behavior differences)
```

---

#### Task 4: Full Risk Panorama and Governance Assessment
- subject: `Assess full-spectrum risks and management/governance structure of {CompanyName}`
- activeForm: `Assess {CompanyName} risks and governance structure`
- description contains:

```
## Full Risk Panorama and Governance Assessment

### 1. Founder / CEO Deep Assessment

> "Buying a stock is buying a person." — Duan Yongping

- **Background and experience**: education, career history, entrepreneurial history
  - Any serial entrepreneur history? Outcome of previous ventures?
  - Years of industry-relevant experience
  - Largest team/business scale previously managed
- **Strategic vision**: search for the CEO's public statements over the past 3 years (speeches, interviews, internal memos, social media)
  | Date | CEO's Judgment/Prediction | Actual Outcome | Accuracy |
  |------|--------------------------|----------------|---------|
  - Has the CEO made correct calls ahead of the market?
  - Has the CEO stayed cool when everyone else was bullish?
- **Execution**: have key milestones been met on schedule?
  | Commitment | Commitment Date | Occasion | Delivery Status | Assessment |
  |-----------|----------------|---------|----------------|-----------|
- **Character and values**:
  - Attitude toward users/employees/society (judge from specific events, not slogans)
  - Choices made when facing difficulty (how layoffs were handled, crisis management, tradeoffs at points of interest conflict)
  - Tradeoffs between short-term profit and long-term value
- **Controversy**: any negative record? (Search "CEO name + controversy/scandal/problem")
- **Rating**: ★1-5 (with detailed rationale)

### 2. Core Team Assessment
- Core executive team roster and backgrounds (CTO / CFO / COO / VP, etc.)
  | Name | Title | Background | Tenure | Prior Experience |
  |------|-------|-----------|--------|-----------------|
- Key talent flow analysis:
  - Senior executive departures in the past 2 years (who left? went where? why?)
  - Senior executive additions in the past 2 years (poached from where? what does this signal?)
  - Net talent inflow or outflow?
- Team complementarity: are founding team capabilities complementary? Any obvious gaps?
- Team culture signals:
  - Glassdoor / Maimai scores and trends (direction of change over past 12 months matters more than absolute value)
  - Employee recommendation rate (Would recommend to a friend)
  - CEO approval rating
  - Sentiment around overwork culture, organizational atmosphere
- Key-person dependency: what happens to the company if the CEO/CTO leaves?

### 3. Equity Structure and Governance

**Ownership structure**:
| Shareholder | Equity % | Voting Rights % | Type | Notes |
|-------------|---------|----------------|------|-------|

- Founder control structure: dual-class shares / concert parties / VIE structure
- Founder equity dilution trend (dilution per funding round)
- Employee stock plan: coverage, vesting conditions, IPO lock-up alignment

**Governance structure**:
- Board composition (independent director ratio, investor seats)
- Major decision-making mechanisms
- Potential conflicts of interest:
  - Related-party transactions (founder's other companies transacting with this company)
  - Business overlap/competition
  - Conflict between major shareholder interests and minority shareholder interests

### 4. Investor Lineup Deep Analysis

| Investor | Round | Amount | Estimated Stake | Type | Strategic Value | Exit Pressure |
|----------|-------|--------|----------------|------|----------------|--------------|

Analysis:
- Brand endorsement significance of lead institution (top-tier VC vs. unknown fund)
- Strategic synergy value of industrial capital (does it bring resources/channels?)
- Investor exit pressure assessment:
  - How much time remains on fund life?
  - Has secondary market selling of old shares occurred?
  - Are ratchet/guarantee clauses approaching expiration?
- Red flags in investor lineup:
  - Any investors with poor reputations?
  - Have early investors fully exited?
  - Follow-on participation in the most recent round (existing investors not following on = lack of conviction?)

### 5. Full-Spectrum Risk Register

| Risk Type | Specific Risk | Probability (H/M/L) | Impact (H/M/L) | Severity | Hedgeable | Monitoring Indicator |
|-----------|-------------|--------------------|--------------------|----------|-----------|---------------------|
| Regulatory Risk | Antitrust, data security, industry crackdown, license risk | | | | | |
| Competitive Risk | Big tech entry, new model disruption, price wars | | | | | |
| Technology Risk | Platform migration, AI disruption, technology pathway failure | | | | | |
| Talent Risk | Founder/core team departure | | | | | |
| Funding Risk | Cash crunch, down round, difficulty raising | | | | | |
| IPO Risk | Listing window, regulatory approval, market conditions | | | | | |
| Geopolitical Risk | US-China relations, cross-border data, sanctions | | | | | |
| Monetization Risk | Monetization below expectations, user backlash | | | | | |
| Governance Risk | Related-party transactions, opacity, investor conflicts | | | | | |
| Compliance Risk | Data privacy (GDPR / Personal Information Protection Law), content compliance | | | | | |
| Macro Risk | Economic cycle, interest rate environment, capital market conditions | | | | | |
| ESG Risk | Environmental / social / governance-related risks | | | | | |

### 6. Exit Path Analysis

| Exit Method | Likelihood (★1-5) | Expected Time Window | Expected Valuation Range | Key Prerequisites | Key Obstacles |
|-------------|------------------|--------------------|-----------------------|-------------------|--------------|
| A-Share IPO | | | | | |
| HK IPO | | | | | |
| US IPO | | | | | |
| M&A acquisition | | Who are potential buyers? | | | |
| Secondary market transfer | | Liquidity level? | | | |
| SPAC | | | | | |
| Remain private long-term | | | | | |

- Most likely exit path and rationale
- Exit timeline projection
- Expected return analysis under each exit path

### 7. Worst-Case Scenario Analysis (Munger-Style Inversion)

> "Invert, always invert." — Munger

- How is this company most likely to **fail**? List 3 specific failure pathways
- Probability assessment and trigger conditions for each failure pathway
- In the worst case, how much can investors recover? (Liquidation value analysis)
- Why would a smart person **not invest** in this company? (List at least 5 reasons)
- Which historically similar-stage/positioning companies have failed? Why?
- What signals indicate the thesis is broken and a stop-loss should be triggered?
```

---

#### Task 5: Technology Capability and Intellectual Property Analysis
- subject: `Analyze {CompanyName} tech stack, patent portfolio, and R&D capability`
- activeForm: `Analyze {CompanyName} technology capability and intellectual property`
- description contains:

```
## Technology Capability and Intellectual Property Deep Analysis

> For technology companies, the authenticity and durability of the technology moat directly determines whether the valuation is justified.

### 1. Tech Stack Analysis
- Core technology architecture inference (from job postings, tech blogs, open-source projects, conference talks)
- Whether the tech stack selection is reasonable (are the right tools being used for the right problems?)
- Technical debt signals:
  - Are job postings heavily recruiting "refactoring/migration" roles?
  - Is a large-scale tech stack migration underway?
  - Are there frequent bug/outage complaints on the user side?

### 2. Patent Portfolio Analysis
Search patent databases (Google Patents, CNIPA, USPTO):

| Patent Metric | Data | Source |
|--------------|------|--------|
| Total patents (granted) | | |
| Patents pending | | |
| New patents added in past 2 years | | |
| Core technology domain distribution | | |
| Citation count of key patents | | |
| International patent coverage | | |

- Patent quality assessment (not just quantity):
  - Are there core/foundational patents?
  - Do patent-covered technology domains align with core business?
  - Are there patent litigation cases (as defendant or plaintiff)?
- Patent trends: is filing speed accelerating or slowing? Any technology direction shifts?
- Patent comparison with competitors

### 3. R&D Capability Assessment
- **R&D investment**:
  - R&D headcount and share (estimated from job platforms, LinkedIn)
  - R&D expense estimate (headcount × average compensation + infrastructure)
  - R&D expense ratio (vs. industry peers)
  - R&D investment trend: growing or shrinking?
- **R&D output**:
  - Academic paper publications (search Google Scholar, arXiv)
  - Technical conference presentations (search KDD, NeurIPS, SIGIR, and other top venues)
  - Open source contributions (search GitHub organization accounts)
  - Technical blog / public account output
- **R&D efficiency**:
  - Speed from R&D to product deployment
  - Commercialization rate of technical outputs

### 4. Technical Talent Assessment
- **Core technology leaders**: CTO / VP Eng / Chief Scientist background and capabilities
  | Name | Title | Education | Previous Company | Technical Influence |
  |------|-------|-----------|-----------------|-------------------|
- **Technical talent density**:
  - Which companies/labs do they come from? (Share of Google / Meta / MSRA / BAT and other top institutions)
  - Technical position salary competitiveness (estimated from job postings)
  - Technical team attrition signals (departure activity on LinkedIn)
- **Hiring signals**:
  - What technical roles are currently being recruited? (Reflects technology strategy direction)
  - Difficulty and fill speed of technical positions
  - Is a new technical team/lab being established?

### 5. Technology Moat Assessment

| Technology Barrier Dimension | Score (★1-5) | Evidence | Durability |
|-----------------------------|-------------|---------|-----------|
| Algorithm / Model Barrier | | Is there a proprietary algorithm? Can it be replicated? | |
| Data Moat | | Data scale, proprietary data, data flywheel speed | |
| Engineering Barrier | | System complexity, long-accumulated engineering capability | |
| Talent Barrier | | Are core technical personnel irreplaceable? | |
| Ecosystem Barrier | | Developer ecosystem, API/SDK coverage, technology standards | |

- Overall technology moat rating: Strong / Moderate / Weak
- Technology moat decay rate assessment (in the AI era, technology barriers may have a short half-life)

### 6. AI / New Technology Impact Assessment
- Company's AI capabilities and positioning
- Impact of AI on the company's core business (augmentation vs. threat vs. neutral)
- Is the company a beneficiary or a disruption target of the AI revolution?
- Impact assessment of other emerging technologies (Web3 / AR / VR / quantum computing, etc.)

### 7. Technology Risk Register
| Risk | Specific Description | Probability | Impact |
|------|---------------------|-------------|--------|
| Technology pathway failure | The bet on a technology direction is proven wrong | | |
| Open-source substitution | Core technology replaced by open-source solutions | | |
| Platform dependency | Dependency on a specific cloud / chip / OS | | |
| Security vulnerability | Data breach / system attack | | |
| Talent departure | Core technical personnel leaving | | |
```

---

#### Task 6: Alternative Data Signal Mining
- subject: `Mine unconventional data signals and hidden clues for {CompanyName}`
- activeForm: `Mine {CompanyName} alternative data signals`
- description contains:

```
## Alternative Data Signal Mining

> Private company conventional information is limited; alternative data often provides more authentic operating signals than news coverage.
> The goal of this task: beyond conventional sources, mine every potentially useful clue.

### 1. Hiring Signal Analysis
Search LinkedIn, Boss Zhipin, Maimai, Indeed, Glassdoor for job postings:

**Hiring scale and trend**:
- Total current open positions
- Hiring trend over the past 6 months (accelerating / stable / contracting)
- Hiring scale comparison with competitors

**Hiring composition analysis**:
| Job Category | Count | Share | Signal Interpretation |
|-------------|-------|-------|-----------------------|
| R&D / Engineering | | | Technology direction |
| Product | | | Product strategy |
| Sales / BD | | | Monetization stage |
| Marketing / Operations | | | Growth strategy |
| Data / AI | | | AI positioning |
| International | | | Overseas expansion plan |
| Compliance / Legal | | | Regulatory response / IPO preparation |
| Finance / IR | | | IPO preparation signal |

**Key signal capture**:
- Recruiting IR (Investor Relations) = IPO signal
- Recruiting Compliance / Data Security = regulatory pressure or IPO preparation
- Recruiting overseas roles = internationalization positioning
- Salary range of senior roles = company financial strength and talent competitiveness
- Technology stack / business directions mentioned in JDs = strategic direction

### 2. App / Product Data Analysis
Search App Store, Google Play, Qimai Data, SimilarWeb:

| Metric | Data | Source | Trend |
|--------|------|--------|-------|
| App Store ranking | | | Past 6 months trend |
| User rating | | | Direction of change |
| Number of ratings | | | Growth rate |
| Download volume estimate | | | |
| App update frequency | | | |
| Major features in recent updates | | | |

- High-frequency keywords and sentiment analysis from App Store reviews
- Main focal points of recent negative reviews (bugs? pricing? degraded experience?)
- Web traffic data (SimilarWeb): UV, PV, session duration, bounce rate

### 3. Social Media and Sentiment Signals
Search Weibo, Zhihu, Xiaohongshu, Twitter/X, Reddit:

- Interaction data on company official accounts (follower/retweet/comment trends)
- Intensity and sentiment of organic user discussions (positive/negative/neutral)
- Evaluations of the company by industry KOLs and influencers
- Sentiment hotspot events in the past 3 months
- Negative sentiment register and company response methods
- Any insider disclosures (ex-employees / current employees)

### 4. Corporate Registration and Legal Signals
Search Tianyancha / Qichacha / Qixinbao:

**Registration information**:
- Registered capital and change history
- Paid-in capital
- Shareholder / equity change records
- Subsidiary / affiliated company list (new = new business? dissolved = business contraction?)
- Business scope changes (newly added scope = new business direction)

**Legal information**:
| Type | Count | Key Case Summary |
|------|-------|-----------------|
| Litigation as plaintiff | | |
| Litigation as defendant | | |
| IP disputes | | |
| Labor arbitration | | |
| Administrative penalties | | |
| Enforcement records | | |

- Details and potential financial impact of major litigation/arbitration
- Administrative penalty records (environmental / tax / labor / data security, etc.)

### 5. Supply Chain and Partner Signals
- Known core suppliers/partner list
- Are suppliers publicly listed? Does their financial reporting mention cooperation data with this company?
- Tender/procurement information (government procurement portals, enterprise bidding platforms)
- Partner evaluations and depth of cooperation

### 6. Domain and Digital Footprint
Search domain/subdomain information:
- List of registered domains (newly registered domains may hint at new businesses/products)
- Subdomain analysis (api.xx.com, pay.xx.com, etc. hint at business architecture)
- SSL certificate information
- Trademark registrations (new trademark filings = new brand/product line)

### 7. Industry Conference and Exposure Signals
- Conference speeches/attendance records of company executives in the past 12 months
- Industry awards/media rankings (on "unicorn list", "most innovative", etc.?)
- Government/industry association engagement (policy consultation, standard-setting participation)
- Trends in media coverage frequency and quality

### 8. Secondary Market Transaction Signals (if any)
- Existence of secondary trading platforms (SharesPost, EquityZen, WeChat groups, etc.)
- Implied valuation from secondary trading vs. most recent funding round valuation
- Supply/demand balance between buyers and sellers
- Volume of employees selling options/RSUs

### 9. Composite Signal Scoring

| Signal Category | Direction (Positive/Negative/Neutral) | Strength (Strong/Medium/Weak) | Confidence | Key Finding |
|----------------|--------------------------------------|------------------------------|------------|------------|
| Hiring signals | | | | |
| Product data | | | | |
| Sentiment signals | | | | |
| Legal signals | | | | |
| Supply chain signals | | | | |
| Digital footprint | | | | |
| Industry exposure | | | | |
| Secondary trading | | | | |

**Combined signal direction**: Do all signals point the same way? Are there contradictory signals?

### 10. Anomalous Signal Register (Most Important)
List all "unusual" findings — these are often the most valuable information:
- Signals inconsistent with the company's public narrative
- Data that contradicts industry conventional wisdom
- Sudden changes (rapid hiring contraction/expansion, cluster of executive departures, etc.)
- Unexplained phenomena
```

---

### Step 4: Launch 6 Parallel Agents

Use the Agent tool to simultaneously launch 6 agents (**must be called in parallel within the same message**):

Each agent configuration:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`

Prompt template for each agent:

```
You are the "{role name}" in the private company research team for {CompanyName}.

You are researching a **private company**, which means:
- No standardized public financial reports; information must be pieced together from multiple sources
- Data may be incomplete or contradictory; confidence levels must be labeled
- More reasoning and reasonable estimation is required, but the estimation process must be shown transparently
- Not finding information ≠ the information doesn't exist; found information may be biased

Please complete the following research task: {task subject}

Specific requirements:
{content of task description}

**Research method**:
1. Use WebSearch to find the latest public information; search each dimension at least 3–5 times with different keyword combinations
2. Keyword search strategy:
   - Chinese: company name + revenue/valuation/funding/user count/MAU/IPO/prospectus/layoffs/rectification
   - English: Company Name + revenue/valuation/funding/users/IPO/filing
   - Specific person name + company name (for management-related information)
   - Company name + specific competitor name (for competitive dynamics)
3. Priority sources:
   - High credibility: prospectuses, regulatory filings, related-party disclosures in listed company annual reports
   - Medium credibility: LatePost, The Information, 36Kr, Bloomberg, Reuters, TechCrunch
   - Supporting validation: Zhihu, Maimai, Glassdoor, Tianyancha, Qichacha
4. Use WebFetch to retrieve the full text of key articles (don't rely only on search snippets)
5. For important data, cross-validate with at least 2 different sources

**Data labeling standards (strictly enforced)**:
- Label each key data point's source (specific outlet name and article title)
- Label the data date (precise to year and month)
- Label confidence: 🟢High (prospectus/official disclosure) / 🟡Medium (credible media/research report) / 🔴Low (estimate/rumor)
- When data from different sources conflicts, **list all** and explain the discrepancy and your judgment
- Distinguish "facts" from "reasoning": facts in regular text, reasoning/estimates in *italics* with the estimation method noted
- Clearly label "data unavailable" for missing information; do not fabricate

**Output requirements**:
- Report should be comprehensive; use Markdown tables to present key data
- Each analytical dimension should have a clear conclusion and score
- All estimation processes must be fully transparent (show calculation logic and each assumption)
- At the end of the report, provide:
  1. Overall score (★1-5) and core judgment for this dimension
  2. Self-assessment of information completeness for this dimension (Adequate/Moderate/Insufficient/Severely Insufficient)
  3. The 3 most important findings
  4. The biggest information blind spot (what missing information most impairs the judgment)
```

### Step 5: Receive Reports and Track Progress

- Show the user a real-time progress table (which agents have completed, which are still researching)
- Upon receiving each report, update progress and display the core findings from that report (3–5 points)
- Wait for all 6 reports to arrive

### Step 6: Cross-Validation and Information Integration

**This is the most critical new step in the enhanced framework.** Before synthesizing, the team-lead must:

1. **Data conflict arbitration**:
   - Extract key data from each agent's report
   - Identify whether the same data cited by different agents is consistent
   - Arbitrate conflicting data: list all sources, state which is adopted and why

2. **Signal consistency check**:
   - Business growth signals (business-decoder) vs. hiring signals (signal-miner) — consistent?
     (If rapid business growth is claimed but hiring is contracting, an explanation is needed)
   - Technology leadership narrative (tech-ip) vs. patent/talent data (signal-miner) — supported?
   - Valuation level (financial-detective) vs. competitive position (competitive-mapper) — matched?
   - Management public narrative (risk-governance) vs. actual action signals (signal-miner) — consistent?

3. **Information puzzle integration**:
   - Combine information fragments from all 6 reports to see if a more complete picture can be reconstructed
   - Label information as "white zone" (confirmed known), "gray zone" (clues but uncertain), "black zone" (completely unknown)

4. **Anti-bias check**:
   - Check whether reports exhibit "positive information detailed, negative information brief" bias
   - Confirm every positive judgment has a corresponding counter-check

### Step 7: Synthesize the Final Report

Consolidate 6 analytical reports into a final report with the following structure:

---

#### 1. One-Sentence Conclusion
> Summarize in one paragraph (50–100 words) the **true value judgment** of this private company: what the business is worth and why.

#### 2. Company Profile Snapshot
| Item | Content | Confidence |
|------|---------|-----------|
| Company name | | |
| Founded | | |
| Headquarters | | |
| Founder / CEO | | |
| Core business | | |
| Headcount | | |
| Latest valuation | | |
| Latest funding round | | |
| Estimated revenue scale | | |
| Estimated profit status | | |
| Estimated user scale | | |
| Key investors | | |
| VIE / Red-chip structure | | |

#### 3. Six-Dimension Scoring Summary
| Dimension | Analyst | Score (★1-5) | Core Judgment | Confidence | Information Completeness |
|-----------|---------|-------------|--------------|------------|------------------------|
| Business Model & Users | business-decoder | | | | |
| Financials & Valuation | financial-detective | | | | |
| Industry & Competition | competitive-mapper | | | | |
| Risk & Governance | risk-governance-analyst | | | | |
| Technology & IP | tech-ip-analyst | | | | |
| Alternative Data Signals | signal-miner | | | | |

Overall score: ★X / 5

#### 4. Key Data Puzzle (Post Cross-Validation)
Consolidate data pieced together by all analysts; **retain only cross-validated data**:

| Metric | Data | Source Count | Source Details | Confidence | Notes |
|--------|------|-------------|---------------|-----------|-------|

#### 5. Signal Consistency Matrix
| Check Item | Signal A | Signal B | Consistency | Interpretation |
|-----------|---------|---------|------------|---------------|
| Growth narrative vs. hiring trend | | | ✅/⚠️/❌ | |
| Technology leadership narrative vs. patent data | | | | |
| Valuation level vs. competitive position | | | | |
| Management narrative vs. actual actions | | | | |

#### 6. Dimension-by-Dimension Analysis Summary
Extract 3–5 most important findings per dimension (with source and confidence label)

#### 7. True Value Assessment

**Business essence judgment**:
- What kind of business is this? (One sentence)
- How high is the "certainty" of this business?
- Duan Yongping-style judgment: is this a "right business"?

**Moat Scorecard**:
| Moat Type | Score (★1-5) | Core Evidence | Trend | Durability |
|-----------|-------------|--------------|-------|-----------|
| Network Effects | | | Widening/Stable/Narrowing | |
| Switching Costs | | | | |
| Brand Mindshare | | | | |
| Data Moat | | | | |
| Regulatory Licenses | | | | |
| Scale Economies | | | | |
| Technology Barrier | | | | |

**Valuation Judgment**:
| Valuation Method | Valuation Range | Confidence | Notes |
|-----------------|----------------|------------|-------|
| Latest funding round valuation (adjusted) | | | |
| Comparable company method | | | |
| DCF scenario analysis | | | |
| Terminal market cap reverse engineering | | | |
| Transaction comparable method | | | |

**Composite True Value Range**:
- Conservative valuation (margin of safety valuation): $XXB
- Fair valuation (neutral assumptions): $XXB
- Optimistic valuation (best-case scenario): $XXB
- Current market valuation: $XXB
- **Margin of safety**: current valuation vs. conservative valuation = XX%

#### 8. Investment Thesis (Bull vs. Bear)
- 🟢 Bull case (5–7 points, each with supporting source)
- 🔴 Bear case (5–7 points, each with supporting source)
- ⚖️ Which side has more persuasive evidence? Why?

#### 9. Risk Matrix
| Risk | Probability | Impact | Combined Severity | Hedgeable | Monitoring Indicator |
|------|-------------|--------|------------------|-----------|---------------------|

Top 3 core risks and mitigation strategies

#### 10. Exit Path Assessment
Most likely exit method, time window, expected return

#### 11. Investment Decision Table

**One-page decision table**:
```
┌──────────────────────────────────────────────┐
│  Company: XXX    Latest Valuation: $XXB       │
│  Stage: [Seed / Growth / Mature / Pre-IPO]   │
│  Information Completeness: [Adequate / Moderate / Insufficient / Severely Insufficient] │
├──────────────────────────────────────────────┤
│  Core Investment Thesis (3 sentences max):    │
│  1. ________________________________________  │
│  2. ________________________________________  │
│  3. ________________________________________  │
├──────────────────────────────────────────────┤
│  True Value Judgment:                         │
│  Fair Valuation Range: $XXB - $XXB            │
│  Current Valuation vs. Fair Value: Expensive / Fair / Cheap │
│  Margin of Safety: ____%                      │
├──────────────────────────────────────────────┤
│  Key Assumptions & Validation:                │
│  Assumption 1 → Tracking metric → Validation node → Validation date │
│  Assumption 2 → Tracking metric → Validation node → Validation date │
│  Assumption 3 → Tracking metric → Validation node → Validation date │
├──────────────────────────────────────────────┤
│  Fatal Risks & "Thesis Broken" Signals:       │
│  Risk 1 → If X occurs, conclusion flips → stop-loss strategy │
│  Risk 2 → If Y occurs, conclusion flips → stop-loss strategy │
├──────────────────────────────────────────────┤
│  Conclusion: Invest / Watch / Avoid           │
│  If watching: what trigger condition for re-evaluation? │
│  Expected exit: IPO / M&A / Secondary transfer │
│  Expected return multiple: X - Y times        │
│  Expected time horizon: X - Y years           │
│  Annualized return: X% - Y%                   │
└──────────────────────────────────────────────┘
```

**Tiered Recommendations**:
| Investor Type | Recommendation | Rationale |
|--------------|---------------|---------|
| PE/VC institution (lead investor) | | |
| PE/VC institution (co-investor) | | |
| Secondary market transfer | | |
| Post-IPO purchase | | |
| Not recommended | | |

**Key Catalysts**:
| Bull Catalyst | Expected Timing | Bear Catalyst | Expected Timing |
|--------------|----------------|--------------|----------------|
| | | | |

#### 12. Information Blind Spot Map
| Dimension | Known Information | Missing Information | Impact of Gap | Acquisition Suggestion |
|-----------|-----------------|-------------------|--------------|----------------------|

Do these information blind spots affect the reliability of the core conclusions? If so, explicitly state: "With X information missing, the confidence level of the above conclusions is Y."

#### 13. Ongoing Tracking Checklist
| Tracking Item | Frequency | Information Source | Key Metric | Alert Threshold |
|--------------|-----------|------------------|-----------|----------------|

#### 14. Summary Paragraph
150–250 word final summary covering:
- The essence of this business
- True value judgment
- Reasonableness of the current valuation
- Greatest certainties and uncertainties
- Final recommendation and core rationale

---

### Step 8: Save the Report

Write the complete final report to `reports/{CompanyName}/{CompanyName}-private-{YYYYMMDD}.md`.

### Step 9: Clean Up the Team

Use TeamDelete to clean up team resources.

---

## Important Notes

1. **6 agents must be launched in parallel** — call the Agent tool 6 times within the same message
2. **Data confidence labeling** — private company data sources vary widely in quality; every key data point must carry source and confidence labels
3. **Transparent estimation** — all estimation processes must show calculation logic; numbers cannot appear out of thin air
4. **Cross-validation** — key data must be validated with at least 2 sources; when sources conflict, list all of them
5. **Signal consistency check** — the synthesis stage must perform cross-dimension signal consistency verification
6. **Clear conclusions** — do not avoid giving an Invest/Watch/Avoid recommendation, but always state the confidence level of the conclusion
7. **Patient waiting** — 6 agents need several minutes to research; provide the user with real-time progress updates
8. **Bilingual search** — private company information may be distributed across Chinese and English media; both languages must be searched
9. **Anti-bias core principle** — thin sources ≠ bad company; short AI analysis ≠ low investment certainty. For companies with extremely scarce information, switch to "first-principles mode" focused on core questions rather than pursuing formal report completeness
10. **Honest blank spaces** — clearly distinguish "evidence-based analysis" from "speculative fill-in" in the report; it is acceptable to state "data for this dimension is insufficient to draw a meaningful conclusion"
11. **Alternative data is not noise** — hiring, patents, litigation, app data, and similar alternative data may be closer to true operating conditions than news coverage
12. **True value orientation** — the ultimate goal is to judge what this business is worth, not to produce a polished report. If information is insufficient for a reliable valuation judgment, say directly: "Insufficient information; a reliable valuation cannot be provided"
