---
name: earnings-team
description: "AI Berkshire skill: Earnings Deep-Read Team: Four Masters parallel analysis + WeChat article publishing. Source: skills/earnings-team.md."
---

## Codex adapter note

This skill is generated from `skills/earnings-team.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Earnings Deep-Read Team: Four Masters Parallel Analysis + WeChat Article Publishing

Perform a team-based earnings deep-read analysis on $ARGUMENTS. Four Masters analyze the earnings report in parallel; an editor polishes the output into an article; a reader reviewer ensures quality — the final deliverable is a WeChat article ready for immediate publication.

**Supported input formats**: `Company name Period`, e.g.: `Tencent 2025Q4`, `PDD 2025 Annual Report`, `Meituan Latest`

## Design Philosophy

A good earnings analysis must solve two problems:
1. **Understanding the future yourself** — requires deep research from four different perspectives
2. **Helping readers understand the value** — requires editorial polish and quality control from a reader's perspective

This Skill's workflow has three phases:
- **Phase 1 · Research**: Four Masters read the earnings report in parallel (Duan Yongping on business fundamentals, Buffett on financial quality, Munger on competitive dynamics, Li Lu on risk signals)
- **Phase 2 · Synthesis**: Team Lead integrates the four perspectives and produces a research report draft
- **Phase 3 · Publication**: Editor Agent rewrites into a WeChat article + Reader Reviewer Agent raises revision suggestions → Team Lead finalizes

---

## Phase 1: Four Masters Parallel Research

### Step 1: Obtain Primary Sources

Use the Agent tool to launch background Agents **in parallel** to retrieve the following raw materials:

| Material Type | Source | Priority |
|---------|---------|--------|
| Earnings report (original text) | Company IR page, SEC EDGAR (US stocks), HKEX Disclosure Easy (HK stocks), CNINFO (A-shares) | Highest |
| Earnings call transcript | Seeking Alpha, company IR page, Xueqiu | Highest |
| Management letter to shareholders | Extracted from annual report | High (annual report only) |
| Previous period earnings report / earnings call | Same as above | High (for promise tracking) |

**Source Availability Rating**:

| Grade | Characteristics | Impact |
|------|------|------|
| Grade A | Full original text obtained | Execute all steps normally |
| Grade B | Only partial original text or third-party summary obtained | Label "non-primary source", reduce weight of footnote analysis |
| Grade C | Only news reports and data-site summaries available | Focus on core data changes, skip footnote mining, label "insufficient primary sources" |

Communicate the source availability rating to each Agent so it calibrates analysis depth accordingly.

### Step 2: Present the Team Framework to the User

| Phase | Role | Master / Focus | Core Task |
|------|------|----------|---------|
| Research | **Team Lead** (yourself) | Overall coordinator | Orchestrate, synthesize, finalize |
| Research | Business Fundamentals Analyst | Duan Yongping | Has this business gotten better or worse? |
| Research | Financial Quality Auditor | Buffett | Is the money earned real or accounting fiction? |
| Research | Competitive Dynamics Analyst | Munger | How is the competitive landscape changing? |
| Research | Risk Signal Hunter | Li Lu | What is management hiding? |
| Publication | Editor | WeChat writing | Rewrite the research report into a great article |
| Publication | Reader Reviewer | Ordinary investor | Can readers understand it? Do they gain value from it? |

### Step 3: Launch 4 Parallel Research Agents

Use the Agent tool to launch 4 background Agents **in the same message**.

---

#### Agent 1: Business Fundamentals Analysis (Duan Yongping Perspective)

**Core question: Does this earnings report show the business has gotten better or worse?**

> Duan Yongping: "Investing is buying a business. Reading an earnings report isn't about reading numbers — it's about seeing whether the business has changed."

Analysis content:

1. **Revenue Structure Breakdown and Interpretation**
   - Revenue by segment / by geography — which are accelerating, which are decelerating
   - Not just listing numbers — what commercial logic does each segment reflect
   - Is revenue growth driven by "volume" or "price"? Which is healthier?

2. **User / Customer Value Changes**
   - Changes in operating metrics such as DAU/MAU/paying users
   - Quality indicators: time spent, ARPU, retention rate
   - Is the platform/product's value to users strengthening or weakening?

3. **Moat Assessment**
   - Gross margin changes reflect whether pricing power is intact
   - Market share changes reflect whether competitive barriers are effective
   - Any signals that customer switching costs / network effects are eroding?

4. **"Good Business" Standard Evaluation**
   - Duan Yongping's three conditions: differentiation, pricing power, sustainable competitive advantage — how did they change this period?
   - Is the business becoming heavier or lighter (asset-intensive vs. asset-light)?
   - If the company shut down tomorrow, would users be in serious pain? Has that changed based on this report?

5. **Management's Product Intuition**
   - When management discusses products/users, do they use specific language or bureaucratic language?
   - Any impressive product insights, or worrying signs of disconnection?

**Output requirement**: Label each sub-item 🟢 Improved / 🟡 Flat / 🔴 Deteriorated; provide a Duan Yongping-style summary commentary.

---

#### Agent 2: Financial Quality Audit (Buffett Perspective)

**Core question: Is this company earning real money or fake money? Has the margin of safety changed?**

> Buffett: "The first thing I do with every earnings report is flip to the cash flow statement."

Analysis content:

1. **Core Financial Data Extraction and Verification**
   - Revenue, gross profit, operating profit, net income — both GAAP and Non-GAAP
   - GAAP vs Non-GAAP gap: how large, where it comes from, is the gap widening or narrowing
   - Cross-validate key data points using at least two sources

   ```bash
   python3 ~/ai-berkshire/tools/financial_rigor.py cross-validate \
     --metric "revenue" --values {value1} {value2} --sources "source1" "source2"
   ```

2. **Cash Flow Analysis (Most Important)**
   - Operating cash flow vs net income ratio (>100% is good, <80% warrants caution)
   - Free cash flow = operating cash flow - capital expenditures
   - Capex composition: maintenance vs expansion
   - Buyback and dividend amounts

3. **Earnings Quality Check**
   - Accounts receivable growth rate vs revenue growth rate
   - Inventory growth rate vs revenue growth rate
   - Trend in gap between operating cash flow and net income
   - Any sudden increase in capitalized expenditures
   - Share of non-recurring gains

4. **Balance Sheet Health**
   - Net cash / net debt changes
   - Accounts receivable / inventory turnover days changes
   - Goodwill and intangible asset impairment risk

5. **Valuation and Margin of Safety Update**

   ```bash
   python3 ~/ai-berkshire/tools/financial_rigor.py verify-market-cap \
     --price {price} --shares {shares} --reported {reported_market_cap} --currency {currency}
   python3 ~/ai-berkshire/tools/financial_rigor.py verify-valuation \
     --price {price} --eps {EPS} --bvps {book_value_per_share}
   python3 ~/ai-berkshire/tools/financial_rigor.py three-scenario \
     --price {price} --eps {EPS} --shares {shares_in_hundreds_of_millions} \
     --growth {bull} {base} {bear} --pe {bull_PE} {base_PE} {bear_PE}
   ```

**Output requirement**: Attach tool output records for all calculations; earnings quality signal lights 🟢/🟡/🔴; Buffett-style summary commentary.

---

#### Agent 3: Competitive Landscape Analysis (Munger Perspective)

**Core question: What changes in the competitive landscape does this earnings report reveal?**

> Munger: "I want to know where I'm going to die so I won't go there."

Analysis content:

1. **Inferring Competitive Changes from Earnings Data**
   - Revenue growth rate vs industry growth rate — outperforming or underperforming?
   - Gross margin changes reflect intensifying/easing competition
   - Marketing expense ratio changes — does it cost more to acquire customers?
   - R&D investment — proactive commitment or reactive catch-up?

2. **Peer Competitor Comparison for the Same Period**
   - Key metrics comparison with major competitors for the same period (if published)
   - Growth rate, profit margin, and investment intensity comparison
   - Who is winning? Who is losing?

3. **Management's Discussion of Competition**
   - How did they describe the competitive environment on the earnings call?
   - Did they name competitors? Was the tone confident or anxious?
   - Any new competitive threats mentioned?

4. **Industry Trend Signals**
   - Impact of technological change (AI/new platforms, etc.)
   - Impact of regulatory changes on the competitive landscape
   - Consumer / demand-side trends

5. **Munger-Style Inversion Thinking**
   - What would kill this company? Does this earnings report contain signals pointing to those threats?
   - Looking back in 5 years, will this earnings report be seen as a "turning point"?

**Output requirement**: Competitive landscape judgment (strengthening / flat / deteriorating), competitor comparison table, Munger-style inversion commentary.

---

#### Agent 4: Risk Signal Hunter (Li Lu Perspective)

**Core question: What is management hiding in this earnings report? Which signals are flashing?**

> Li Lu: "The most important thing in investing is to avoid permanent capital loss."

Analysis content:

1. **Management Tone Analysis**
   - Read through management discussion and earnings call remarks paragraph by paragraph, flagging signals:
   - 🟢 Candor signal (proactively acknowledging problems) / 🟢 Clarity signal (quantified targets given)
   - 🔴 Vagueness signal (empty words) / 🔴 Deflection signal (non-responsive answers) / 🔴 External attribution (blaming outside factors)

2. **Promise Tracking**
   - Specific management commitments from the previous period vs actual delivery this period — compare line by line
   - Duan Yongping: "To judge whether management is trustworthy, look at whether they did what they said before."

3. **Footnotes and Hidden Information**
   - Related-party transactions, stock-based compensation dilution, contingent liabilities
   - Accounting policy changes, segment profit margin discrepancies
   - Changes in customer / supplier concentration

4. **Earnings Call Q&A Highlights**
   - The 3–5 sharpest analyst questions and quality rating of management's responses

5. **Permanent Capital Loss Risk**
   - Any signals that could lead to permanent capital loss
   - New developments in regulatory / compliance / litigation risk
   - Did management make any irreversible wrong decisions?

**Output requirement**: Management credibility rating ★1–5, promise fulfillment rate, risk signal checklist, Li Lu-style summary commentary.

---

### Step 4: Track Progress

Display in real time for the user:

```
📊 {Company Name} {Period} Earnings Deep-Read Progress
━━━━━━━━━━━━━━━━━━━━━━━
Phase 1 · Research
  ☐ Duan Yongping · Business Fundamentals    ⏳ Analyzing...
  ☐ Buffett · Financial Quality              ⏳ Analyzing...
  ☐ Munger · Competitive Landscape           ⏳ Analyzing...
  ☐ Li Lu · Risk Signals                    ⏳ Analyzing...
