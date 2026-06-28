# Investment Research Team: Four-Role Parallel Analysis Framework

Conduct a team-based investment research analysis on $ARGUMENTS. Use the Team tool to create a true multi-agent parallel research team.

## Execution Flow

### Step 1: Present the Team Framework

Present the following team structure to the user and confirm before launching:

| Role | Responsibility | Analysis Framework |
|------|---------------|-------------------|
| **team-lead** (yourself) | Coordination, synthesis, final report output | Four Masters integrated framework |
| **business-analyst** | Business model & economic moat analysis | Duan Yongping perspective |
| **financial-analyst** | Financial statements & valuation analysis | Buffett perspective |
| **industry-researcher** | Industry landscape & competitive dynamics | Munger perspective |
| **risk-assessor** | Risk assessment & management evaluation | Li Lu perspective |

### Step 1.5: AI Research Bias Assessment

Before creating the team, present the "AI Researchability" assessment for this company to the user:

**Information Richness Rating** (determines research strategy):
| Rating | Characteristics | Research Strategy Adjustment |
|--------|----------------|------------------------------|
| A-Grade (Information-rich) | Listed for many years, broad analyst coverage | Team focuses on **counter-verification** and **non-consensus perspectives** — avoid outputting "correct but meaningless" analysis that merely echoes market consensus |
| B-Grade (Moderate information) | Recently listed, limited coverage | Each Agent's estimated data must be labeled with confidence levels; team-lead summary must include "data sufficiency" notation |
| C-Grade (Information-scarce) | Obscure / newly listed / emerging market | Team switches to "first-principles mode": do not pursue report completeness — focus on a few core questions about the business fundamentals |

**Key reminder**: More data ≠ higher certainty; less data ≠ lower certainty. AI's confidence level ≠ actual investment certainty. Certainty comes from the business model itself, not from the volume of available information.

Communicate the rating to each Agent so it influences their research approach.

### Step 2: Create the Team

Use TeamCreate to create the team:
- team_name: `{company-name}-research` (lowercase English, e.g., `meituan-research`)
- agent_type: `team-lead`

### Step 3: Create 4 Tasks

Use TaskCreate to create the following 4 tasks (each must include subject, description, and activeForm):

#### Task 1: Business Model Analysis
- subject: `Analyze {company name} business model, economic moat, and user value`
- description includes:
  1. Business model fundamentals: core business definition, revenue breakdown
  2. How the platform/product flywheel operates
  3. Economic moat analysis: brand / switching costs / network effects / scale effects / technology barriers — verify each individually
  4. User/customer value: what unique value is created for each stakeholder
  5. Business portfolio and synergies
  6. Duan Yongping "good business" criteria assessment: differentiation, pricing power, sustainable competitive advantage
  7. Must search for the latest earnings reports, industry research, and other public information

#### Task 2: Financial & Valuation Analysis
- subject: `Analyze {company name} financial data, profitability, and valuation`
- description includes:
  1. Revenue, net income, and operating profit trends over the past 3–5 years
  2. Profitability metrics: ROE, ROA, gross margin, operating margin
  3. Cash flow analysis: operating cash flow, free cash flow, capital expenditure (CapEx)
  4. Balance sheet health: cash reserves, debt ratio, liquidity
  5. Valuation analysis: PE/PS/PB/EV, compared with historical and peer benchmarks
  6. Margin of safety assessment: intrinsic value vs. current share price
  7. **Financial rigor verification (must use Bash to call tools — mental math is prohibited)**:
     - Market cap verification: `python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap --price {price} --shares {shares} --reported {reported market cap} --currency {currency}`
     - Valuation verification: `python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation --price {price} --eps {EPS} --bvps {book value per share}`
     - Key data cross-validation: `python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate --field {field} --values '{JSON}' --unit {unit}`
     - Three-scenario valuation: `python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario --price {price} --eps {EPS} --shares {shares in 100M} --growth {bull} {base} {bear} --pe {bull PE} {base PE} {bear PE}`
     - Embed tool output directly into the report as verification records

#### Task 3: Industry & Competitive Analysis
- subject: `Analyze {industry} industry landscape and {company name} competitive position`
- description includes:
  1. Industry size and growth: market size, growth rate, penetration rate
  2. Competitive landscape: major competitors' market share, competitive strategy comparison
  3. Key competitor threat assessment: analyze each major competitor individually
  4. Sub-segment landscape breakdown
  5. Industry trends: technological shifts, policy impact, new entrants
  6. Value chain analysis: value distribution across upstream, midstream, and downstream
  7. Must search for the latest industry data and competitive developments

