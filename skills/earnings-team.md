# Earnings Deep-Read Team: Four Masters Parallel Analysis + Investment Article Publication

Perform a team-based earnings deep-read analysis for $ARGUMENTS. Four masters analyze the earnings report in parallel, an editor polishes the draft into an article, a reader reviewer ensures quality, and the final output is an investment newsletter article ready for immediate publication.

**Supported input formats**: `Company Name Quarter`, for example: `WEGE3 2025Q4`, `VALE3 2025 Annual`, `ITUB4 Latest`

## Design Philosophy

A good earnings analysis must solve two problems:
1. **Seeing the future yourself** — requires deep research from four different perspectives
2. **Helping readers understand the value** — requires editorial polish and quality assurance from the reader's point of view

This Skill's workflow has three phases:
- **Phase 1 · Research**: Four masters read the earnings report in parallel (Duan Yongping examines the business essence, Buffett audits financial quality, Munger reads competitive shifts, Li Lu hunts for risk signals)
- **Phase 2 · Synthesis**: Team Lead consolidates the four perspectives and produces a research report draft
- **Phase 3 · Publication**: Editor Agent rewrites into an investment newsletter article + Reader Reviewer Agent provides feedback → Team Lead finalizes

---

## Phase 1: Four Masters Parallel Research

### Step 1: Gather Primary Sources

Use the Agent tool to launch background Agents **in parallel** to fetch the following raw materials:

| Source Type | Where to Obtain | Priority |
|-------------|----------------|----------|
| Earnings report (original) | Company RI (investor relations) page, CVM filings (DFP/ITR), B3 disclosures, SEC EDGAR (US-listed BDRs) | Highest |
| Earnings call transcript | Teleconferência de resultados (company RI page), Fundamentus, Status Invest | Highest |
| Letter to shareholders from management | Extract from annual report | High (annual reports only) |
| Prior period earnings report / call | Same as above | High (for commitment tracking) |

**Source Availability Rating**:

| Grade | Characteristics | Impact |
|-------|----------------|--------|
| Grade A | Full original document obtained | Execute all steps normally |
| Grade B | Only partial original or third-party summary obtained | Label as "non-primary source," reduce weight given to footnote analysis |
| Grade C | Only news coverage and data-site summaries available | Focus on core data changes, skip footnote mining, label "insufficient primary sources" |

Inform each Agent of the source availability rating, which will affect the depth of their analysis.

### Step 2: Present the Team Framework to the User

| Phase | Role | Master / Position | Core Task |
|-------|------|------------------|-----------|
| Research | **Team Lead** (you) | Overall coordinator | Coordinate, synthesize, finalize |
| Research | Business Essence Analyst | Duan Yongping | Has this business gotten better or worse? |
| Research | Financial Quality Auditor | Buffett | Is the money earned real or illusory? |
| Research | Competitive Landscape Analyst | Munger | How is the competitive landscape shifting? |
| Research | Risk Signal Hunter | Li Lu | What is management hiding? |
| Publication | Editor | Newsletter writing | Rewrite the research report into a compelling article |
| Publication | Reader Reviewer | Ordinary investor | Can readers understand it? Do they gain from it? |

### Step 3: Launch 4 Parallel Research Agents

Use the Agent tool to launch 4 background Agents **in the same message**.

---

#### Agent 1: Business Essence Analysis (Duan Yongping Perspective)

**Core question: Does this earnings report show the business has gotten better or worse?**

> Duan Yongping: "Investing is buying a business. Reading earnings reports is not about reading numbers — it's about seeing whether this business has changed."

Analysis content:

1. **Revenue structure breakdown and interpretation**
   - Revenue by business segment / by region: which are accelerating, which are decelerating
   - Not just listing numbers — what business logic does each segment reflect
   - Is revenue growth driven by "volume" or "price"? Which is healthier?

2. **User / customer value changes**
   - Changes in operating metrics such as DAU / MAU / paying users
   - Quality metrics such as user time spent, ARPU, retention rate
   - Is the platform / product delivering more or less value to users?

3. **Economic moat check**
   - Gross margin changes indicate whether pricing power remains intact
   - Market share changes indicate whether competitive barriers are holding
   - Signals of weakening customer switching costs or network effects

4. **"Good Business" standard assessment**
   - Duan Yongping's three criteria: differentiation, pricing power, sustainable competitive advantage — changes this period
   - Is the business becoming more asset-heavy or more asset-light?
   - If the company closed tomorrow, would users be in pain? Has this earnings report changed that answer?

5. **Management's product intuition**
   - When management discusses products / users, do they use specific language or bureaucratic language?
   - Are there impressive product insights, or worrying signals of disconnect?