Phase 2 · Synthesis                          ⏸ Waiting
Phase 3 · Publication                        ⏸ Waiting
```

As each report arrives, update the progress and display the core findings (3–5 points).

---

## Phase 2: Team Lead Synthesizes the Research Report

Once all 4 research reports are in, the Team Lead integrates them into a research report draft.

**Synthesis principles** — not stitching reports together, but finding convergence and contradictions:

1. **Consensus across four perspectives**: Conclusions all four Masters agree on carry the highest credibility
2. **Contradictions across four perspectives**: For example, Duan Yongping says the business improved, but Munger says competition is deteriorating — these contradictions are the most valuable part of the analysis
3. **Overlooked corners**: Things none of the four emphasized — could they be precisely the most important?

#### Research Report Structure

```markdown
# {Company Name} {Period} Earnings Deep-Read Report
**Four Masters Parallel Analysis | {Date}**

## I. One-Sentence Conclusion
> 50–100 words: beat/met/missed expectations, core changes, impact on investment thesis.

## II. The 3 Most Important Changes This Period
Focus on truly important changes, do not list data exhaustively; each change within 100 words.

## III. Four Masters Scorecard
| Perspective | Master | Core Question | Conclusion | Rating | vs Prior Period |
|------|------|---------|------|------|--------|

