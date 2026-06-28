---
name: wechat-article
description: "AI Berkshire skill: WeChat public account article: Author-Editor-Reader three-Agent collaboration. Source: skills/wechat-article.md."
---

## Codex adapter note

This skill is generated from `skills/wechat-article.md` so Claude Code and Codex users share one canonical workflow.

- Treat `$ARGUMENTS` as the user's request in the current Codex thread.
- When the source mentions Claude-only surfaces such as Task, Agent, WebSearch, Bash, Read, or Write, use the closest Codex capability available in this session: subagents when available, web search when needed, shell commands for local tools, and normal file edits for workspace files.
- Use shared project tools from `tools/` in this repository. Commands that reference `~/ai-berkshire/tools/...` assume the repo is checked out at `~/ai-berkshire`; if needed, prefer the current workspace path.
- Preserve the research quality rules from `AGENTS.md`: cross-check financial data, use exact arithmetic tools for valuation/math, and clearly label uncertainty and source gaps.

# WeChat Public Account Article: Author-Editor-Reader Three-Agent Collaboration

Conduct deep research on $ARGUMENTS and produce a WeChat public account article ready for direct publication. Three Agents each play a distinct role: the Author writes the in-depth first draft, the Editor refines structure and expression, and the Reader reviews from the target audience's perspective.

**Supported input formats**: Topic descriptions, for example: `Explanation of large model OPD technology`, `Qwen3 technical report breakdown`, `Why Buffett doesn't buy tech stocks`

---

## Design Philosophy