**Output requirements**: Label each sub-item 🟢Improved / 🟡Flat / 🔴Deteriorated, and provide a Duan Yongping-style summary comment.

---

#### Agent 2: Financial Quality Audit (Buffett Perspective)

**Core question: Is this company earning real money or accounting profits? Has the margin of safety changed?**

> Buffett: "The first thing I do when I read any earnings report is flip to the cash flow statement."

Analysis content:

1. **Core financial data extraction and validation**
   - Revenue, gross profit, operating profit, net income — both IFRS reported and adjusted (Non-GAAP)
   - IFRS vs adjusted gap: how large, where, and is the gap widening or narrowing
   - Cross-validate key figures with at least two sources (e.g., Release de Resultados vs CVM filing)

   ```bash
   python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate \
     --metric "revenue" --values {value1} {value2} --sources "source1" "source2"
   ```

2. **Cash flow analysis (most important)**
   - Operating cash flow vs net income ratio (>100% is good, <80% is a warning)
   - Free cash flow = operating cash flow - capital expenditure (CapEx)
   - CapEx composition: maintenance vs expansion
   - Amount of buybacks and dividends

3. **Earnings quality check**
   - Accounts receivable growth rate vs revenue growth rate
   - Inventory growth rate vs revenue growth rate
   - Trend in gap between operating cash flow and net income
   - Whether capitalized expenditures have suddenly increased
   - Proportion of non-recurring gains

4. **Balance sheet health**
   - Change in net cash / net debt
   - Changes in accounts receivable / inventory turnover days
   - Goodwill and intangible asset impairment risk

5. **Valuation and margin of safety update**

   ```bash
   python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
     --price {price} --shares {shares} --reported {reported_market_cap} --currency BRL
   python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
     --price {price} --eps {LPA} --bvps {VPA}
   python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
     --price {price} --eps {LPA} --shares {shares_in_millions} \
     --growth {bull} {base} {bear} --pe {bull_PL} {base_PL} {bear_PL}
   ```

**Output requirements**: Attach tool output records for all calculations, earnings quality traffic lights 🟢/🟡/🔴, Buffett-style summary comment.

---

#### Agent 3: Competitive Landscape Analysis (Munger Perspective)

**Core question: What does this earnings report reveal about shifts in the competitive landscape?**

> Munger: "I want to know where I'm going to die, so I never go there."

Analysis content:

1. **Inferring competitive changes from earnings data**
   - Revenue growth rate vs industry growth rate — outperforming or underperforming?
   - Gross margin changes indicating intensified / eased competition
   - Marketing expense ratio change — does the company need to spend more to acquire customers?
   - R&D investment — proactive investment or forced catch-up?

2. **Comparison with competitors in the same period**
   - Key metrics compared with major competitors for the same period (if published)
   - Comparison of growth rates, profit margins, and investment intensity
   - Who is winning? Who is losing?

3. **Management's discussion of competition**
   - How they describe the competitive environment on the earnings call
   - Do they name competitors? Is the tone confident or anxious?
   - Are there any new competitive threats?

4. **Industry trend signals**
   - Impact of technology change (AI / new platforms, etc.)
   - Impact of regulatory changes on the competitive landscape
   - Consumer / demand-side trends

5. **Munger-style contrarian thinking**
   - What would kill this company? Does this earnings report contain signals pointing to those threats?
   - Looking back in 5 years, will this earnings report prove to have been a "turning point"?

**Output requirements**: Competitive landscape verdict (strengthening / flat / deteriorating), competitor comparison table, Munger-style contrarian comment.

---

#### Agent 4: Risk Signal Hunter (Li Lu Perspective)

**Core question: What is management hiding in this earnings report? Which signals are flashing?**

> Li Lu: "The most important thing in investing is avoiding permanent loss of capital."

Analysis content:

1. **Management tone analysis**
   - Read management discussion and earnings call statements paragraph by paragraph, flagging signals:
   - 🟢Candid signal (proactively acknowledging problems) / 🟢Clear signal (quantified targets given)
   - 🔴Vague signal (empty talk) / 🔴Deflection signal (answering a different question) / 🔴Externalizing blame

2. **Commitment tracking**
   - Specific management commitments from the prior period vs actual delivery this period, compared item by item
   - Duan Yongping: "To judge whether management is reliable, just check whether they did what they said they would."

3. **Footnotes and hidden information**
   - Related-party transactions, equity compensation dilution, contingent liabilities
   - Accounting policy changes, segment profit margin differences
   - Changes in customer / supplier concentration

