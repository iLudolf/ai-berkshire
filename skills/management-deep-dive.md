# Management Deep Dive: Buying Stocks Means Buying People

Conduct a deep management research on $ARGUMENTS.

**Supported input formats**: `company name` or `person name company name`, e.g.: `Weg`, `Décio da Silva Weg`, `Roberto Campos Neto`

> "Buying stocks means buying people. Find people you trust, then hold for the long term." — Duan Yongping
>
> "When evaluating management, look at what they do when no one is watching." — Buffett

## Design Philosophy

Most investment analyses evaluate management only at a surface level: résumé, ownership stake, compensation. But Buffett spends considerable time **having meals and conversations with management**, Li Lu says **the essence of his investing is investing in people**, and Duan Yongping says **buying stocks means buying people**.

This Skill is a **deep-dive extension** of Step 5 (management evaluation) in `/investment-research`. Use this Skill for in-depth research when the management rating in a standard investment research is uncertain (★★★ or below), or when management is the core investment thesis.

AI cannot have dinner with management, but through public information it can:
- **Track whether management's words and actions are consistent** (promises vs. delivery)
- **Analyze the returns of every major capital allocation decision**
- **Infer character from decisions made during difficult times**
- **Validate indirectly through employee/merchant/customer feedback**

## Execution Workflow

### Step 1: Identify Key Management and Launch Parallel Data Collection

Use WebSearch to confirm the following key individuals:

| Role | Name | Tenure | Background | Shares/Options |
|------|------|--------|------------|----------------|
| CEO / Chairman | | | | |
| CFO | | | | |
| Founder (if not in role) | | | | |
| Actual controller (if different from CEO) | | | | |
| Other key executives | | | | |

**Note**: Distinguish "who makes decisions" from "whose name is on the title." At some companies, the founder remains the soul of the business even after stepping down (e.g., Jorge Paulo Lemann at 3G Capital / Ambev, or the Da Silva family influence at Weg).

After confirming key individuals, use the Task tool to launch multiple background Agents to **concurrently** collect the following data:
1. Agent 1: CEO public statements and forecast record (shareholder letters, earnings calls, interviews, social media)
2. Agent 2: Capital allocation decision record (M&A, buybacks, dividends, new business investments)
3. Agent 3: Governance structure and compensation (equity structure, related-party transactions, executive pay)
4. Agent 4: Indirect validation (employee reviews, customer feedback, industry reputation)

### Step 2: CEO Competency Circle Assessment

#### 2.1 Strategic Vision

Search for the CEO's public statements over the past 5 years (shareholder letters, earnings calls, interviews, social media) and extract their judgments on the following:

| Date | CEO Judgment / Prediction | Actual Outcome | Accuracy |
|------|--------------------------|----------------|:--------:|
| | "We believe market X will..." | Market X actually... | ✅/❌ |
| | "Our focus for the next 3 years will be..." | Actual execution... | ✅/❌ |

**Key questions**:
- Has the CEO ever made correct judgments ahead of the market?
- Has the CEO maintained calm when everyone else was optimistic?
- Is the CEO's understanding of industry trends independent thinking or following the herd?

#### 2.2 Execution Ability

| Dimension | Assessment | Evidence |
|-----------|-----------|----------|
| Strategy to execution | Did they do what they said? | |
| Organizational capability | Can they attract and retain talent? | |
| Crisis management | How did they respond when facing difficulties? | |
| Iteration speed | How quickly did they course-correct after mistakes? | |

### Step 3: Integrity Assessment (Most Important)

**Buffett**: "We look for three qualities: integrity, intelligence, and energy. If someone lacks the first, the other two will kill you."

#### 3.1 Promises vs. Delivery Tracking

From earnings calls, shareholder letters, and public interviews over the past 3 years, extract **specific commitments** made by management:

| # | Date | Commitment | Occasion | Delivery Status | Rating |
|---|------|-----------|----------|-----------------|--------|
| 1 | | "We will achieve profitability in business X by 2025" | 2024 earnings call | | ✅/⚠️/❌ |
| 2 | | "We plan to buy back $X billion" | 2024 shareholder letter | | ✅/⚠️/❌ |

