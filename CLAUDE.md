# AI Berkshire — Project Instructions

## Project Overview

A collection of Value Investment Research Skills built on Claude Code. Four Masters framework: Buffett, Munger, Duan Yongping, Li Lu.
**Focus: Brazilian equities (B3) and FIIs (Fundos de Investimento Imobiliário / Brazilian REITs).**
GitHub: iLudolf/ai-berkshire

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
├── Petrobras/                   — All Petrobras (PETR4) research reports
│   ├── Petrobras-research-20260701.md
│   ├── Petrobras-earnings-2025Q4.md
│   └── Petrobras-thesis.md
├── Vale/                        — All Vale (VALE3) research reports
├── MXRF11/                      — All MXRF11 FII research reports
├── real-estate-fii-industry-20260701.md  — Industry reports go in root
├── b3-quality-funnel-20260701.md         — Funnel screening reports go in root
├── portfolio-latest.md                   — Portfolio report goes in root
└── multi-company-checklist-20260701.md   — Multi-company reports go in root
```

## Report Naming Conventions

| Skill | File Naming Format | Example |
|-------|-------------------|---------|
| /investment-team | `{company}/` folder with 4 perspectives + final report | `reports/Vale/final-report.md` |
| /investment-research | `{company}-research-{YYYYMMDD}.md` | `reports/Petrobras/Petrobras-research-20260701.md` |
| /investment-checklist | `{company}-checklist-{YYYYMMDD}.md` | `reports/Itau/Itau-checklist-20260701.md` |
| /industry-research | `{industry}-industry-{YYYYMMDD}.md` (root) | `reports/real-estate-fii-industry-20260701.md` |
| /industry-funnel | `{industry}-funnel-{YYYYMMDD}.md` (root) | `reports/b3-quality-funnel-20260701.md` |
| /private-company-research | `{company}-private-{YYYYMMDD}.md` | `reports/NuBank/NuBank-private-20260701.md` |
| /earnings-review | `{company}-earnings-{period}.md` | `reports/Petrobras/Petrobras-earnings-2025Q4.md` |
| /earnings-team | `{company}/` folder with 4 master perspectives + research draft + final article | `reports/Vale/Vale-earnings-2025Q4.md` |
| /thesis-tracker | `{company}-thesis.md` (long-term maintenance) | `reports/Petrobras/Petrobras-thesis.md` |
| /portfolio-review | `portfolio-latest.md` (root, continuously updated) | `reports/portfolio-latest.md` |
| /management-deep-dive | `{company}-management-{YYYYMMDD}.md` | `reports/Ambev/Ambev-management-20260701.md` |

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
- Currency units must be explicit (BRL / USD) to prevent confusion; FII distributions are always in BRL
- PE/ROE and similar metrics must be calculated precisely using tools/financial_rigor.py
- After finishing a report, proactively ask whether to push to GitHub
