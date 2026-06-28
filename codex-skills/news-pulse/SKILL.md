---
name: news-pulse
description: Company News Pulse: rapid attribution of stock price movements. Uses 4 parallel Agents to scout company events / regulatory policy / industry peers / market sentiment, producing an "event timeline + primary cause judgment + whether the investment thesis needs review".
---

## Codex adapter note

This skill is generated from `skills/news-pulse.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Company News Pulse: Rapid Stock Price Attribution Team

Conduct recent news scouting and movement attribution for $ARGUMENTS. **This is not deep investment research — it is rapid intelligence response** — the goal is to answer within 10 minutes: "What has happened with this company recently? What is the true cause of the stock price movement? Do we need to review the investment thesis?"

## Applicable Scenarios

- A position or watchlist stock surges or drops sharply (general trigger: ±5% in a single day, ±10% in a week)
- Stock moves after an earnings report and you want to quickly understand what the market is reacting to
- You see a news headline but are unsure whether it is noise or a real signal
- **Not applicable for**: full investment research (use `/investment-team`), deep earnings reading (use `/earnings-review`), long-term thesis tracking (use `/thesis-tracker`)

## Execution Flow

### Step 1: Confirm Parameters and Scenario

Clarify the following with the user (if not provided in $ARGUMENTS):

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Company name** | Chinese / English / ticker symbol all accepted | Required |
| **Time window** | Number of days to look back for news | Default 14 days; can narrow to 7 days during earnings season |
| **Stock movement** | Gain/loss magnitude + timeframe, e.g. "down 12% over 3 days" | Optional — if provided, use to focus attribution |
| **Focus area** | Company events / regulatory / industry / sentiment | Default: equal weight across all four |

If the user only provides the company name, ask first: "How many days of news? Is there a specific stock price movement you want explained?" — **do not silently assume**.

### Step 2: Information Availability Rating

Refer to the A/B/C rating from `investment-team.md`, but with different dimensions:

| Rating | Characteristics | Scouting Strategy |
|--------|-----------------|-------------------|
| **Grade A (information-rich)** | Large-cap, broad media coverage, earnings season | Focus on **noise reduction and attribution** — too much information makes finding the true cause harder; each Agent must exercise judgment and filter out second-hand "re-reported" news |
| **Grade B (moderate information)** | Small/mid-cap, average coverage | Standard mode — attach 1-2 independent sources to each key event |
| **Grade C (information-scarce)** | Small HK-listed stocks, newly listed, obscure names | Switch to "blind-spot mode" — there may be no news at all that explains the movement; **this conclusion itself is valuable** (movement may be technical/flow-driven rather than fundamental) |

Inform each Agent of the rating, as it affects their scouting approach.

### Step 3: Create the Team

Use TeamCreate to create the team:
- `team_name`: `{company-name}-newspulse` (lowercase English, e.g. `pdd-newspulse`)
- `agent_type`: `team-lead`

### Step 4: Create 4 Scouting Tasks

Use TaskCreate to create the following 4 tasks:

#### Task 1: Company Event Scout (company-event-scout)

- **subject**: `Scout company-level events for {company name} over the past {N} days`
- **description**:
  1. **Official announcements**: Recent disclosures on regulatory platforms such as HKEX / SEC / CNINFO
  2. **Earnings and guidance**: Latest quarterly/annual reports, profit alerts, earnings call highlights
  3. **Management actions**: Executive changes, insider buy/sell, buybacks, dividends, equity incentives
  4. **Major business events**: New product launches, M&A, divestitures, major customers / large orders
  5. **Capital operations**: Secondary offerings, convertible bonds, ADR conversions, return-to-A-share / delisting proposals
  6. **Litigation and compliance**: Lawsuits filed, self-disclosed compliance events
  7. For each event, annotate: **Date / Source link / One-sentence summary / Likely relevance to stock price movement (High / Medium / Low)**
  8. Output a timeline table sorted by date in reverse chronological order

#### Task 2: Regulatory and Policy Watcher (regulatory-watcher)

- **subject**: `Scout regulatory and policy changes for {industry/company} over the past {N} days`
- **description**:
  1. **Industry regulation**: New rules, fines, rectification orders, license changes in the relevant sector
  2. **Cross-border policy**: China-US relations (Chinese ADRs), tariffs, export controls, data security
  3. **Tax policy**: VAT, corporate income tax, individual income tax changes
  4. **Antitrust and competition law**: Investigations, fines, M&A vetoes
  5. **Sector-specific policy**: pharmaceutical volume-based procurement, education double-reduction, real estate three red lines, internet platform regulation, etc.
  6. **Currency and foreign exchange**: Exchange rate / interest rate / capital control changes affecting this company
  7. For each policy, annotate: **Date / Source / Degree of direct impact on the company (Direct / Indirect / Not relevant)**
  8. Key judgment: Has a "policy black swan" just landed?

#### Task 3: Industry and Peer Analyst (industry-peer-analyst)

- **subject**: `Scout competitive landscape and peer movements for {company name} over the past {N} days`
- **description**:
  1. **Direct competitors**: List 3-5 core competitors and check each for recent events (earnings, products, price wars, personnel)
  2. **Supply chain**: Upstream raw materials/suppliers, downstream customers/channels — recent price, capacity, and order changes
  3. **Industry overall**: Industry cycle data, shipment volumes, demand-side signals (consumption data, bidding data, etc.)
  4. **Substitute threats**: New technology or new business models disrupting the industry
  5. **Sector index performance**: Recent performance of peer stocks — is this company outperforming, underperforming, or in line?
  6. Key judgment: **Is this a company-specific event or a broader industry beta swing?**
  7. Annotate source and date for each event

#### Task 4: Market Sentiment and Sell-Side / Key Opinion Leaders (sentiment-tracker)

- **subject**: `Scout market sentiment and institutional view changes for {company name} over the past {N} days`
- **description**:
  1. **Sell-side rating changes**: Recent rating / target price revisions from Goldman Sachs, Morgan Stanley, CICC, etc.
  2. **Institutional position changes**: 13F disclosures (US stocks), Stock Connect holdings, northbound capital flows
  3. **Short-selling data**: Short interest ratio, newly published short reports (if any)
  4. **Key opinion leaders**: Can call `python3 ~/ai-berkshire/tools/xueqiu_scraper.py` to scrape recent relevant posts from Duan Yongping and other key investors
     - Duan Yongping user_id: `1247347556`
     - Example command: `python3 ~/ai-berkshire/tools/xueqiu_scraper.py --user-id 1247347556 --keywords {company name},{ticker} --output /tmp/dyp-{company name}.md`
     - Only call this if the company is a known holding of Duan Yongping / Li Lu; otherwise skip to save time
  5. **Rumors and unofficial pieces**: Unverified media rumors, trending social media discussions (Xueqiu / X / Reddit)
  6. **Technical signals**: Key support/resistance levels touched, block trades, abnormal margin activity
  7. Key judgment: **Is this fundamentals-driven or sentiment/flow-driven?**

### Step 5: Launch 4 Agents in Parallel

**Must call the Task tool 4 times in parallel within the same message**. Each Agent configuration:
- `subagent_type`: `general-purpose`
- `run_in_background`: `true`
- `team_name`: `{company-name}-newspulse`
- `name`: the corresponding role name (company-event-scout / regulatory-watcher / industry-peer-analyst / sentiment-tracker)

Prompt template for each Agent:

```
You are the "{role name}" on the {company name} News Pulse team, responsible for scouting the {scouting dimension} dimension over the past {N} days.

