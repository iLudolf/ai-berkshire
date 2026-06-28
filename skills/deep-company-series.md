# Deep Company Series: 8 Long-Form Articles to Deconstruct One Company

Write an 8-article deep-dive series for $ARGUMENTS, intended for public publication on platforms such as WeChat Official Account or Video Account. **The core IP is not "writing well" — it's "revising rigorously" — 99% of financial articles violate the fact-checking standards in this skill**.

Reference sample: `reports/Tencent/Understanding-Tencent/`

---

## I. When to Use This Skill

The user wants to conduct "textbook-level" deep research on a company and publish it publicly as a **long-form series**. This is distinct from a single research report:
- 8 articles, approximately 120,000 words, covering a complete loop from cognitive reset to decision framework
- Each article stands alone (suitable for individual sharing), yet threads a consistent valuation / management / price-target thesis throughout
- Written for readers "willing to spend 90 minutes truly understanding a company" — not for brokerage clients

**Scenarios where this skill is NOT appropriate**: single-company research reports, quarterly earnings reviews, industry research — use `/investment-research`, `/earnings-review`, `/industry-research` for those.

---

## II. Series Article Template (8 Articles)

| # | Article Title Template | Core Question | Word Count |
|---|----------------------|---------------|------------|
| 01 | You Think You Understand X — You Don't | Cognitive reset: debunk 3 common misconceptions | 4,000–5,000 |
| 02 | X's Economic Moat — `<business essence in one sentence>` | How deep is the moat? Will it still exist in 5 / 10 years? | 6,000–8,000 |
| 03 | X's Biggest Profit Engine — `<most profitable business unit>` | What is the core business, and why can it persist? | 6,000–8,000 |
| 04 | The Hidden Company on X's Balance Sheet — `<hidden assets>` | Investment portfolio / subsidiaries / hidden value | 8,000–10,000 |
| 05 | In the Age of AI (or Current Narrative), Is X a Winner or Loser? | Era variable: break down AI impact by business segment | 8,000–10,000 |
| 06 | Deconstructing X's Financials the Buffett Way | Financial deep-dive: gross margin / FCF / ROE / SBC | 8,000–10,000 |
| 07 | `<Management quote>` — Is X's Management Worth Trusting? | Capital allocation discipline + integrity test + succession | 8,000–10,000 |
| 08 | At What Price Is It Worth Buying, and What Signal Demands a Sell? (Series Finale) | DCF three-scenario + red-line checklist + position sizing framework | 10,000–12,000 |

Include one `00-series-overview.md` as a table of contents / index — not for publication.

---

## III. Writing Style Guidelines

### Tone

- **Direct, sharp, no filler** — lead with a number or a contrarian conclusion in the very first sentence
- **Value investing framework** — weave in Buffett / Munger / Duan Yongping / Li Lu perspectives (but do not pile on quotes)
- **No predetermined stance** — present data first, then reason through logic, then draw conclusions
- **Present both sides** — every core judgment must include a "but on the other hand..." counterargument
- **WeChat-compatible opening** — the first 18–20 characters must stand on their own (mobile preview)

### Banned Words

| Banned | Reason | Replacement |
|--------|--------|-------------|
| Obviously / inevitably / certainly | Subjective absolutism | Data shows / evidence indicates |
| I think / I feel | Subjective framing | Delete or replace with "per this framework" |
| Textbook-level / masterstroke | Clickbait praise | Describe the specific facts |
| Severely mismatched / severely undervalued | Strong subjective language | Give a specific discount percentage |
| Perfect / flawless | One-sided judgment | Add a counterpoint observation |

### Title Style

- Use **contrasting numbers** or **contrarian conclusions** as hooks (e.g., "15 Years, 7 Challenges, All Failed", "Annual Salary of $4.292M Equals 0.0017% of Net Income")
- Subtitles should be neutral and summarize the content ("— `<core judgment>`")
- **Avoid clickbait comparisons**: "the little Buffett", "China's version of X", "GOAT" — all off-limits
- Use terminology familiar to professional readers ("Berkshire" not "Buffett", prefer company names over personal names)

---

## IV. Rigorous Fact-Checking Checklist (Core IP)

### "False Precision" Traps to Watch for Before Writing

1. **Probability-weighted expected value**: Calculations like `30% × A + 50% × B + 20% × C = expected +X%` are almost always garbage — probability assignments are purely subjective, giving readers a false sense of precision. **Only list scenarios + trigger conditions + directional outcomes; do not calculate weighted expectations**.
2. **Third-party MAU / market share estimates**: Data from QuestMobile, Qimai, CBNData, etc. vary enormously by methodology (the same time point can differ 2–3×). **Only use the two most credible sources as anchors; treat others as qualitative descriptions**.
3. **Linear extrapolation of historical growth**: `2025: +33% × 5-year CAGR → 2030: X` is financial-illiteracy forecasting. **Use scenario assumptions + high/low ranges + clearly label as non-committal**.
4. **Undisclosed ownership stakes**: Ownership stakes in unlisted companies like ByteDance or Halti **have never been publicly disclosed**. **Give a range, label as "unknowable"**.
5. **Strong single-cause attribution**: Competitor failure = caused by X. List multiple causes; **this article does not assign single-cause attribution**.

### 7 Checks to Run During Revision

