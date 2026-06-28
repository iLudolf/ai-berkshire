---
name: news-pulse
description: Company News Pulse — rapid attribution of stock price movements. Uses 4 parallel Agents to scout company events / regulatory policy / industry peers / market sentiment, producing an "event timeline + primary cause of movement + whether to trigger thesis review".
---

# Company News Pulse: Rapid Stock Movement Attribution Team

Conduct a recent news reconnaissance and movement attribution analysis for $ARGUMENTS. **This is not deep investment research — it is rapid intelligence response** — the goal is to answer within 10 minutes: "What has happened with this company recently? What is the true cause of the stock price movement? Should we re-examine the investment thesis?"

## Use Cases

- A position or watchlist stock surges/drops sharply (typical trigger: ±5% in a single day, ±10% in a week)
- Stock moves after earnings and you want to quickly understand what the market is reacting to
- You see a news headline but are unsure whether it is noise or a real signal
- **Not applicable for**: full investment research (use `/investment-team`), deep earnings analysis (use `/earnings-review`), long-term thesis tracking (use `/thesis-tracker`)

## Execution Flow

### Step 1: Confirm Parameters and Scenario

Clarify the following with the user (if not provided in $ARGUMENTS):

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Company name** | Brazilian / English / ticker (e.g. PETR4, VALE3) all accepted | Required |
| **Time window** | Number of days to look back for news | Default 14 days; can narrow to 7 days during earnings season |
| **Price movement** | Magnitude + timeframe, e.g. "down 12% / 3 days" | Optional — if provided, used to focus the attribution |
| **Focus area** | Company events / regulatory / industry / sentiment | Default: all four equally |

If the user only provides a company name, ask first: "How many days of news? Is there a specific price movement to explain?" — **do not assume silently**.

### Step 2: Information Availability Classification

Reference the A/B/C rating in `investment-team.md`, but with different dimensions:

| Grade | Characteristics | Reconnaissance Strategy |
|-------|----------------|------------------------|
| **Grade A (Information-rich)** | Large-cap, wide media coverage, earnings season | Focus on **noise reduction and attribution** — too much information makes finding the true cause harder; each Agent must exercise judgment and filter out "repeated paraphrase" secondary news |
| **Grade B (Moderate information)** | Small/mid-cap, average coverage | Standard mode — each key event accompanied by 1-2 independent sources |
| **Grade C (Information-scarce)** | Small B3-listed stocks, newly listed, obscure companies | Switch to "reconnaissance mode" — may find no news to explain the movement; **this conclusion itself is valuable** (may be technical/capital-flow driven rather than fundamental) |

Communicate the grade to each Agent — it affects their reconnaissance approach.

### Step 3: Create the Team

Use TeamCreate to create the team:
- `team_name`: `{company-name}-newspulse` (lowercase English, e.g. `vale3-newspulse`)
- `agent_type`: `team-lead`

### Step 4: Create 4 Reconnaissance Tasks

Use TaskCreate to create the following 4 tasks:

#### Task 1: Company Event Scout (company-event-scout)

- **subject**: `Scout {company name} company-level events over the past {N} days`
- **description**:
  1. **Official announcements**: Recent filings on CVM (DFP/ITR/FRE), company RI (investor relations) pages, and B3 disclosure platform (www.rad.cvm.gov.br)
  2. **Earnings and guidance**: Latest quarterly/annual report, earnings pre-announcement, key earnings call takeaways
  3. **Management actions**: Executive changes, insider buys/sells, buybacks, dividends, equity incentives
  4. **Major business events**: New product launches, mergers and acquisitions, divestitures, major customers / major orders
  5. **Capital operations**: Secondary offerings (follow-on), debentures, BDR conversions, stock splits / reverse splits, delisting proposals
  6. **Litigation and compliance**: Lawsuits filed, voluntarily disclosed compliance events
  7. Each event annotated with: **date / source link / one-sentence summary / likely relevance to price movement (high/medium/low)**
  8. Output as a timeline table in reverse chronological order

#### Task 2: Regulatory and Policy Watcher (regulatory-watcher)