#### Task 4: Risk & Management Assessment
- subject: `Assess {company name} investment risks and management quality`
- description includes:
  1. Management assessment: CEO competency circle, integrity, strategic vision, capital allocation ability, quality of historical decisions
  2. Regulatory risk: current and potential regulatory impact
  3. Competitive risk: threat level assessment for each major competitor
  4. Business risk: losses from new business lines, expansion uncertainty
  5. Macro risk: economic cycle and industry cycle impact
  6. Governance structure: ownership structure, related-party transactions, shareholder return policy
  7. Long-term certainty: what will the company look like in 10 years? What could disrupt its business model?
  8. Must search for the latest regulatory developments and management commentary

### Step 4: Launch 4 Parallel Agents

Use the Task tool to launch all 4 Agents simultaneously (**must be called in parallel within the same message**):

Configuration for each Agent:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`
- `team_name`: corresponding team name
- `name`: corresponding role name (business-analyst / financial-analyst / industry-researcher / risk-assessor)

Prompt template for each Agent:

```
You are the "{role name}" on the {company name} investment research team, responsible for analyzing {company name} from the {master name} investment perspective.

Please complete Task #{task number}: {task subject}

Specific requirements:
{task description content}

**Research methodology**:
- Use WebSearch to find the latest publicly available information (earnings reports, industry research, news)
- **Financial data must come from two independent sources**, following the `skills/financial-data.md` specification (US stocks: macrotrends + stockanalysis; HK stocks: aastocks + macrotrends; A-shares: Eastmoney + CNINFO) — discrepancies >1% between sources must be flagged
- Ensure data accuracy; annotate sources for all key data points
- Analysis must be deep and substantive, not superficial

**Output requirements**:
- Report must be comprehensive; present key data in Markdown tables
- Each analytical dimension must include a clear conclusion and rating
- End the report with an overall conclusion for that dimension

**Upon completion**:
1. Use TaskUpdate to mark Task #{task number} as completed
2. Send the complete analysis report to team-lead via SendMessage (type: "message", recipient: "team-lead")
```

### Step 5: Receive Reports and Track Progress

- Show the user a real-time progress table (which Agents have completed, which are still researching)
- Each time a report is received, update progress and display the key findings from that report (3–5 points)
- Wait until all 4 reports have been received

### Step 6: Shut Down Team Members

Once all reports are received, send a shutdown_request to all 4 Agents (using SendMessage, type: "shutdown_request").

### Step 7: Synthesize the Final Report

Consolidate all 4 analysis reports and output a final report with the following structure:

---

#### 1. One-Sentence Conclusion
> A single paragraph (50–100 words) summarizing whether the company is worth investing in and the core rationale

#### 2. Four-Dimension Scoring Summary Table
| Dimension | Framework | Rating (1–5 stars) | Core Judgment |
|-----------|-----------|-------------------|---------------|

Overall Score: X / 5

#### 3. Key Data Snapshot
Table of key financial and operating metrics (last 2 years comparison)

#### 4. Per-Dimension Analysis Highlights
Extract the 3–5 most important findings from each dimension

#### 5. Investment Thesis (Bull vs Bear)
- 🟢 Bull case (5–7 points)
- 🔴 Bear case (5–7 points)

#### 6. Buffett Pre-Buy Checklist
| # | Checklist Item | Pass? | Notes |
10 core checklist items, assessed individually

#### 7. Final Investment Recommendation
- Qualitative judgment table (business quality / management / valuation / timing)
- Tiered action recommendation table (Aggressive / Balanced / Conservative → recommendation + price range)
- Key catalysts (3–5 signals each for adding to position and reducing position)

#### 8. Closing Summary
100–200 word final summary

---

### Step 8: Save the Report

Write the complete final report to `~/{company-name}-investment-research-report_{date}.md` (date format: YYYYMMDD).

### Step 9: Data Spot-Check (Quality Gate)

```bash
# Step 1 — Extract spot-check list (15% random sampling)
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report file path>

# Step 2 — For each item on the list, retrieve data from reliable sources (see skills/financial-data.md)

# Step 3 — Output pass/reject verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report <report filename>
```

**[PASS]** All items pass → report is cleared for publication; **[REJECT]** Any item fails → correct and re-audit.

### Step 10: Clean Up the Team

Use TeamDelete to clean up team resources.

## Important Notes

1. **All 4 Agents must be launched in parallel** — call the Task tool 4 times within the same message
2. **Agents report via SendMessage** — this is message-based communication, not file collaboration
3. **Data accuracy** — require Agents to use WebSearch for the latest data; cross-validate all key data points
4. **Conclusions must be definitive** — do not avoid giving buy / hold / avoid recommendations with specific price ranges
5. **All analysis must be data-backed** — include data sources
6. **Be patient** — 4 Agents conducting research takes several minutes; keep the user updated on progress in real time
7. **Anti-bias awareness** — when synthesizing, team-lead must assess: is each Agent's analysis limited by information availability? Is it overly aligned with market consensus? The final report must include an "Information Richness Rating" and an "AI Research Limitations Disclaimer"
8. **Honesty principle when information is scarce** — it is better to leave sections blank and label them "insufficient data" than to fill a framework with speculation disguised as certainty