**Delivery rate statistics**:

| Commitment Delivery Rate | Rating |
|:------------------------:|--------|
| >80% | Excellent — says what they do, does what they say |
| 60–80% | Adequate — right direction but execution has gaps |
| 40–60% | Concerning — over-promises and under-delivers |
| <40% | Serious problem — not trustworthy |

#### 3.2 Performance During Difficult Times

Search for major crises/difficulties the company has faced historically (stock price crash, earnings miss, regulatory shock, intensified competition) and analyze management's response:

| Crisis Event | Date | Management Response | Retrospective Assessment |
|-------------|------|--------------------|--------------------------| 

**Watch for**:
- Proactive communication vs. avoidance?
- Attributing causes internally vs. blaming external factors?
- Taking the difficult but right action vs. choosing short-term market appeasement?

#### 3.3 Attitude Toward Stakeholders

| Stakeholder | Management Attitude | Evidence | Rating |
|-------------|--------------------|---------|---------| 
| Shareholders | Respectful / Indifferent / Exploitative | | |
| Employees | Treats well / Exploits / Neglects | | |
| Customers / Users | Customer-centric / Short-term extraction | | |
| Merchants / Suppliers | Fair partnership / Extreme price pressure | | |
| Regulators / Society | Compliant / Operating in gray areas | | |

**Li Lu**: "The attitude toward stakeholders determines the long-term vitality of a business. Short-term exploitation can improve efficiency, but in the long run it damages the ecosystem."

### Step 4: Capital Allocation Ability

This is the management capability Buffett values most — **for every dollar earned, how much can management turn it into?**

#### 4.1 Capital Allocation Decision Record

Search for major capital allocation decisions over the past 5 years and evaluate each one:

**M&A Record**:

| Date | Acquisition Target | Amount | Strategic Rationale | Post-Acquisition Return | Score (1–5) |
|------|-------------------|--------|--------------------|-----------------------------|:-----------:|

**Buyback Record**:

Use `tools/financial_rigor.py verify-valuation` to verify PE and other valuation metrics at the time of buyback and currently.

| Date | Buyback Amount | Average Buyback Price | PE at the Time | Retrospective View | Score (1–5) |
|------|---------------|----------------------|:--------------:|---------------------|:-----------:|

**Dividend Record**:

| Year | Dividend Amount | Payout Ratio | FCF Same Period | Sustainable? |
|------|----------------|:------------:|-----------------|:------------:|

**New Business Investment**:

| Date | Investment Area | Cumulative Investment | Current Status | Return Assessment | Score (1–5) |
|------|----------------|----------------------|----------------|---------------------|:-----------:|

#### 4.2 Capital Allocation Score

| Dimension | Score (1–5) | Notes |
|-----------|:-----------:|-------|
| M&A discipline | | Acquired at a reasonable price? Post-acquisition integration? |
| Buyback timing | | Buying back when undervalued, stopping when overvalued? |
| Dividend appropriateness | | Does payout ratio match free cash flow? |
| New business investment | | Success rate? Stop-loss discipline? |
| Cash management | | Is cash reserve appropriate? Excessive hoarding? |
| **Overall Score** | | |

**Buffett's standard**: Ideal management invests decisively when good opportunities arise, actively returns capital via buybacks/dividends when there are no good opportunities, and never does expensive acquisitions.

### Step 5: Governance Structure Assessment

#### 5.1 Equity Structure

| Item | Details | Risk Assessment |
|------|---------|----------------|
| Dual-class shares / super-voting rights? | | |
| Founder / controlling shareholder ownership %? | | |
| Tag-along rights (tag along) in place for minority shareholders? | | |
| Are independent directors truly independent? | | |
| Recent insider buying/selling by major shareholders? | | |

#### 5.2 Compensation Reasonableness

| Executive | Total Annual Compensation | % of Net Income | vs. Peers | Reasonable? |
|-----------|--------------------------|:---------------:|:---------:|:-----------:|