- **subject**: `Scout {industry/company} regulatory and policy changes over the past {N} days`
- **description**:
  1. **Industry regulation**: New rules, fines, rectification orders, license changes in the relevant sector
  2. **Cross-border policy**: Brazil-US / Brazil-China trade relations, tariffs, export controls, LGPD (data privacy), BNDES financing changes
  3. **Tax policy**: VAT, corporate income tax, individual income tax related changes
  4. **Antitrust and competition law**: Investigations, fines, merger vetoes
  5. **Sector-specific policy**: ANS/ANVISA regulations (healthcare), ANEEL/ANATEL/ANP rules (utilities/telecom/oil), marco legal do saneamento, agronegócio export quotas, Petrobras pricing policy, real estate credit (SFH/SFI limits), etc.
  6. **Monetary and foreign exchange**: Selic/CDI rate decisions (COPOM), BRL/USD exchange rate moves, capital flow controls, IPCA surprises affecting the company's cost base or debt
  7. Each policy annotated with: **date / source / degree of direct impact on the company (direct/indirect/unrelated)**
  8. Key judgment: whether any "policy black swan" has just landed

#### Task 3: Industry and Peer Analyst (industry-peer-analyst)

- **subject**: `Scout {company name} competitive landscape and peer activity over the past {N} days`
- **description**:
  1. **Direct competitors**: List 3-5 core competitors and check recent events for each (earnings, products, price wars, personnel)
  2. **Supply chain upstream and downstream**: Upstream raw materials / suppliers, downstream customers / channels — recent price, capacity, order changes
  3. **Industry overall**: Industry health indicators, shipment data, demand-side signals (consumption data, tender data, etc.)
  4. **Substitution threat**: Impact of new technologies and new business models on the industry
  5. **Sector index performance**: Recent performance of peer stocks — is this company outperforming / underperforming / in line with the sector?
  6. Key judgment: **Is this a company-specific event, or a beta-level fluctuation across the entire industry?**
  7. Each event annotated with source and date

#### Task 4: Market Sentiment and Sell-Side / KOL Tracker (sentiment-tracker)

- **subject**: `Scout {company name} market sentiment and institutional view changes over the past {N} days`
- **description**:
  1. **Sell-side rating changes**: Recent rating / price target adjustments from XP Investimentos, BTG Pactual Research, Itaú BBA, Goldman Sachs Brasil, UBS BB, etc.
  2. **Institutional position changes**: CVM filings (Form 358 — significant shareholder changes), FII Informe Mensal updates, fund manager letters (cartas de gestão) from major asset managers
  3. **Short interest data**: B3 aluguel de ações (short lending) data, short ratio changes, newly published short-selling reports (if any)
  4. **KOL views**: Search for recent commentary from prominent Brazilian value investors and analysts on X / YouTube / Telegram investor channels / Infomoney / Suno Research
     - Only invoke if relevant to the specific company being investigated
  5. **Rumors and unverified reports**: Unverified media rumors, hot social media discussions (X / Reddit / Telegram investor groups / Infomoney forums)
  6. **Technical signals**: Whether key support/resistance levels have been hit, block trades, abnormal margin activity
  7. Key judgment: **Is this driven by fundamentals, or by sentiment / capital flows?**

### Step 5: Launch 4 Agents in Parallel

**All 4 Task tool calls must be made in a single message in parallel.** Configuration for each Agent:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`
- `team_name`: `{company-name}-newspulse`
- `name`: corresponding role name (company-event-scout / regulatory-watcher / industry-peer-analyst / sentiment-tracker)

Prompt template for each Agent:

```
You are the "{role name}" in the {company name} News Pulse team, responsible for scouting the {reconnaissance dimension} dimension over the past {N} days.

