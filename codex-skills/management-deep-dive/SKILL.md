---
name: management-deep-dive
description: "AI Berkshire skill: Management deep-dive research: buying stock means buying people. Source: skills/management-deep-dive.md."
---

## Codex adapter note

This skill is generated from `skills/management-deep-dive.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Management Deep-Dive Research: Buying Stock Means Buying People

Conduct an in-depth management research on $ARGUMENTS.

**Supported input formats**: `Company name` or `Person name Company name`, e.g.: `Meituan`, `Wang Xing Meituan`, `Jensen Huang Nvidia`

> "Buying stock means buying people. Find the people you trust, and hold for the long term." — Duan Yongping
>
> "To evaluate management, look at what they do when no one is watching." — Buffett

## Design Philosophy

Most investment analysis evaluates management only at a surface level: resume, ownership percentage, compensation. But Buffett spends significant time **having meals and conversations with management**, Li Lu says **his investing is fundamentally investing in people**, and Duan Yongping says **buying stock means buying people**.

This Skill is a **deeper version** of Step 5 (management evaluation) in `/investment-research`. Use this Skill for in-depth research when the management rating in a standard investment research is uncertain (★★★ or below), or when management is the core investment thesis.

AI cannot have dinner with management, but it can accomplish the following through public information:
- **Track whether management's words and actions are consistent** (promises vs. delivery)
- **Analyze the return on every major capital allocation decision**
- **Infer character from decisions made during difficult periods**
- **Cross-validate through employee/merchant/customer feedback**

## Execution Flow

### Step 1: Identify Key Management and Launch Parallel Data Collection

Use WebSearch to confirm the following key individuals:

| Role | Name | Tenure | Background | Shares/Options |
|------|------|--------|------------|----------------|
| CEO/Chairman | | | | |
| CFO | | | | |
| Founder (if not in role) | | | | |
| Actual controller (if different from CEO) | | | | |
| Other key executives | | | | |

**Note**: Distinguish between "who is making decisions" and "whose name is on the title." In some companies the founder has stepped down but remains the soul of the organization (e.g., Huang Zheng at Pinduoduo).

Once key individuals are confirmed, use the Task tool to launch multiple background Agents to collect the following data in **parallel**:
1. Agent 1: CEO public statements and prediction records (shareholder letters, earnings calls, interviews, social media)
2. Agent 2: Capital allocation decision records (M&A, buybacks, dividends, new business investments)
3. Agent 3: Governance structure and compensation (equity structure, related-party transactions, executive pay)
4. Agent 4: Side-channel validation (employee reviews, customer feedback, industry reputation)

### Step 2: CEO Competence Assessment

#### 2.1 Strategic Vision

Search for the CEO's public statements over the past 5 years (shareholder letters, earnings calls, interviews, social media) and extract their judgments on the following:

| Date | CEO Judgment/Prediction | Actual Outcome | Accuracy |
|------|------------------------|----------------|:--------:|
| | "We believe the X market will..." | X market actually... | ✅/❌ |
| | "Our focus over the next 3 years is..." | Actual execution... | ✅/❌ |

**Key questions**:
- Has the CEO made correct calls that were ahead of the market?
- Has the CEO remained calm when everyone else was bullish?
- Is the CEO's understanding of industry trends market-following or independent thinking?

#### 2.2 Execution Ability

| Dimension | Assessment | Evidence |
|-----------|------------|---------|
| Strategy to execution | Did they do what they said? | |
| Organizational capability | Can they attract and retain talent? | |
| Crisis handling | How did they respond when faced with difficulties? | |
| Iteration speed | How quickly did they correct mistakes? | |

### Step 3: Integrity Assessment (Most Important)

**Buffett**: "We look for three qualities: integrity, intelligence, and energy. If they don't have the first, the other two will kill you."

#### 3.1 Promises vs. Delivery Tracking

From the past 3 years of earnings calls, shareholder letters, and public interviews, extract **specific commitments** made by management:

| # | Date | Commitment | Occasion | Delivery Status | Rating |
|---|------|------------|----------|----------------|--------|
| 1 | | "We will achieve profitability in the X business by 2025" | 2024 annual earnings call | | ✅/⚠️/❌ |
| 2 | | "We plan to buy back $X billion" | 2024 shareholder letter | | ✅/⚠️/❌ |

**Delivery rate statistics**:

| Delivery Rate | Assessment |
|:-------------:|------------|
| >80% | Excellent — walks the talk |
| 60-80% | Acceptable — right direction but execution off |
| 40-60% | Concerning — over-promises and under-delivers |
| <40% | Serious problem — not trustworthy |

#### 3.2 Performance During Difficult Periods

Search for major crises/difficulties the company has encountered historically (stock price crash, earnings miss, regulatory shock, intensified competition) and analyze management's response:

| Crisis Event | Date | Management Response | Retrospective Assessment |
|-------------|------|--------------------|-----------------------------|

**Focus on**:
- Did they communicate proactively or avoid the issue?
- Did they attribute to internal causes or blame external factors?
- Did they take the opportunity to do difficult but correct things, or did they choose to please the market short-term?

#### 3.3 Attitude Toward Stakeholders

| Stakeholder | Management Attitude | Evidence | Assessment |
|-------------|---------------------|---------|------------|
| Shareholders | Respectful/Indifferent/Exploitative | | |
| Employees | Well-treated/Exploited/Neglected | | |
| Customers/Users | Customer-centric/Short-term extraction | | |
| Merchants/Suppliers | Fair cooperation/Extreme price pressure | | |
| Regulators/Society | Compliant/Playing the edge | | |

**Li Lu**: "The attitude toward stakeholders determines the long-term vitality of an enterprise. Short-term exploitation can improve efficiency, but long-term it will damage the ecosystem."

### Step 4: Capital Allocation Capability

This is the management capability Buffett values most — **for every dollar earned, how much can management turn it into?**

#### 4.1 Capital Allocation Decision Records

Search for the company's major capital allocation decisions over the past 5 years and evaluate each one:

**M&A Records**:

| Date | Acquisition Target | Amount | Strategic Rationale | Subsequent Return | Score (1-5) |
|------|-------------------|--------|--------------------|--------------------|:-----------:|

**Buyback Records**:

Use `tools/financial_rigor.py verify-valuation` to verify PE and other valuation metrics at the time of buyback and currently.

| Date | Buyback Amount | Average Buyback Price | PE at Time | Retrospective View | Score (1-5) |
|------|---------------|----------------------|:----------:|--------------------|:-----------:|

**Dividend Records**:

| Year | Dividend Amount | Payout Ratio | Concurrent FCF | Sustainable? |
|------|----------------|:------------:|----------------|:------------:|

**New Business Investment**:

| Date | Investment Area | Cumulative Investment | Current Status | Return Assessment | Score (1-5) |
|------|----------------|----------------------|----------------|------------------|:-----------:|

#### 4.2 Capital Allocation Score

| Dimension | Score (1-5) | Notes |
|-----------|:-----------:|-------|
| M&A discipline | | Did they acquire at reasonable prices? How was post-acquisition integration? |
| Buyback timing | | Did they buy back at undervalued prices and stop when overvalued? |
| Dividend reasonableness | | Does the payout ratio match FCF? |
| New business investment | | What is the success rate? How is the stop-loss discipline? |
| Cash management | | Is the cash reserve reasonable? Is there excessive hoarding? |
| **Overall Score** | | |

**Buffett standard**: Ideal management invests decisively when good opportunities arise, actively buys back/pays dividends when there are no good opportunities, and never makes expensive acquisitions.

### Step 5: Governance Structure Assessment

#### 5.1 Equity Structure

| Item | Details | Risk Assessment |
|------|---------|----------------|
| Are there dual-class shares/super-voting rights? | | |
| Founder/controller ownership percentage? | | |
| Is there a VIE structure? | | |
| Are independent directors truly independent? | | |
| Major shareholder's recent buy/sell records? | | |

#### 5.2 Compensation Reasonableness

| Executive | Total Annual Compensation | % of Net Income | vs. Peers | Reasonable? |
|-----------|:-------------------------:|:---------------:|:---------:|:-----------:|

**Focus on**: Does the incentive structure align with long-term shareholder interests? Or does it encourage short-term behavior?

#### 5.3 Related-Party Transactions

| Related Party | Transaction Content | Amount | Fair Price? | Risk Assessment |
|---------------|--------------------:|--------|:-----------:|----------------|

### Step 6: Side-Channel Validation

AI cannot interact face-to-face with management, but it can validate through publicly available side-channel information. **Note**: The following information depends on publicly searchable content and may be incomplete; label information sources and availability.

#### 6.1 Employee Perspective

Search for **publicly searchable** employee reviews such as Glassdoor rating summaries, Zhihu discussions, etc. (platforms requiring login, such as Maimai, should be labeled "users can supplement themselves"):

| Dimension | Rating Trend | Key Feedback |
|-----------|-------------|-------------|
| Company culture | | |
| Management evaluation | | |
| Work intensity | | |
| Compensation satisfaction | | |
| Career prospects | | |

#### 6.2 Customer/Merchant Perspective

Search App Store ratings, consumer complaints, merchant forums:

| Dimension | Rating/Trend | Key Feedback |
|-----------|-------------|-------------|
| Product satisfaction | | |
| Customer service | | |
| Merchant/supplier relations | | |

#### 6.3 Industry Reputation

Search industry forums and social media to understand how peers and industry insiders evaluate this management team.

### Step 7: Scenario Analysis for CEO Departure

**Buffett**: "A great business should be one that even a fool can run — because sooner or later a fool will."

| Question | Answer |
|----------|--------|
| If the CEO left tomorrow, could the company operate normally? | |
| How deep is the existing management team? Is there a clear successor? | |
| Does the company's competitive advantage depend on the CEO personally, or on the organization/systems? | |
| Have historical management transitions been smooth? | |

### Step 8: Output Management Assessment Report

#### Report Structure

```
I. Key Personnel Overview (table)
II. Integrity Assessment
   - Promise delivery rate
   - Performance during difficult periods
   - Attitude toward stakeholders