## IV. Key Data Snapshot
Table of key financial and operating metrics (this period vs prior period vs year-over-year)

## V. Deep Analysis by Perspective
3–5 most important findings per perspective

## VI. Management Tone and Promise Tracking
Promise fulfillment table + tone change analysis

## VII. What Would the Four Masters Do?
| Master | If holding | If not holding | Rationale |

## VIII. Conclusion
1. Beat / met / missed expectations?
2. Investment thesis impact: reinforced / no impact / weakened / broken
3. Next catalyst
4. Action recommendation
```

---

## Phase 3: Editorial Polish + Reader Review

Once the research report is complete, launch two Agents **in parallel**:

### Agent 5: Editor (WeChat Article Rewrite)

**Role**: Rewrite the hard-core research report into an article that WeChat readers will enjoy and understand.

**Core principles**:
- Preserve all key data and conclusions; do not reduce professional depth
- Improve presentation so even non-professional investors can follow the logic
- This is not "simplification" — it is "making professional content less exhausting to read"

**Specific tasks**:

1. **Title and Opening**
   - The title should be informative and compelling to click, but not clickbait
   - Good title example: "Kuaishou Bet 26 Billion on AI — Did It Pay Off?"
   - Bad title example: "Shocking! Kuaishou Earnings Explode!"
   - The opening 100 words must clearly state: what is the most important conclusion of this earnings report, and why should the reader care

2. **Structure Optimization**
   - Research reports are written for yourself; WeChat articles are written for others — adjust the logical order
   - Put "The 3 Most Important Changes" at the very front (inverted pyramid structure)
   - Keep tables but simplify them; replace long analytical paragraphs with bullet points
   - Insert a "stage summary" every ~500 words to help readers digest

3. **Expression Polish**
   - Explain rigid financial jargon through analogy/scenario: "Operating cash flow is 30% below net income" → "Earned 100 yuan but only 70 yuan made it into the pocket"
   - The Four Masters' commentary quotes are the soul of the article — make sure every one reads sharply and memorably
   - Paragraphs no longer than 4 lines; sentences no longer than 30 characters
   - Use contrast and tension in moderation to create reading rhythm

4. **Reader Value Check**
   - After each section, ask: after reading this, what decision can the reader make? If the answer is "nothing," either rewrite or cut
   - The article must end with a clear "So what?" — give specific guidance for both current holders and those on the sidelines

5. **Format Adaptation**
   - WeChat layout-friendly: short paragraphs, clear sub-headings, concise tables
   - Add appropriate dividers and quotation formatting
   - Article length: 1,000–3,000 words (too long and readers will drop off)

**Output**: Complete rewritten WeChat article.

---

### Agent 6: Reader Review (Ordinary Investor Perspective)

**Role**: Review the article as an "ordinary investor who follows value investing, has basic financial knowledge, and holds or watches the company."

**Review dimensions**:

1. **Readability (weight 30%)**
   - How many minutes does it take to read the full article? Are there paragraphs you want to skip?
   - Which parts are hard to understand or require re-reading?
   - How is the reading rhythm? Is there a feeling of "getting tired of reading"?

2. **Information Value (weight 30%)**
   - After reading, do I understand the company better?
   - Were there any "ah, so that's how it works" moments?
   - Compared with other analyses I've read, what is unique about this one?
   - Which information is redundant and could be removed without affecting understanding?

3. **Credibility (weight 20%)**
   - Are data points sourced? Are key judgments supported by evidence?
   - Does the article present both sides, or is it one-sided bullish/bearish?
   - Are there any judgments that feel "overconfident" and make you uncomfortable?
   - Are the Four Masters' quotes appropriate and powerful?

4. **Actionability (weight 20%)**
   - After reading, do I know what to do?
   - Are the recommendations for "current holders" and "those on the sidelines" specific enough?
   - What should I watch next? (Catalysts, timelines)

**Output format**:

```markdown
## Reader Review Report