Time window: {start date} ~ {today's date}
Price movement context: {user-provided movement info, or write "No specific movement — routine check" if none}
Information availability grade: {A/B/C}

Please complete Task #{task number}: {task subject}

Detailed reconnaissance requirements:
{task description content}

**Reconnaissance methods**:
- Prioritize WebSearch for time-sensitive queries (add date or "recently", "latest", "2026" to keywords)
- Use WebFetch to read original sources for key events (announcement text, earnings reports, regulatory filings)
- Apply "independent source verification" for each event — rumors require at least 2 independent sources
- **Do not be misled by clickbait headlines**: flag any event where the headline does not match the body as "headline misleading"

**Output format (important)**:
1. **Key findings**: 3-5 most critical events, 1-2 sentences each
2. **Full event timeline table** (reverse chronological):
   | Date | Event | Source | Relevance to Price Movement | Persistence |
3. **Dimension-level attribution conclusion**: Based on events found, answer "Can this dimension explain the price movement? What is the confidence level?"
4. **Data gap declaration**: What information was not found, what is questionable, what needs more data
5. Strictly distinguish "fact" from "speculation" — follow CLAUDE.md objectivity principles

**Upon completion**:
1. Use TaskUpdate to mark the task as completed
2. Send the full reconnaissance report to team-lead via SendMessage (type: "message", recipient: "team-lead")
```

### Step 6: Track Progress in Real Time

- Each time a reconnaissance report is received, show the user the top 3 key findings from that dimension
- Wait for all 4 reports to arrive
- Once all 4 are received, send a shutdown_request to all 4 Agents via SendMessage

### Step 7: Team-Lead Consolidated Attribution

Aggregate the 4 reconnaissance reports and produce a **movement attribution report** (not a research report — the focus is "judgment"):

---

#### 1. One-Sentence Attribution
> One paragraph (30-60 words): primary cause + secondary cause + nature judgment (value event / sentiment fluctuation / unknown)

#### 2. Full Event Timeline (merged across 4 dimensions)

Reverse chronological, merging all dimension events:

| Date | Dimension | Event | Source | Attribution Weight |
|------|-----------|-------|--------|--------------------|
| 2026-04-30 | Company | XX | link | 🔴 High |
| 2026-04-29 | Industry | XX | link | 🟡 Medium |
| 2026-04-28 | Sentiment | XX | link | ⚪ Low |

Weight legend: 🔴 High (sufficient to explain movement on its own) / 🟡 Medium (partial contributor) / ⚪ Low (background noise)

#### 3. Movement Attribution Table

| Candidate Explanation | Evidence | Counter-Evidence | Confidence | Persistence |
|-----------------------|----------|-----------------|------------|-------------|
| Example: earnings miss | Revenue 5% below expectations, gross margin declined | Management cited one-time factors | High | Short-term 1-2 weeks |
| Example: industry beta | Peers down 8% in same period | This stock fell significantly more than the sector | Medium | In line with sector |

#### 4. Nature Judgment (Core Conclusion)

Check one:

- [ ] **Value event**: A real fundamental change has occurred (earnings, economic moat, management, end-game thesis) — investment thesis review required
- [ ] **Sentiment / technical fluctuation**: No fundamental change — driven by capital flows / sentiment / beta; treat as opportunity or noise
- [ ] **True cause unknown**: No event found that matches the magnitude of the price movement — **this is the most dangerous conclusion**: either the market has advance knowledge (insider / front-running), or we missed an information source
- [ ] **Mixed**: Partial value event + partial sentiment amplification

#### 5. Per-Dimension Scout Summary

3-5 most important findings per dimension + that dimension's attribution contribution.

#### 6. Action Recommendations

| Action | Recommended | Rationale |
|--------|-------------|-----------|
| Trigger investment thesis review (`/thesis-tracker`) | | |
| Trigger deep earnings analysis (`/earnings-review`) | | |
| Trigger management review (`/management-deep-dive`) | | |
| Position adjustment (add / reduce / hold) | | Note only — final decision rests with the user |
| Observe only | | |

#### 7. Tracking Checklist for the Next 7-30 Days

- [ ] Upcoming event 1 (e.g., 5/15 earnings call)
- [ ] Metric to track 2
- [ ] Key observation signal 3

#### 8. Information Gap Declaration

Honestly list any unresolved questions from this reconnaissance, information that could not be found, and items awaiting further disclosure. **Prefer marking "uncertain" over filling gaps with speculation**.

---

### Step 8: Save the Report

Write to `reports/{company-name}/{company-name}-news-{YYYYMMDD}.md`. If the `reports/{company-name}/` directory does not exist, create it (indicating no prior research reports have been filed for this company).

### Step 9: Clean Up the Team

Use TeamDelete to clean up team resources.

## Core Principles

1. **Speed over completeness** — the core value of this skill is delivering an attribution judgment within 10-15 minutes; do not fall into deep analysis (that is the responsibility of other skills)
2. **Attribution over enumeration** — finding events is not hard; the challenge is judging "which event is proportionate to this price movement". Make cuts, not additions
3. **Be honest about "unknown"** — when the primary cause cannot be found, explicitly write "true cause unknown". This is more valuable than forcing a causal chain (the market may be front-running negative news)
4. **No predetermined stance** — do not lean toward "this is just sentiment noise, no big deal" simply because you hold a position. Follow where the evidence points
5. **Distinguish "catalyst" from "coincidence"** — events that happen simultaneously are not necessarily the primary cause; check whether the magnitude of impact is proportionate
6. **Respect information availability** — for Grade C companies, it may simply be impossible to find any news; this conclusion must be written up
7. **Follow `CLAUDE.md` objectivity principles** — all judgments accompanied by data sources; distinguish fact from opinion
8. **Do not make decisions for the user** — provide attribution and an action recommendation checklist, but buy/sell decisions belong to the user