**Watch for**: Is the incentive structure aligned with long-term shareholder interests? Or does it encourage short-term behavior?

#### 5.3 Related-Party Transactions

| Related Party | Transaction Content | Amount | Arms-Length? | Risk Assessment |
|---------------|--------------------|---------|-----------:|----------------|

### Step 6: Indirect Validation

AI cannot interact face-to-face with management, but can validate through publicly accessible indirect information. **Note**: The following information depends on what is publicly searchable and may be incomplete; annotate the source and availability of information.

#### 6.1 Employee Perspective

Search for **publicly searchable** employee reviews such as Glassdoor rating summaries, LinkedIn discussions, Vagas.com.br reviews, or Reclame Aqui employer mentions (platforms requiring login should be annotated as "user can supplement"):

| Dimension | Rating Trend | Key Feedback |
|-----------|-------------|--------------|
| Corporate culture | | |
| Management evaluation | | |
| Work intensity | | |
| Compensation satisfaction | | |
| Career prospects | | |

#### 6.2 Customer / Merchant Perspective

Search App Store ratings, consumer complaints, merchant forums:

| Dimension | Rating / Trend | Key Feedback |
|-----------|---------------|--------------|
| Product satisfaction | | |
| Customer service | | |
| Merchant / Supplier relations | | |

#### 6.3 Industry Reputation

Search industry forums and social media to understand how peers and industry insiders evaluate this management team.

### Step 7: Scenario Analysis — What Happens If the CEO Leaves?

**Buffett**: "A good business should be able to be run by a fool — because eventually one will."

| Question | Answer |
|----------|--------|
| If the CEO left tomorrow, could the company continue operating normally? | |
| How deep is the existing management team? Is there a clear successor? | |
| Does the company's competitive advantage depend on the CEO personally, or on the organization/systems? | |
| Have historical management transitions been smooth? | |

### Step 8: Output Management Assessment Report

#### Report Structure

```
I.   Key Personnel Summary (table)
II.  Integrity Assessment
     - Commitment delivery rate
     - Performance during difficult times
     - Attitude toward stakeholders
III. Competency Assessment
     - Strategic vision (forecast accuracy)
     - Execution ability
     - Capital allocation record
IV.  Governance Structure
     - Equity structure risks
     - Compensation reasonableness
     - Related-party transactions
V.   Indirect Validation
     - Employee perspective
     - Customer / Merchant perspective
VI.  Overall Score and Conclusion
```

#### Overall Score

| Dimension | Weight | Score (1–5) | Weighted |
|-----------|:------:|:-----------:|:--------:|
| Integrity | 35% | | |
| Strategic & Execution Ability | 25% | | |
| Capital Allocation Ability | 25% | | |
| Governance Structure | 15% | | |
| **Overall Score** | 100% | | |

#### Duan Yongping's "Buying People" Standard

> Answer the following three questions:
> 1. **Is this person honest?** (Truthful, does not take advantage of shareholders)
> 2. **Is this person capable?** (Strategic vision + execution + capital allocation)
> 3. **Would you entrust your money to this person to manage for 10 years?**
>
> All three "Yes" = ★★★★★ (5 points)
> First two "Yes" = ★★★★ (4 points)
> Only the first "Yes" = ★★★ (3 points)
> First one is not "Yes" = ★ (1 point, do not invest)

### Step 9: Save Report

Write the report to `reports/{company-name}-management-{YYYYMMDD}.md`, e.g. `reports/Weg/Weg-management-20260409.md` or `reports/Petrobras/Petrobras-management-20260409.md`

---

## Core Principles

- **Integrity is a veto item** — Lack of ability can be learned; flawed character cannot be repaired
- **Watch actions, not words** — What management says doesn't matter; what they do does
- **Truth is revealed in difficult times** — Anyone looks like a good CEO in a tailwind; real skill shows in a headwind
- **Capital allocation is the ultimate test** — Earning money is easy; allocating it well is hard
- **Don't fall in love with management** — Stay objective; even people you admire can make grave mistakes