### Overall Rating: X/10

### Strengths (2–3 points)
What the article does well from the reader's perspective

### Must Fix (critical issues)
- Issue 1: Specific description → Suggested fix
- Issue 2: ...

### Suggested Improvements (nice-to-have)
- Suggestion 1: ...
- Suggestion 2: ...

### Questions readers most want answered but the article didn't address
- Question 1
- Question 2

### One-Line Overall Verdict
```

---

### Team Lead Finalizes

After receiving the editor's rewrite and the reader review report:

1. **Address the "Must Fix" items from the reader review** — revise each one
2. **Selectively adopt the "Suggested Improvements"** — judge whether they are worth implementing
3. **Fill in "Questions readers wanted answered but weren't"** — add them if data supports
4. **Final read-through** — ensure the revised article flows coherently and is logically consistent

---

## Output Files

```
reports/{Company Name}/
├── {Company Name}-earnings-{Period}.md               ← Final WeChat article (finalized)
├── {Company Name}-earnings-{Period}-research-draft.md ← Four Masters synthesized research report (internal use)
├── {Company Name}-earnings-{Period}-DuanYongping.md  ← Business fundamentals analysis
├── {Company Name}-earnings-{Period}-Buffett.md       ← Financial quality audit
├── {Company Name}-earnings-{Period}-Munger.md        ← Competitive landscape analysis
├── {Company Name}-earnings-{Period}-LiLu.md          ← Risk signal analysis
└── {Company Name}-earnings-{Period}-reader-review.md ← Reader review report
```

## Data Spot-Check (Publication Gate)

Run a spot-check on the final article:

```bash
python3 ~/ai-berkshire/tools/report_audit.py extract \
  --report reports/{Company Name}/{Company Name}-earnings-{Period}.md

python3 ~/ai-berkshire/tools/report_audit.py verdict \
  --results '<completed JSON>' \
  --report {report_filename}
```

**[PASS]** All checks pass → ready to publish; **[REJECT]** Any check fails → fix and re-audit.

## Relationship to Existing Skills

| Skill | Role | When to Use |
|-------|------|--------|
| `/earnings-review` | Single-Agent earnings read | Quick pass, only one perspective needed |
| **`/earnings-team` (this Skill)** | **Six-Agent team deep-read + WeChat publishing** | **Key earnings reports for important companies, requiring depth + publication** |
| `/investment-team` | Four-Agent comprehensive company research | First-time research on a company |

## Key Principles

- **Read the original, not summaries**: make every effort to obtain primary sources
- **Four perspectives are not four departments**: they must cross-validate and challenge each other, not talk past each other
- **Team Lead's value is in integrated judgment**: find convergence and contradictions, not stitch reports together
- **Conclusions must be clear**: "overall largely in line with expectations but there are also some points worth noting" is not acceptable
- **Counter-checking runs throughout**: every positive finding must be accompanied by a counter-argument
- **Editing does not mean dumbing down**: it means making professional content more readable, not turning it into popular science
- **Reader review is not a formality**: genuinely adopt the reader's perspective and find real problems
- **Data accuracy**: cross-validate key data, use financial_rigor.py tools for verification