A good WeChat article must satisfy three dimensions simultaneously:
1. **Depth** — worth the time it takes to read (Author's responsibility)
2. **Readability** — clear structure, good pacing, not off-putting (Editor's responsibility)
3. **Actually comprehensible** — the target reader won't quit halfway through (Reader's responsibility)

Solo writing easily becomes self-indulgent — the writer thinks it's clear, but readers can't follow. The essence of three-Agent collaboration is **forcing the introduction of an external perspective**.

---

## Phase 1: Research and Material Collection

### Step 1: Define the Article's Positioning

Before writing begins, confirm the following information (if the user has not specified, ask proactively):

| Dimension | What to Confirm | Default |
|-----------|----------------|---------|
| **Target audience** | Technical background level | Some technical background but not a domain expert |
| **Article depth** | Introductory / mid-depth / hardcore | Mid-depth (formulas included but explained clearly) |
| **Article length** | Word count range | 3000–4000 characters |
| **Whether to download the original paper/materials** | PDF/diagrams needed | Yes |
| **Writing style** | Formal / conversational / sharp | Conversational (like writing for a smart friend) |

### Step 2: Deep Research

Use the Agent tool to launch 2–3 research Agents **in parallel** to gather sufficient material:

**Research Agent A: Core Content Research**
- For paper breakdowns: download the paper PDF, extract core contributions, key figures, and experimental results
- For technical topics: search for the latest developments, key papers, and technical details
- For business/investment topics: search for the latest data, industry reports, and competitive landscape

**Research Agent B: Industry Background and Applications**
- Search for industry adoption of the technology/topic
- Which companies are using it? What are the results?
- Latest development trends and milestone events

**Research Agent C (optional): Competing Products / Comparative Research**
- Comparison with similar methods/products
- Historical development timeline
- Future evolution directions

### Step 3: Organize the Material Framework

After all research Agents complete, consolidate:
1. **Core thesis** (summarize in one sentence the central message the article conveys)
2. **Key data** (3–5 most impactful data points)
3. **Diagram checklist** (which figures are needed and where they come from)
4. **Article outline** (titles and core content for 6–8 sections)

---

## Phase 2: Author Agent Writes the First Draft

Use the Agent tool to launch the **Author Agent** and provide detailed writing instructions.

### Author Agent Prompt Template

```
You are a deep technical writer (Author Agent). Write a WeChat public account article.

## Target Audience
{Reader profile confirmed in Step 1}

## Writing Style Requirements
- Pure Chinese expression; avoid mixing Chinese and English (give the English for technical terms on first appearance, then use Chinese thereafter)
- Like a technical explainer written for a smart friend, not a translation of an academic paper
- Use analogies to aid understanding, but make them apt and not clichéd
- Key formulas/data should be included, but each must be explained in plain language
- No emojis
- Paragraphs no longer than 4 lines (WeChat reading environment)

## Core Content
{Organized material, data, and arguments}

## Article Structure Requirements
1. **Opening (first 3 paragraphs)**: Must have a strong hook — open with data impact or a counter-intuitive conclusion; do not open with a mild analogy
2. **Background**: Why does this matter? What problem does it solve?
3. **Core content (2–3 sections)**: This is where technical depth appears, but every technical point must have a "plain language translation"
4. **Evidence/cases**: Let data and cases speak; no empty talk
5. **Industry impact/outlook**: What does this mean for the industry?
6. **Closing**: End with a judgment that has viral potential, suitable for being screenshotted and shared

## Diagram Requirements
- For paper-breakdown articles: images must be extracted from the paper PDF and inserted directly with `![description](relative path)` — do not use `[Figure X: description]` placeholders
- Extraction method: use pdftoppm to render PDF pages as high-resolution PNGs (at least 900 DPI), then use PIL to crop the target chart area
- Each image must be at least 500KB to ensure high resolution
- Store all images in the `assets/{topic-shortname}/` directory
- For non-paper articles: if diagrams are needed, search and download suitable images and insert them directly

## Formula Requirements
- All mathematical formulas use LaTeX format: inline with `$...$`, standalone formulas with `$$...$$`
- Do not write formulas in plain text (e.g., `> D_KL(P || Q) = ...`); always use LaTeX rendering format
- Each formula must still be followed by a "plain language translation"

Please write the complete first draft of the article, approximately {target word count} characters.
```

### After the Author Agent Completes

Check that the draft file has been generated, read the full text, and confirm the content is complete.

---

## Phase 3: Editor Agent + Reader Agent Parallel Review

After the first draft is complete, use the Agent tool to launch the Editor Agent and Reader Agent **in the same message**.

### Editor Agent Prompt Template

```
You are a senior WeChat public account editor (Editor Agent). Please review and refine the following article.

## Review Criteria
1. **Title**: Can it attract clicks in a WeChat Moments feed? Will it be truncated (more than 30 characters)?
2. **Opening**: Can the first 3 paragraphs hold the reader? Is the hook strong enough?
3. **Structure**: Is the logical chain smooth? Are there any jumps or gaps?
4. **Balance of depth and readability**: Are the formula/technical sections truly accessible? Are there places that "pretend to be simple but don't actually explain"?
5. **Pacing**: Are any paragraphs too long? Is the length of each section appropriate?
6. **Diagrams**: Have images actually been inserted (not placeholders)? Do they appear when readers most need visual support?
7. **Closing**: Does it have viral potential? Will readers want to share it after finishing?

## Full Article Text
{Complete first draft}

## Output Format
1. Overall assessment (3–5 sentences)
2. Title revision suggestions (provide 2–3 alternatives)
3. Section-by-section revision suggestions (give specific "original text → suggested revision" comparisons)
4. The 3 most critical improvements
```

### Reader Agent Prompt Template

```
You are a {target reader profile} (Reader Agent). Please review the following article from a reader's perspective.

## Your Background
{Specific description of the target reader's knowledge level and reading habits}

## Full Article Text
{Complete first draft}

## Please Answer the Following Questions
1. After reading the first 3 paragraphs, would you continue reading? Why?
2. Which parts are "incomprehensible" or "require rereading to understand"? Which specific sentences?
3. Did you understand the technical/formula sections? Did the "plain language translations" help you?
4. Are the core analogies in the article apt? Are there better analogies?
5. Too long or too short? Where would you lose patience?
6. After finishing, can you summarize the article's core point in one sentence?
7. Would you share this article? What would you say when sharing it?
8. Are there questions you wanted answered that the article didn't cover?
```

---

## Phase 4: Finalization

### Step 1: Synthesize Feedback from Both Agents

Focus on the following frequently occurring issues:

| Issue Type | Common Editor Feedback | Common Reader Feedback | How to Handle |
|------------|----------------------|----------------------|---------------|
| Weak opening | Hook not strong enough | No motivation to continue after first 3 paragraphs | Rewrite opening with data/counter-intuitive conclusion |
| Technical section is off-putting | Formulas too dense | A section requires 3 re-reads | Remove formulas or convert to diagrams; add more intuitive analogies |
| Sluggish pacing | A section is too long | Lost patience at a certain point | Merge or cut (especially repeated technical explanations in the second half) |
| Weak closing | Lacks viral potential | Would not share | Rewrite as a single screenshottable, shareable judgment |
| Conceptual jumps | Logical gap | "Suddenly couldn't follow" at a certain point | Add transition sentences or background explanations |

### Step 2: Execute Revisions

Rewrite the article based on feedback. Core revision principles:

1. **Issues flagged by both Editor and Reader must be fixed**
2. **Issues flagged only by the Editor should probably be fixed** (the Editor's professional judgment is usually accurate)
3. **Issues flagged only by the Reader should be fixed case by case** (Reader feedback represents real experience, but not every point requires a response)
4. **When they conflict, side with the Reader** (the Editor pursues perfection, but Reader experience is the ultimate standard)

### Step 3: Extract Diagrams

For paper-breakdown articles, diagram extraction must be completed before finalization:

1. **Render**: `pdftoppm -png -r 900 -f {page} -l {page} paper.pdf /tmp/page` (start at 900 DPI; if the image is under 500KB, increase to 1200 or 1500 DPI)
2. **Locate**: first render the full page at 150 DPI and visually confirm the pixel coordinates of each chart
3. **Crop**: use PIL to crop by coordinates, save with `compress_level=1`, ensure each image is ≥ 500KB
4. **Store**: save to `assets/{topic-shortname}/` directory, named `fig{number}-{description}.png`
5. **Insert**: reference in the article with `![description](../../assets/{topic-shortname}/fig{number}-{description}.png)`

### Step 4: Produce the Final File

Save the final draft as an md file, with the original paper/source links appended at the end:

```markdown
**Original paper:**
- arXiv: {link}
```

---

## File Naming and Storage

| Type | Path | Naming Format |
|------|------|--------------|
| Technical topic | `reports/AI-Industry-Research/` | `WeChat-{topic-keyword}-{YYYYMMDD}.md` |
| Investment topic | `reports/{company-name}/` | `{company-name}-WeChat-{YYYYMMDD}.md` |
| General topic | `reports/` | `WeChat-{topic-keyword}-{YYYYMMDD}.md` |

---

## Writing Red Lines

1. **Do not fabricate data**. Cited data must have a source; if it cannot be found, label it "estimated"
2. **Do not use AI-speak**. Banned phrases: "let's take a look together", "it's worth noting that", "it goes without saying", and similar clichés
3. **Do not overpromise**. Technical articles must not say "disruptive" or "revolutionary" — let the data speak
4. **Formulas must be accompanied by plain language**. Every formula must be followed by a "translated into plain terms, this means…" paragraph
5. **Formulas must use LaTeX**. `$$...$$` format; plain-text formulas are prohibited
6. **Diagrams must actually be inserted**. For paper-breakdown articles, extract high-resolution originals from the PDF (≥500KB); placeholders like `[Figure X]` are prohibited
7. **Table bracket annotations must be precise**. Use accurate definitions when describing concepts; do not use vague verb-object phrases (e.g., "text comes from the teacher" rather than "learns the teacher's text")
8. **Analogies must be consistent throughout**. Use one main analogy for the entire article; do not switch to a new analogy in each section
9. **The closing must have viral potential**. The final sentence must be worth being screenshotted and shared on its own