```
□ 1. Cross-article number consistency: total market cap, Non-IFRS net income, key ownership % — aligned across all 8 articles
□ 2. Accounting basis labeling: Non-IFRS / GAAP / Non-IFRS-SBC / FCF — clarify which is used throughout
□ 3. Double-counting scan: already-consolidated subsidiaries must not appear in "investment portfolio"; SOTP must not double-count
□ 4. Fairness in peer comparison: do not use "core business PE (ex-cash + portfolio)" vs "peer PE (not ex)" 
□ 5. Remove all probability-weighted figures: see above
□ 6. Soften all absolute language: grep "obviously|inevitably|severely|textbook|perfect"
□ 7. Third-party data sourcing: every non-earnings-report data point followed by "(Source: X)"
```

### Known Hard-Error Risks

List **known hard-error risks** before writing:
- Historical return multiples: must use cumulative-cost basis (e.g., Riot 33× not 58×)
- Ownership stakes: must check latest Futu / earnings report disclosures (e.g., Tencent holds 1.5% of Meituan, not 6.4%)
- "Dividend-in-specie" accounting: treated as deemed disposal gain, recognized on declaration date per IFRIC 17 (e.g., JD.com in 2021, Meituan in 2022 but small amount)
- Total share count can rebound: SBC grants concentrated at year-start can temporarily increase share count

---

## V. Execution Workflow

### Phase 1: Research (Complete Before Writing Articles 01–02)

1. Read the company's annual reports for the past 5 years and latest quarterly report
2. Read at least 3 independent sell-side research reports (identify consensus + contrarian views)
3. Use `/investment-team` or `/investment-research` to generate an internal research draft first
4. Confirm the core thesis for all 8 articles with the user (to avoid finding out the direction was wrong after writing)

### Phase 2: Writing (Write in order from 01 → 08; do not skip)

- After completing each article, save to `reports/{CompanyName}/Understanding-{CompanyName}/0X-XX.md`
- Do not push to GitHub immediately — wait for user review
- Revise based on user feedback
- Only `git push` after revisions are complete

### Phase 3: Cross-Article Consistency Scan (After All 8 Articles Are Complete)

Dispatch an Explore agent to scan all 8 articles in parallel and check:
1. Whether the same numbers (market cap, net income, ownership %) are consistent across articles
2. Whether the same terms (FBS, SBC, Non-IFRS) are explained upon first appearance
3. Cross-references: whether "see Article 06" in Article 02 actually corresponds
4. Whether key-takeaway recaps match the numbers in the main body

### Phase 4: Final Check Before Publication

```bash
# Must run local grep before pushing (per ai-berkshire privacy rules)
grep -r "linxuan\|/Users/\|<user company alias>" reports/ | head
```

Only proceed with `git pull --rebase && git commit && git push` after confirming clean.

---

## VI. Revision Handling Workflow

When the user provides revision feedback, handle it in this order:

### 1. Verify Facts First (Do Not Edit Immediately)

If the user says "data point X is wrong," first cross-validate using Bash/Read to find the original source:
- Check earnings reports / financial reports for the same company in the ai-berkshire project
- Check Futu / official disclosures
- Present a three-way comparison: "what user says vs. what I found vs. what I previously used"

### 2. Determine Revision Level

| Level | Type | Action |
|-------|------|--------|
| 🔥 Hard error | Wrong number, wrong attribution, wrong accounting basis | Must fix — no hesitation |
| ⚠️ Subjectivity | Strong subjective language, absolutism, clickbait comparisons | Soften or remove |
| 🔬 Granularity | Source labeling, methodology clarification | Lower priority — balance against readability |
| ❓ Unreliable | Third-party estimates with large variance | **Deleting is safer than editing** (per user instruction) |

### 3. Post-Revision Linkage Check

Before fixing one place, ask "where else does this number / concept appear?" For example:
- Changed total market cap → update linked PE / core business PE / discount / FCF Yield across the entire series
- Changed ownership % → update TOP 10 ranking + historical ownership table + reduction-in-stake list
- Changed terminology basis → update first-occurrence definition + all subsequent references + key-takeaway recaps

### 4. Report Immediately After Pushing

```
Push successful (commit hash).
[N] revision(s) summary [with table]:
- What was changed
- What was changed as a linked update
- What was not yet changed

Awaiting further instructions.
```

---

## VII. What This Skill Does NOT Do

- **Does not make investment decisions on behalf of readers** — all articles end with "this does not constitute investment advice"
- **Does not predict stock prices** — only provides "scenarios + trigger conditions"
- **Does not calculate "probability-weighted annualized return"** — subjective probability assignments mislead readers
- **Does not write "Big-Name Investor X also holds this"** — using others' positions to endorse your own judgment is anti-value-investing
- **Does not require all 8 articles to be written** — if a given article lacks sufficient standalone content (e.g., a company's management is not particularly noteworthy), merge it into another article or reduce the total count

---

## VIII. Compliance and Privacy

- All public reports **use only public information** (earnings reports, official disclosures, sell-side research reports, reputable third-party institutions)
- Do not use any **user personal information** (company aliases, internal IM conversations, undisclosed position information)
- Before pushing, must run grep to scan for `linxuan` / `/Users/` / user company aliases and other private fields (see `~/.claude/projects/-Users-linxuan/memory/feedback_privacy_upload.md`)
- Public bylines follow the user's multi-identity strategy — do not mix

---

## One-Line Summary

**The core capability for writing an "Understanding X Series" is not writing well — it's revising rigorously** —
89% of long-form financial articles fail due to false-precision numbers, subjective probability-weighted expectations, and absolutist language. This skill exists to flag all those pitfalls: avoid them before writing, and sweep them clean after.
