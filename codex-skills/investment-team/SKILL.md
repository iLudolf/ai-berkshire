---
name: investment-team
description: "AI Berkshire skill: Investment Research Team: Four-Role Parallel Analysis Framework. Source: skills/investment-team.md."
---

## Codex adapter note

This skill is generated from `skills/investment-team.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Investment Research Team: Four-Role Parallel Analysis Framework

Conduct a team-based investment research analysis on $ARGUMENTS. Use the Team tool to create a true multi-Agent parallel research team.

## Execution Flow

### Step 1: Present the Team Framework

Show the user the following team structure and confirm before launching:

| Role | Responsibilities | Analysis Framework |
|------|------------------|--------------------|
| **team-lead** (yourself) | Coordination, synthesis, final report output | Four Masters integrated framework |
| **business-analyst** | Business model & economic moat analysis | Duan Yongping perspective |
| **financial-analyst** | Financial statements & valuation analysis | Buffett perspective |
| **industry-researcher** | Industry landscape & competitive dynamics | Munger perspective |
| **risk-assessor** | Risk assessment & management evaluation | Li Lu perspective |

### Step 1.5: AI Research Bias Assessment

Before creating the team, present the "AI Researchability" assessment for this company:

**Information Richness Rating** (determines research strategy):
| Grade | Characteristics | Research Strategy Adjustment |
|-------|-----------------|------------------------------|
| Grade A (Information Rich) | Listed for many years, broad analyst coverage | Team should focus on **counter-validation** and **non-consensus perspectives** — avoid producing consensus-aligned "correct but useless" output |
| Grade B (Information Moderate) | Recently listed, limited coverage | Each Agent's estimated data must include a confidence level; team-lead summary must note "data sufficiency" |
| Grade C (Information Scarce) | Obscure / newly listed / emerging market | Team switches to "first-principles mode": do not pursue report completeness — focus on a few core questions about business fundamentals |

**Key reminder**: More data ≠ higher certainty; less data ≠ lower certainty. The confidence AI can output ≠ true investment certainty. Certainty comes from the business model itself, not from the volume of available information.

Communicate the rating to each Agent so it shapes their research approach.

### Step 2: Create the Team

Use TeamCreate to create the team:
- team_name: `{company-name}-research` (lowercase English, e.g. `meituan-research`)
- agent_type: `team-lead`

### Step 3: Create 4 Tasks

Use TaskCreate to create the following 4 tasks (each must have a subject, description, and activeForm):

#### Task 1: Business Model Analysis
- subject: `Analyze {Company Name} business model, economic moat, and user value`
- description includes:
  1. Business model fundamentals: core business definition, revenue structure breakdown
  2. How the platform/product flywheel operates
  3. Moat analysis: brand / switching costs / network effects / economies of scale / technology barriers — verify each individually
  4. User/customer value: what unique value is created for each stakeholder
  5. Business portfolio and synergies
  6. Duan Yongping "good business" standard assessment: differentiation, pricing power, sustainable competitive advantage
  7. Search for latest earnings reports, industry reports, and other public information

#### Task 2: Financial and Valuation Analysis
- subject: `Analyze {Company Name} financial data, profitability, and valuation`
- description includes:
  1. Revenue, net income, and operating profit trends over the past 3–5 years
  2. Profitability metrics: ROE, ROA, gross margin, operating margin
  3. Cash flow analysis: operating cash flow, free cash flow, capital expenditure
  4. Balance sheet health: cash reserves, leverage ratio, liquidity
  5. Valuation analysis: PE/PS/PB/EV and others, compared with historical and peer benchmarks
  6. Margin of safety assessment: intrinsic value vs. current share price
  7. **Financial rigor verification (must use Bash tool calls — mental math is prohibited)**:
     - Market cap verification: `python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap --price {price} --shares {shares} --reported {reported market cap} --currency {currency}`
     - Valuation verification: `python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation --price {price} --eps {EPS} --bvps {book value per share}`
     - Key data cross-validation: `python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate --field {field} --values '{JSON}' --unit {unit}`
     - Three-scenario valuation: `python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario --price {price} --eps {EPS} --shares {shares in 100M} --growth {bull} {base} {bear} --pe {bull PE} {base PE} {bear PE}`
     - Embed tool output directly in the report as a verification record

#### Task 3: Industry and Competitive Analysis
- subject: `Analyze {Industry} industry landscape and {Company Name} competitive positioning`
- description includes:
  1. Industry size and growth: market size, growth rate, penetration rate
  2. Competitive landscape: major competitors' market share, competitive strategy comparison
  3. Key competitor threat assessment: analyze each major competitor individually
  4. Sub-segment landscape breakdown
  5. Industry trends: technological change, regulatory impact, new entrants
  6. Industry chain analysis: value distribution across upstream, midstream, and downstream
  7. Search for the latest industry data and competitive dynamics

#### Task 4: Risk and Management Assessment
- subject: `Assess {Company Name} investment risks and management quality`
- description includes:
  1. Management assessment: CEO's circle of competence, integrity, strategic vision, capital allocation ability, historical decision quality
  2. Regulatory risk: current and potential regulatory impact
  3. Competitive risk: threat level assessment for each competitor
  4. Business risk: new business losses, expansion uncertainty
  5. Macro risk: economic cycle and industry cycle impact
  6. Governance structure: ownership structure, related-party transactions, shareholder return policy
  7. Long-term certainty: what will this company look like in 10 years? What could disrupt its business model?
  8. Search for latest regulatory developments, management statements, etc.

### Step 4: Launch 4 Parallel Agents

Use the Task tool to launch all 4 Agents simultaneously (**must be called in parallel within the same message**):

Configuration for each Agent:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`
- `team_name`: corresponding team name
- `name`: corresponding role name (business-analyst / financial-analyst / industry-researcher / risk-assessor)

