# AI Berkshire — Project Instructions

## Project Overview

A collection of Value Investment Research Skills built on Claude Code. Four Masters framework: Buffett, Munger, Duan Yongping, Li Lu.
GitHub: xbtlin/ai-berkshire

## Project Structure

```
skills/          — Investment research Skill definitions (.md), copy to ~/.claude/commands/ to use
tools/           — Supporting tools (financial_rigor.py for precise calculations)
reports/         — Investment research report output
assets/          — Images and static assets
```

## Report Directory Structure

All reports are organized by **company name** in individual folders:

```
reports/
├── AI-Industry-Research/        — AI industry chain panoramic research (pinned)
│   ├── AI-Five-Layer-Cake-Industry-Research-20260605.md
│   └── AI-Five-Layer-Cake-WeChat-20260605.md
├── Tencent/                     — All Tencent research reports
│   ├── Tencent-research-20260408.md
│   ├── Tencent-earnings-2025Q4.md
│   ├── Tencent-management-20260409.md
│   └── Tencent-thesis.md
├── Pinduoduo/                   — All Pinduoduo research reports
├── PopMart/                     — All Pop Mart research reports
├── nuclear-power-industry-20260409.md   — Industry reports go in root
├── AI-compute-funnel-20260509.md        — Funnel screening reports go in root
├── AI-rotation-decision-20260509.md     — Theme-level synthesis reports go in root
├── portfolio-latest.md                  — Portfolio report goes in root
└── multi-company-checklist-20260408.md  — Multi-company reports go in root
```

## Report Naming Conventions

| Skill | File Naming Format | Example |
|-------|-------------------|---------|
| /investment-team | `{company}/` folder with 4 perspectives + final report | `reports/Pinduoduo/final-report.md` |
| /investment-research | `{company}-research-{YYYYMMDD}.md` | `reports/Tencent/Tencent-research-20260408.md` |
| /investment-checklist | `{company}-checklist-{YYYYMMDD}.md` | `reports/Tencent/Tencent-checklist-20260408.md` |
| /industry-research | `{industry}-industry-{YYYYMMDD}.md` (root) | `reports/nuclear-power-industry-20260409.md` |
| /industry-funnel | `{industry}-funnel-{YYYYMMDD}.md` (root) | `reports/AI-compute-funnel-20260509.md` |
| /private-company-research | `{company}-private-{YYYYMMDD}.md` | `reports/ByteDance/ByteDance-private-20260408.md` |
| /earnings-review | `{company}-earnings-{period}.md` | `reports/Tencent/Tencent-earnings-2025Q4.md` |
| /earnings-team | `{company}/` folder with 4 master perspectives + research draft + WeChat article + reader review | `reports/Tencent/Tencent-earnings-2025Q4.md` (final WeChat version) |
| /thesis-tracker | `{company}-thesis.md` (long-term maintenance) | `reports/Tencent/Tencent-thesis.md` |
| /portfolio-review | `portfolio-latest.md` (root, continuously updated) | `reports/portfolio-latest.md` |
| /management-deep-dive | `{company}-management-{YYYYMMDD}.md` | `reports/Tencent/Tencent-management-20260409.md` |

## /investment-team File Structure

```
reports/{company}/
├── README.md                              — Research framework overview + core conclusions
├── 01-business-model-analysis-DuanYongping-perspective.md
├── 02-financial-valuation-analysis-Buffett-perspective.md
├── 03-industry-competition-analysis-Munger-perspective.md
├── 04-risk-management-assessment-LiLu-perspective.md
└── final-report.md                        — Team Lead consolidated report
```

## Core Investment Research Principles (Highest Priority)

- **Objective, Objective, Objective** — all investment analysis must be based on facts and data; subjective speculation is strictly prohibited
- Strictly distinguish "facts" from "opinions": facts must be supported by data; opinions must be explicitly labeled as "opinion" or "speculation"
- **No predetermined stance**: do not preset bullish or bearish views; first present data, then reason through logic, then draw conclusions. Conclusions must be naturally derived from data
- Prohibited phrases: "I think", "I feel", "obviously" — replace with "data shows", "evidence indicates", "according to XX source"
- **Present both sides**: every core judgment must include a counter-argument ("on the other hand..."), letting readers weigh for themselves
- Be honest when uncertain: say "uncertain" or "insufficient data" — do not fill uncertainty with speculation
- All skills (investment-team, investment-research, earnings-review, etc.) must follow these principles during execution

## Report Language and Style

- All reports in **English**
- Style: direct, sharp, no filler
- Data must cite sources; key data points require at least 2 source cross-validation
- Estimated values must be labeled "estimated"
- Ratings use ★ symbol (★1–5), no half stars
- Intersperse quotes from Buffett / Munger / Duan Yongping / Li Lu

## GitHub Operations

- Local clone path: `~/ai-berkshire/`
- Remote: `https://github.com/xbtlin/ai-berkshire.git`
- Before pushing: `git pull --rebase origin main` (remote often has new commits)
- Commit messages in English, describe clearly what changed
- Do not push intermediate files (e.g. data_collection.md); only push final reports

## Common Commands

```bash
# Push report to GitHub
cd ~/ai-berkshire
git add reports/xxx.md
git commit -m "Add xxx report"
git pull --rebase origin main
git push origin main
```

## Important Notes

- Market cap must be manually verified: share price × total shares, compare with reported market cap
- Currency units must be explicit (HKD / CNY / USD) to prevent confusion
- PE/ROE and similar metrics must be calculated precisely using tools/financial_rigor.py
- After finishing a report, proactively ask whether to push to GitHub