4. **Earnings call Q&A highlights**
   - The 3–5 sharpest analyst questions and quality scoring of management's answers

5. **Risk of permanent capital loss**
   - Whether signals have appeared that could lead to permanent loss
   - New developments in regulatory / compliance / litigation risks
   - Whether management has made irreversible mistakes

**Output requirements**: Management credibility rating ★1–5, commitment fulfillment rate, risk signal checklist, Li Lu-style summary comment.

---

### Step 4: Track Progress

Show the user real-time progress:

```
📊 {Company Name} {Period} Earnings Deep-Read Progress
━━━━━━━━━━━━━━━━━━━━━━━
Phase 1 · Research
  ☐ Duan Yongping · Business Essence    ⏳ Analyzing...
  ☐ Buffett · Financial Quality         ⏳ Analyzing...
  ☐ Munger · Competitive Landscape      ⏳ Analyzing...
  ☐ Li Lu · Risk Signals                ⏳ Analyzing...
Phase 2 · Synthesis                     ⏸ Waiting
Phase 3 · Publication                   ⏸ Waiting
```

Each time a report is received, update progress and display core findings (3–5 items).

---

## Phase 2: Team Lead Synthesizes Research Report

Once all 4 research reports are in, Team Lead consolidates them into a research report draft.

**Synthesis principles** — this is not about stitching reports together; it's about finding convergence and contradictions:

1. **Consensus across the four perspectives**: conclusions all four masters agree on carry the highest credibility
2. **Contradictions across the four perspectives**: for example, Duan Yongping says the business has improved, but Munger says competition is deteriorating — these contradictions are the most valuable analysis
3. **Overlooked corners**: things none of the four emphasized — are these actually the most important?

#### Research Report Structure

```markdown
# {Company Name} {Period} Earnings Deep-Read Report
**Four Masters Parallel Analysis | {Date}**

## 1. One-Sentence Conclusion
> 50–100 words: beat / met / missed expectations, core changes, impact on investment thesis.

## 2. The 3 Most Important Changes This Period
Focus on truly significant changes — do not list data; each change within 100 words.

## 3. Four Masters Scorecard
| Perspective | Master | Core Question | Conclusion | Rating | vs Prior Period |
|-------------|--------|--------------|------------|--------|-----------------|

## 4. Core Data Snapshot
Key financial and operating metrics table (current period vs prior period vs year-over-year)

## 5. Deep Analysis by Each Perspective
3–5 most important findings per perspective

## 6. Management Tone and Commitment Tracking
Commitment fulfillment table + tone change analysis

## 7. What Would Each Master Do?
| Master | If Holding | If Not Holding | Rationale |

## 8. Conclusion
1. Beat / met / missed expectations?
2. Impact on investment thesis: strengthened / no impact / weakened / broken
3. Next catalyst
4. Action recommendation
```

---

## Phase 3: Editorial Polish + Reader Review

After the research report is complete, launch two Agents **in parallel**:

### Agent 5: Editor (Investment Newsletter Rewrite)

**Role**: Rewrite the hard-core research report into an investment newsletter article that retail investors on B3 will enjoy and understand.

**Core principles**:
- Retain all key data and conclusions; do not reduce professional depth
- Improve expression so non-professional investors can follow the logic
- Not "popularizing" — it's "making professional content less tiring to read"

**Specific tasks**:

1. **Title and opening**
   - The title should be informative and encourage clicks, but not clickbait
   - Good title example: "WEGE3 Invested R$2 Billion in Automation — Did It Pay Off?"
   - Bad title example: "Shocking! VALE3 Earnings Disaster!"
   - The opening (within 100 words) must clearly state: what is the most important conclusion of this earnings report, and why should the reader care

2. **Structure optimization**
   - A research report is for yourself; a newsletter article is for others — adjust the logical order accordingly
   - Put "The 3 Most Important Changes" at the very front (inverted pyramid structure)
   - Keep tables but trim them; convert long analytical passages into bullet points
   - Insert a "stage summary" approximately every 500 words to help readers absorb the content

3. **Expression polish**
   - Explain rigid financial jargon with analogies / scenarios: "operating cash flow is 30% below net income" → "earned 100 but only 70 ended up in the pocket"
   - The four masters' quoted comments are the soul of the article — ensure each reads sharply and is memorable
   - Paragraphs no longer than 4 lines; sentences no longer than 30 characters
   - Use contrast and juxtaposition in moderation to create reading rhythm

4. **Reader value check**
   - After each section, ask: after reading this, what decision can the reader make? If the answer is "nothing," either rewrite it or cut it
   - The article must end with a clear "So what?" — provide specific action guidance for both holders and those on the sidelines

