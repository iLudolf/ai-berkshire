---
name: deep-company-series
description: "AI Berkshire skill: Deep Company Series: 8 long-form articles to dissect one company. Source: skills/deep-company-series.md."
---

## Codex adapter note

This skill is generated from `skills/deep-company-series.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# Deep Company Series: 8 Long-Form Articles to Dissect One Company

Write an 8-article deep-dive series for $ARGUMENTS, to be published on public channels such as WeChat Official Account / Video Account. **The core IP is not "writing well" — it's "editing rigorously" — 99% of financial articles violate this skill's fact-checking standards**.

Reference sample: `reports/Tencent/Understanding-Tencent/`

---

## I. When to Use This Skill

The user wants to conduct "textbook-level" deep research on a company and publish it publicly as a **long-form series**. This is distinct from a single research report:
- 8 articles totaling ~120,000 words, forming a complete loop from cognitive reset to decision framework
- Each article stands alone (suitable for individual sharing), but runs through a unified valuation / management / price judgment
- Written for readers "willing to spend 90 minutes to truly understand a company" — not for brokerage clients

**Scenarios where this skill is NOT appropriate**: single research reports, earnings commentary, industry research — use `/investment-research`, `/earnings-review`, `/industry-research` for those.

---

## II. Series Article Template (8 Articles)

| # | Title Template | Core Question | Word Count |
|---|---------------|--------------|-----------|
| 01 | You Think You Understand X — You Don't | Cognitive reset: debunking 3 common misconceptions | 4,000-5,000 |
| 02 | X's Economic Moat — `<business essence in one sentence>` | How deep is the moat; will it still exist in 5/10 years | 6,000-8,000 |
| 03 | X's Biggest Profit Engine — `<most profitable business>` | What the core business is and why it can sustain | 6,000-8,000 |
| 04 | The Hidden Company Buried in X's Balance Sheet — `<hidden asset>` | Investment portfolio / subsidiaries / hidden value | 8,000-10,000 |
| 05 | In the Age of AI (or Current Narrative), Is X a Winner or Loser | Time variable: break down AI impact by business segment | 8,000-10,000 |
| 06 | Dissecting X's Earnings Report the Buffett Way | Financial depth: gross margin / FCF / ROE / SBC | 8,000-10,000 |
| 07 | `<Management quote>` — Is X's Management Worth Trusting | Capital allocation discipline + integrity test + succession | 8,000-10,000 |
| 08 | At What Price Is It Worth Buying, and What Signals Mean You Must Sell (Series Finale) | DCF three scenarios + red line list + position framework | 10,000-12,000 |

Add a `00-series-overview.md` as a table of contents — not for publication.

---

## III. Writing Style Standards

### Tone

- **Direct, sharp, no filler** — lead with numbers or counter-intuitive conclusions in the first sentence
- **Value investing framework** — weave in Buffett / Munger / Duan Yongping / Li Lu perspectives (without piling on quotes)
- **No predetermined stance** — present data first, then logic, then conclusions
- **Present both sides** — every core judgment must include a "but on the other hand..." counter-argument
- **WeChat-friendly format** — the first 18-20 characters must stand on their own (mobile preview)

### Prohibited Words

| Prohibited | Reason | Replacement |
|-----------|--------|-------------|
| Obviously / Inevitably / Certainly | Subjective absolutism | Data shows / Evidence indicates |
| I think / I feel | Subjective tone | Delete or replace with "Under this framework" |
| Textbook-level / Stroke of genius | Clickbait praise | Describe specific facts |
| Severely undervalued / Severely mismatched | Strongly subjective | Give a specific discount percentage |
| Perfect / Flawless | One-sided judgment | Add counter-observations |

### Title Style

- Use **contrasting numbers** or **counter-consensus conclusions** as hooks ("Failed 7 Challenges Over 15 Years", "Annual salary of 42.92 million = 0.0017% of profit")
- Subtitles are neutral and descriptive ("— `<core judgment>`")
- **Avoid clickbait comparisons**: "mini-Buffett", "China's version of X", "GOAT" — avoid all of these
- Use terminology familiar to professional readers ("Berkshire" not "Buffett", company names over personal names)

---

## IV. Rigorous Fact-Checking Checklist (Core IP)

### "False Precision" Traps to Watch Before Writing

1. **Probability-weighted expected values**: `30% × A + 50% × B + 20% × C = expected +X%` — these calculations are almost always garbage. Probability assignments are purely subjective and give readers a false sense of precision. **Only list scenarios + trigger conditions + direction; do not calculate weighted expected values**.
2. **Third-party MAU/market share estimates**: QuestMobile / Qimai / CBNData and similar sources have huge methodology differences (can vary 2-3x at the same point in time). **Only use the two most reliable sources as anchors; describe others qualitatively**.
3. **Linear extrapolation of historical growth**: `2025 +33% × 5-year CAGR → 2030 X` is amateur-level forecasting. **Scenario assumptions + high/low range + not a promise**.
4. **Undisclosed ownership percentages**: Stake in unlisted companies like ByteDance or Halti has **never been publicly disclosed**. **Give a range, label "unknowable"**.
5. **Strong causal attribution**: Competitor failure = caused by X. List multiple causes; **this article does not make single-cause attributions**.

### 7 Checks to Run During Revision

```
□ 1. Cross-article number consistency: total market cap, Non-IFRS net income, key ownership % aligned across the full series
□ 2. Metric labeling: Non-IFRS / GAAP / Non-IFRS-SBC / FCF — which is used where, clearly stated throughout
□ 3. Double-counting scan: already-consolidated subsidiaries not in "investment portfolio"; no double-counting in SOTP
□ 4. Fairness of cross-comparisons: don't compare "core business PE (ex-cash+portfolio)" vs "competitor PE (not ex)"
□ 5. Delete all probability-weighted figures: see above
□ 6. Soften all absolute statements: grep "obviously|inevitably|severely|textbook|perfect"
□ 7. Third-party data source attribution: every non-earnings-report data point followed by "(Source: X)"
```

### Known Hard-Error Risks

Before writing, **list known hard-error risks upfront**:
- Historical return multiples: must use cumulative-investment basis (e.g., Riot 33x not 58x)
- Ownership percentages: must use latest Futu/earnings report data (e.g., Tencent holds Meituan 1.5% not 6.4%)
- "Dividend-in-specie" accounting: treated as disposal gain recognized on declaration date per IFRIC 17 (e.g., JD.com in 2021, Meituan in 2022 but smaller amount)
- Total shares can rebound: SBC granted heavily at year-start can temporarily increase share count

---

## V. Execution Workflow

### Phase 1: Research (Complete Before Writing Articles 01-02)

1. Read the company's annual reports for the past 5 years, plus the latest quarterly report
2. Read at least 3 independent sell-side research reports (find consensus + counter-consensus)
3. Use `/investment-team` or `/investment-research` to generate an internal research draft first
4. Confirm the core thesis of all 8 articles with the user (to avoid finishing and finding the direction was wrong)

### Phase 2: Writing (Write in order 01→08, no skipping)

- Save each article after writing to `reports/{Company Name}/Understanding-{Company Name}/0X-XX.md`
- Do not push to GitHub immediately — wait for user review
- Make revisions after user feedback
- Only `git push` after revisions are complete

### Phase 3: Cross-Article Consistency Scan (After All 8 Articles Are Written)

Deploy an Explore agent to scan all 8 articles in parallel for the following:
1. Whether the same numbers (market cap, net income, ownership %) are consistent across articles
2. Whether the same terms (FBS, SBC, Non-IFRS) are explained on first occurrence
3. Reference integrity: if article 02 says "see article 06," does it actually correspond
4. Whether key takeaways vs. body text numbers are consistent

### Phase 4: Pre-Publication Final Check

```bash
# Must grep locally before pushing (per ai-berkshire privacy rules)
grep -r "linxuan\|/Users/\|<user company alias>" reports/ | head
```

Only proceed with `git pull --rebase && git commit && git push` after confirming clean.

---

## VI. Revision Handling Workflow

When the user provides revision feedback, process in the following order:

### 1. Verify Facts First (Do Not Edit Directly)

If the user says "X data is wrong," first use Bash/Read to cross-validate with source data:
- Check earnings/financial reports for the same company in the ai-berkshire project
- Check Futu / official disclosures
- Provide a three-way comparison: "what the user said vs. what I found vs. what I previously used"

### 2. Classify the Revision Level

| Level | Type | Action |
|-------|------|--------|
| 🔥 Hard error | Wrong number, wrong attribution, wrong metric basis | Must fix, no hesitation |
| ⚠️ Subjective | Strongly subjective words, absolutes, clickbait comparisons | Soften or delete |
| 🔬 Granularity | Source labeling, metric refinement | Lower priority, balance with readability |
| ❓ Unreliable | Third-party estimates with large variance | **Deleting is safer than editing** (per user instruction) |

### 3. Cascade Check After Revision

Before fixing one item, think "where else is this number/concept referenced?" For example:
- Changed total market cap → cascade-update PE / core PE / discount / FCF Yield across the full series
- Changed ownership % → update TOP 10 ranking + historical ownership table + reduction list
- Changed metric definition → update first definition + subsequent references + key takeaways

### 4. Report Immediately After Pushing

```
Push successful (commit hash).
[N] revisions summary [with table]:
- What was changed
- What was cascade-changed
- What has not yet been changed