Prompt template for each Agent:

```
You are the "{role name}" in the {Company Name} investment research team, responsible for analyzing {Company Name} from the {Master Name} investment perspective.

Please complete Task #{task number}: {task subject}

Specific requirements:
{task description content}

**Research methodology**:
- Use WebSearch to find the latest public information (earnings reports, industry reports, news)
- **Financial data must come from two independent sources**, following the `skills/financial-data.md` standards (US stocks: macrotrends + stockanalysis; HK stocks: aastocks + macrotrends; A-shares: East Money + CNINFO), discrepancies >1% between sources must be flagged
- Ensure data accuracy; cite sources for all key data points
- Analysis must be deep — do not stay at the surface level

**Output requirements**:
- Reports should be thorough; use Markdown tables to present key data
- Each analysis dimension must have a clear conclusion and rating
- The report must end with an overall conclusion for that dimension

**Upon completion**:
1. Use TaskUpdate to mark Task #{task number} as completed
2. Send the full analysis report to team-lead via SendMessage (type: "message", recipient: "team-lead")
```

### Step 5: Receive Reports and Track Progress

- Show the user a real-time progress table (which Agents have finished, which are still researching)
- Each time a report is received, update progress and display the key takeaways from that report (3–5 points)
- Wait until all 4 reports have been received

### Step 6: Shut Down Team Members

Once all reports are received, send a shutdown_request to all 4 Agents (using SendMessage, type: "shutdown_request").

### Step 7: Synthesize the Final Report

Integrate all 4 analysis reports and produce a final report with the following structure:

---

#### 1. One-Sentence Conclusion
> Summarize in one paragraph (50–100 words) whether the company is worth investing in and the core investment logic

#### 2. Four-Dimension Scorecard
| Dimension | Framework | Score (1–5 stars) | Core Judgment |
|-----------|-----------|-------------------|---------------|

Composite Score: X / 5

#### 3. Key Data Snapshot
Key financial and operational metrics table (last 2 years comparison)

#### 4. Per-Dimension Analysis Summary
3–5 most important findings from each dimension

#### 5. Investment Thesis (Bull vs Bear)
- 🟢 Bull case (5–7 points)
- 🔴 Bear case (5–7 points)

#### 6. Buffett Pre-Buy Checklist
| # | Check Item | Pass? | Notes |
10 core check items, evaluated one by one

#### 7. Final Investment Recommendation
- Qualitative judgment table (business quality / management / valuation / timing)
- Tiered action recommendation table (aggressive / balanced / conservative → recommendation + price range)
- Key catalysts (3–5 add signals / 3–5 trim signals)

#### 8. Closing Summary
100–200 word final summary

---

### Step 8: Save the Report

Write the complete final report to `~/{CompanyName}-investment-research-{date}.md` (date format YYYYMMDD).

### Step 9: Data Spot-Check (Release Gate)

```bash
# Step 1 — Extract spot-check list (15% random sample)
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report <report file path>

# Step 2 — For each item in the list, retrieve the value from a reliable source (see skills/financial-data.md)

# Step 3 — Output pass/fail verdict
python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report <report file name>
```

**[PASS]** All items verified → report is ready to publish; **[FAIL]** Any item fails → correct and re-audit.

### Step 10: Clean Up the Team

Use TeamDelete to release team resources.

## Important Notes

1. **All 4 Agents must be launched in parallel** — call the Task tool 4 times within the same message
2. **Agents report via SendMessage** — this is message-based communication, not file-based collaboration
3. **Data accuracy** — require Agents to use WebSearch for the latest data; cross-validate all key data points
4. **Conclusions must be definitive** — do not avoid giving buy/hold/avoid recommendations with specific price ranges
5. **All analysis must be supported by data** — include data sources
6. **Be patient** — 4 Agents researching in parallel takes several minutes; provide real-time progress updates to the user
7. **Anti-bias awareness** — when synthesizing, team-lead must assess: is each Agent's analysis constrained by data availability? Is it overly aligned with market consensus? The final report must include an "Information Richness Rating" and an "AI Research Limitations Disclaimer"
8. **Honesty when information is scarce** — it is better to leave a section blank and label it "insufficient data" than to fill the framework with speculation and fake certainty
