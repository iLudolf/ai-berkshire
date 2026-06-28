# AI Berkshire — AI Memory File

> This file records project knowledge, user preferences, and historical decisions accumulated by Claude during collaboration with the user, for reference in future sessions.

## User Profile

- Investment style: Value investing, concentrated high-conviction positions, focus on Chinese internet + consumer + AI
- Research preferences: Direct and sharp with no filler, clear conclusions without hedging both sides, data must be accurate
- Use case: Personal investment decision support, while also promoting this project as an open-source product

## Project Evolution History

### April 7–9, 2026 (First batch of research + framework refinement)

**Completed research:**
1. `/investment-team Pinduoduo` — First complete 4-Agent parallel research, composite score 3.4/5
2. `/investment-checklist` for 7 companies — Moutai, Tencent, Nvidia, Meituan, Pinduoduo, Pop Mart, Kuaishou
3. Master holdings tracker — Buffett/Li Lu/Duan Yongping latest 13F + PDD cost basis analysis
4. Deep re-evaluation of Meituan and 4 other companies (user challenged initial assessments)

**Corrections driven by user feedback:**
- Meituan changed from ❌ to ✅ conditional pass — user pointed out: waiting for profit recovery before buying is too late; 200B RMB couldn't kill it = real economic moat
- Nvidia changed from ❓ to ✅ conditional pass — AI capex still accelerating, Jevons Paradox
- Kuaishou changed from ❓ to ✅ conditional pass — Kling AI underestimated, Sora already shut down

**Key lessons:**
- Don't mechanically apply checklists — exercise independent judgment
- "Wait for profit recovery before buying" is a logical fallacy — stock prices reflect this in advance
- Competitors spent more money but gained no advantage = the best evidence of an economic moat

### Skill System Evolution

**V1 (5 Skills) — covers pre-purchase research:**
- investment-research, investment-team, investment-checklist, industry-research, private-company-research

**V2 (9 Skills) — fills in post-purchase workflow:**
- Added: earnings-review, thesis-tracker, portfolio-review, management-deep-dive
- Fixed through 2 rounds of self-validation: unified paths, complete tool calls, parallel collection, anti-bias mechanisms, quantitative scoring formulas

## Core Project Value Propositions (reflected in README)

1. **Forced conclusions, no hedging** — pass/fail/gray zone, with specific price ranges
2. **Four Masters adversarial perspectives** — not division of labor but mutual challenge, creating genuine tension and conflict
3. **Structured anti-bias mechanisms** — A/B/C information richness, Munger inversion, rapid rejection, anti-consensus
4. **Financial data precision** — Decimal exact calculation, manual market cap verification, multi-source cross-validation
5. **Reproducible research process** — same input → structurally consistent output, supports horizontal comparison and longitudinal tracking
6. **Multi-Agent parallel depth** — 4 Agents each searching + independently analyzing, 4x information volume
7. **Live portfolio validation** — cumulative gain of 1.46M CNY over two years, consistently outperforming the index by 40–50 percentage points

## User Preferences and Work Habits

- **Report language**: Chinese
- **Push to GitHub**: usually requested after research is complete; ask proactively
- **Git operations**: remote often has new commits (user may be making changes elsewhere too); must `git pull --rebase` before pushing
- **Attitude toward errors**: point them out directly, no need to soften. User will challenge AI judgments; at that point, seriously re-evaluate rather than defend
- **No excessive summarizing**: user can see the diff; no need to recap what was done after every operation
- **Research depth**: better to spend time going deep and getting it right than to be quick and rough

## Known Issues and Areas for Improvement

- Some early files in the reports/ directory have non-standard naming (mix of Chinese and underscores); should be unified to English hyphen format going forward
- Some early reports used old naming conventions (Chinese-language filenames); all have since been renamed to English
- The actual coverage of the financial_rigor.py tool needs to be verified during Skill execution
- Output examples in the README are fabricated; should be replaced with excerpts from real reports going forward