Time window: {start date} ~ {today's date}
Stock movement context: {movement info provided by user, or "No specific movement — routine check" if none}
Information availability rating: {A/B/C}

Please complete Task #{task number}: {task subject}

Specific scouting requirements:
{task description content}

**Scouting methods**:
- Prioritize WebSearch for time-sensitive queries (add date or "recently", "latest", "2026" to keywords)
- Use WebFetch to read original sources in detail for key events (announcement text, earnings reports, regulatory filings)
- Apply "independent source verification" to each event — rumors require at least 2 independent sources
- **Do not be misled by clickbait**: if a headline contradicts the article body, annotate it as "misleading headline"

**Output format (important)**:
1. **Core findings**: 3-5 most critical events, 1-2 sentences each
2. **Full event timeline table** (reverse chronological order):
   | Date | Event | Source | Relevance to stock movement | Persistence |
3. **Attribution conclusion for this dimension**: Based on scouted events, answer "Can this dimension explain the stock price movement? Confidence level?"
4. **Data gap declaration**: What information was not found, what is questionable, what requires more disclosures
5. Strictly distinguish "facts" from "speculation"; follow the CLAUDE.md objectivity principles

**Upon completion**:
1. Use TaskUpdate to mark the task as completed
2. Send the full scouting report to team-lead via SendMessage (type: "message", recipient: "team-lead")
```

### Step 6: Track Progress in Real Time

- Each time a scouting report arrives, show the user the 3 core findings from that dimension
- Wait for all 4 reports to arrive
- Once all 4 are in, send a shutdown_request to the 4 Agents via SendMessage

### Step 7: Team-Lead Synthesizes Attribution

Aggregate the 4 scouting reports and output a **movement attribution report** (not a research report — the focus is on "judgment"):

---

#### 1. One-Sentence Attribution
> Use one paragraph (30-60 words) to state: the primary cause + secondary cause of this stock price movement + nature judgment (value event / sentiment swing / unknown)

#### 2. Full Event Timeline (merged across 4 dimensions)

Reverse chronological order, merging events from all dimensions:

| Date | Dimension | Event | Source | Attribution Weight |
|------|-----------|-------|--------|-------------------|
| 2026-04-30 | Company | XX | Link | 🔴 High |
| 2026-04-29 | Industry | XX | Link | 🟡 Medium |
| 2026-04-28 | Sentiment | XX | Link | ⚪ Low |

Weight legend: 🔴 High (sufficient to explain the movement on its own) / 🟡 Medium (partial contributor) / ⚪ Low (background noise)

#### 3. Movement Attribution Table

| Candidate Explanation | Evidence | Counter-evidence | Confidence | Persistence |
|-----------------------|----------|-----------------|------------|-------------|
| Example: earnings miss | Revenue 5% below expectations, gross margin declined | One-time factor with management explanation | High | Short-term 1-2 weeks |
| Example: industry beta | Peers down 8% in same period | This stock fell significantly more than the sector | Medium | In sync with industry |

#### 4. Nature Judgment (Core Conclusion)

Check one:

- [ ] **Value event**: A real fundamental change occurred (earnings, moat, management, endgame) — investment thesis needs review
- [ ] **Sentiment / technical swing**: No fundamental change — driven by flows / sentiment / beta; treat as opportunity or noise
- [ ] **True cause unknown**: Cannot find any event that matches the magnitude of the price movement — **this is the most dangerous conclusion**; either the market is front-running something (insider / pre-positioning), or we are missing an information source
- [ ] **Mixed**: Partial value event + partial sentiment amplification

#### 5. Per-Dimension Scouting Summary

3-5 most important findings per dimension + that dimension's attribution contribution.

#### 6. Action Recommendations

| Action | Recommended? | Rationale |
|--------|-------------|-----------|
| Trigger investment thesis review (`/thesis-tracker`) | | |
| Trigger deep earnings read (`/earnings-review`) | | |
| Trigger management review (`/management-deep-dive`) | | |
| Position adjustment (add / trim / hold) | | For reference only — final decision is the user's |
| Monitor only | | |

#### 7. Tracking Checklist for the Next 7-30 Days

- [ ] Upcoming disclosure 1 (e.g. 5/15 earnings call)
- [ ] Metric to track 2
- [ ] Key observation signal 3

#### 8. Information Gap Declaration

Honestly list unresolved questions from this scouting session, information that could not be found, and items awaiting further disclosure. **Label "uncertain" rather than filling gaps with speculation**.

---

### Step 8: Save the Report

Write to `reports/{company name}/{company name}-news-{YYYYMMDD}.md`. If the `reports/{company name}/` directory does not exist, create it (indicating no research reports have been filed for this company yet).

### Step 9: Clean Up the Team

Use TeamDelete to clean up team resources.

## Core Principles

1. **Speed over completeness** — the core value of this skill is delivering an attribution judgment within 10-15 minutes; do not fall into deep analysis (that is other skills' responsibility)
2. **Attribution over enumeration** — finding events is easy; the hard part is judging "which event is commensurate with this stock price movement". Subtract, do not add
3. **Honest about "unknown"** — when the primary cause cannot be found, explicitly write "true cause unknown". This is more valuable than forcing a causal chain (the market may be front-running negative news)
4. **No predetermined stance** — do not lean toward "this is just sentiment noise, no big deal" because you hold a position. Write wherever the evidence points
5. **Distinguish "catalyst" from "coincidence"** — events that happen at the same time are not necessarily the primary cause of the movement; check whether the impact magnitude matches
6. **Respect information availability** — a Grade C company may simply have no news to find; this conclusion must be stated explicitly
7. **Follow `CLAUDE.md` objectivity principles** — attach data sources to all judgments; distinguish facts from opinions
8. **Do not make decisions for the user** — provide attribution and a list of action recommendations, but buy/sell decisions belong to the user