III. Capability Assessment
   - Strategic vision (prediction accuracy)
   - Execution ability
   - Capital allocation record
IV. Governance Structure
   - Equity structure risk
   - Compensation reasonableness
   - Related-party transactions
V. Side-Channel Validation
   - Employee perspective
   - Customer/merchant perspective
VI. Overall Score and Conclusions
```

#### Overall Score

| Dimension | Weight | Score (1-5) | Weighted |
|-----------|:------:|:-----------:|:--------:|
| Integrity | 35% | | |
| Strategic & execution ability | 25% | | |
| Capital allocation ability | 25% | | |
| Governance structure | 15% | | |
| **Overall Score** | 100% | | |

#### Duan Yongping's "Investing in People" Standard

> Answer the following three questions:
> 1. **Is this person honest?** (Honest, doesn't take advantage of shareholders)
> 2. **Is this person capable?** (Strategic vision + execution + capital allocation)
> 3. **Would you entrust your money to this person for 10 years?**
>
> All three "Yes" = ★★★★★ (5 stars)
> First two "Yes" = ★★★★ (4 stars)
> Only first "Yes" = ★★★ (3 stars)
> First is not "Yes" = ★ (1 star, do not invest)

### Step 9: Save Report

Write the report to `reports/{Company name}-management-{YYYYMMDD}.md`, e.g. `reports/Meituan-management-20260409.md`

---

## Core Principles

- **Integrity is a veto item** — lack of ability can be learned; character flaws cannot be fixed
- **Watch actions, not words** — what management says doesn't matter; what they do is what counts
- **Difficulties reveal the truth** — anyone can be a good CEO in a tailwind; a headwind reveals real skill
- **Capital allocation is the ultimate test** — making money is easy; allocating that money well is hard
- **Don't fall in love with management** — stay objective; even people you admire can make major mistakes