5. **Format adaptation**
   - Newsletter-friendly layout: short paragraphs, clear subheadings, concise tables
   - Add appropriate dividers and block-quote formatting
   - Article length between 1,000–3,000 words (too long and readers will drop off)

**Output**: The complete rewritten investment newsletter article.

---

### Agent 6: Reader Review (Ordinary Investor Perspective)

**Role**: Review the article as an "ordinary investor who follows value investing, has basic financial knowledge, and holds or watches this company."

**Review dimensions**:

1. **Readability (weight 30%)**
   - How many minutes does reading the full article take? Are there paragraphs the reader wants to skip?
   - Which parts are unclear or require re-reading?
   - How is the pacing? Is there a "reading fatigue" feeling?

2. **Informational value (weight 30%)**
   - After reading, has my understanding of this company deepened?
   - Were there any "oh, so that's how it works" moments?
   - Compared with analyses I've seen elsewhere, what is unique about this piece?
   - Which information is redundant and could be removed without affecting understanding?

3. **Credibility (weight 20%)**
   - Are data sources cited? Are key judgments backed by evidence?
   - Are both sides presented, or is this one-sidedly bullish / bearish?
   - Are there any judgments that feel "overconfident" in an uncomfortable way?
   - Are the four masters' quoted comments used appropriately and powerfully?

4. **Actionability (weight 20%)**
   - After reading, do I know what to do?
   - Are the recommendations for "holders" and "observers" specific enough?
   - What should be watched next? (Catalysts, timing milestones)

**Output format**:

```markdown
## Reader Review Report

### Overall Score: X/10

### Strengths (2–3 items)
What the article does well from the reader's perspective

### Must Fix (critical issues)
- Issue 1: Specific description → Suggested fix
- Issue 2: ...

### Suggested Improvements (nice-to-have)
- Suggestion 1: ...
- Suggestion 2: ...

### Questions Readers Want Answered But the Article Doesn't Address
- Question 1
- Question 2

### One-Sentence Overall Assessment
```

---

### Team Lead Finalizes

After receiving the editor's rewrite and the reader review report:

1. **Address all "Must Fix" items from the reader review** — revise each one
2. **Selectively adopt "Suggested Improvements"** — judge whether each is worthwhile
3. **Address "Questions readers wanted answered but weren't"** — add if data supports it
4. **Final read-through** — ensure the revised full article flows and is logically consistent

---

## Output Files

```
reports/{CompanyName}/
├── {CompanyName}-earnings-{Period}.md              ← Final investment newsletter article (finalized)
├── {CompanyName}-earnings-{Period}-research.md     ← Four-masters synthesized research report (internal use)
├── {CompanyName}-earnings-{Period}-DuanYongping.md ← Business essence analysis
├── {CompanyName}-earnings-{Period}-Buffett.md      ← Financial quality audit
├── {CompanyName}-earnings-{Period}-Munger.md       ← Competitive landscape analysis
├── {CompanyName}-earnings-{Period}-LiLu.md         ← Risk signal analysis
└── {CompanyName}-earnings-{Period}-reader-review.md ← Reader review report
```

## Data Spot-Check (Quality Gate)

Run a spot-check on the final article:

```bash
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report reports/{CompanyName}/{CompanyName}-earnings-{Period}.md

python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report {report_filename}
```

**[PASS]** All checks pass → ready to publish; **[FAIL]** Any check fails → fix and re-audit.

## Relationship to Existing Skills

| Skill | Role | When to Use |
|-------|------|-------------|
| `/earnings-review` | Single-agent earnings deep-read | Quick pass, only one perspective needed |
| **`/earnings-team` (this Skill)** | **Six-agent team deep-read + investment newsletter publication** | **Key earnings for important companies, requiring depth + publication** |
| `/investment-team` | Four-agent comprehensive company research | First-time research on a company |

## Key Principles

- **Read the original, not the summary**: make every effort to obtain primary sources
- **Four perspectives are not four departments**: they must corroborate and challenge each other, not operate in silos
- **Team Lead's value lies in integrated judgment**: finding convergence and contradictions, not stitching reports together
- **Conclusions must be definitive**: "overall broadly in line with expectations but with some points worth noting" is not acceptable
- **Counterpoint runs throughout**: every positive finding must be accompanied by a counter-argument
- **Editing does not mean dumbing down**: it means making professional content more readable, not turning it into popular science
- **Reader review is not a formality**: genuinely find fault from the reader's perspective
- **Data accuracy**: cross-validate key figures, use financial_rigor.py tools for verification