Awaiting further instructions.
```

---

## VII. What This Skill Does NOT Do

- **Does not make investment decisions for readers** — all articles end with "this does not constitute investment advice"
- **Does not predict stock prices** — only provides "scenarios + trigger conditions"
- **Does not calculate "expected annualized return" weighted values** — subjective probability assignments mislead readers
- **Does not write "X celebrity also holds this"** — using others' positions to endorse your own judgment is anti-value-investing
- **Does not require all 8 articles** — if a particular article lacks sufficient independent content (e.g., management isn't distinctive enough), merge with another article or reduce the count

---

## VIII. Compliance and Privacy

- All public reports **use only public information** (earnings reports, official disclosures, brokerage research, well-known third-party institutions)
- Do not use any **user personal information** (company aliases, internal IM, undisclosed position information)
- Before pushing, must grep `linxuan` / `/Users/` / user company aliases and other private fields (see `~/.claude/projects/-Users-linxuan/memory/feedback_privacy_upload.md`)
- Public attribution follows the user's multi-layer identity strategy — do not mix

---

## One-Line Summary

**The core competency of writing the "Understanding X Series" is not writing well — it's editing rigorously** —
89% of long-form financial articles fail due to false-precision numbers, subjective weighted expected values, and absolute statements. This skill exists to flag all these pitfalls, avoid them before writing, and clean them up after.
