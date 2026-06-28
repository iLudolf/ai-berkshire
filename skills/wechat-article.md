# WeChat Public Account Article: Author-Editor-Reader Three-Agent Collaboration

Conduct in-depth research on $ARGUMENTS and produce a WeChat public account article ready for direct publication. Three agents each play a distinct role: the author writes a deep-dive draft, the editor refines structure and expression, and the reader reviews the piece from the target audience's perspective.

**Supported input formats**: Topic descriptions, for example: `Explainer on large model OPD technology`, `Breakdown of the Qwen3 technical report`, `Why Buffett doesn't buy tech stocks`

---

## Design Philosophy

A great WeChat article must satisfy three dimensions simultaneously:
1. **Depth** — worth the time it takes to read (the author's responsibility)
2. **Readability** — clear structure, good pacing, doesn't drive readers away (the editor's responsibility)
3. **Actually understandable** — the target reader won't give up halfway (the reader's responsibility)

Solo writing easily becomes self-indulgent — the writer thinks it's clear, but readers can't follow it. The essence of three-agent collaboration is **forcing the introduction of external perspectives**.

---

## Phase One: Research and Material Collection

### Step 1: Define the Article's Positioning

Before writing, confirm the following (proactively ask the user if not specified):

| Dimension | Needs Confirmation | Default |
|------|---------|--------|
| **Target audience** | Level of technical background | Some technical background but not a domain expert |
| **Article depth** | Popular science / mid-depth / hardcore | Mid-depth (formulas included but clearly explained) |
| **Article length** | Word count range | 3,000–4,000 words |
| **Source materials needed** | PDF / diagrams required | Yes |
| **Writing style** | Formal / conversational / sharp | Conversational (like writing for a smart friend) |

### Step 2: In-Depth Research

Use the Agent tool to **simultaneously** launch 2–3 research agents to gather sufficient material:

**Research Agent A: Core Content Research**
- For paper breakdowns: download the paper PDF, extract core contributions, key figures, and experimental results
- For technical topics: search for the latest developments, key papers, and technical details
- For business/investment topics: search for the latest data, industry reports, and competitive landscape

**Research Agent B: Industry Context and Applications**
- Search for real-world adoption of the technology/topic
- Which companies are using it? What results are they seeing?
- Latest development trends and milestone events

**Research Agent C (optional): Competitor / Comparative Research**
- Comparisons with similar methods/products
- Historical development trajectory
- Future evolution directions

### Step 3: Organize the Material Framework

Once all research agents are done, produce:
1. **Core thesis** (summarize the article's central message in one sentence)
2. **Key data points** (3–5 most impactful data points)
3. **Figure checklist** (which figures are needed, and where do they come from)
4. **Article outline** (titles and core content for 6–8 sections)

---

## Phase Two: Author Agent Writes the First Draft

Use the Agent tool to launch the **Author Agent** with detailed writing instructions.

### Author Agent Prompt Template

```
You are a deep technical writer (Author Agent) tasked with writing a WeChat public account article.

## Target Audience
{Reader profile confirmed in Step 1}

## Writing Style Requirements
- Write entirely in Chinese; avoid mixing in English (give the English term the first time a technical term appears, then use the Chinese going forward)
- Like a technical explainer written for a smart friend, not an academic translation
- Use analogies to aid understanding, but keep them apt and non-clichéd
- Key formulas/data should be included, but each must come with a plain-language explanation
- No emojis
- Paragraphs no longer than 4 lines (WeChat reading environment)

## Core Content
{Organized materials, data, and arguments}

## Article Structure Requirements
1. **Opening (first 3 paragraphs)**: Must have a strong hook — open with impactful data or a counterintuitive conclusion; do not open with a gentle analogy
2. **Background**: Why does this matter? What problem does it solve?
3. **Core content (2–3 sections)**: This is where technical depth lives, but every technical point must have a "plain-language translation"
4. **Evidence/case studies**: Let data and examples do the talking — no vague generalizations
5. **Industry impact/outlook**: What does this mean for the industry?
6. **Closing**: End with a shareable, punchy judgment that works as a standalone screenshot

## Figure Requirements
- For paper breakdown articles: extract original figures directly from the PDF and insert them with `![description](relative-path)` — no `[Figure X: description]` placeholders
- Extraction method: use pdftoppm to render PDF pages as high-resolution PNGs (at least 900 DPI), then crop target chart regions with PIL
- Each image must be at least 500 KB to ensure high resolution
- Store all images under `assets/{topic-slug}/`
- For non-paper articles: if figures are needed, search and download appropriate images and insert them directly

## Formula Requirements
- All math formulas must use LaTeX format: inline with `$...$`, standalone with `$$...$$`
- Do NOT write formulas as plain text (e.g., `> D_KL(P || Q) = ...`) — use LaTeX rendering format
- Every formula must still be followed by a plain-language explanation

Please write a complete first draft of approximately {target word count} words.
```

### After the Author Agent Finishes

Check that the draft file has been generated, then read through the full text to confirm completeness.

---

## Phase Three: Editor Agent + Reader Agent Parallel Review

Once the first draft is complete, use the Agent tool to launch the Editor Agent and Reader Agent **in the same message**.

### Editor Agent Prompt Template

```
You are a senior WeChat editor (Editor Agent). Please conduct a careful review and refinement of the following article.

## Review Criteria
1. **Title**: Would it attract clicks in a WeChat Moments feed? Would it get truncated (over 30 characters)?
2. **Opening**: Do the first 3 paragraphs retain the reader? Is the hook strong enough?
3. **Structure**: Is the logic chain smooth? Are there any jumps or gaps?
4. **Balance of depth and readability**: Are the formula/technical sections truly accessible? Any places that pretend to be simple but don't actually explain things?
5. **Pacing**: Are any paragraphs too long? Is the length of each section appropriate?
6. **Figures**: Are images actually embedded (not placeholders)? Do they appear at the moment the reader most needs visual support?
7. **Closing**: Does it have viral potential? Would readers want to share it after finishing?

## Full Article
{Complete first draft}

## Output Format
1. Overall assessment (3–5 sentences)
2. Title revision suggestions (provide 2–3 alternatives)
3. Section-by-section revision suggestions (specific "original text → suggested revision" comparisons)
4. The 3 most critical improvements
```

### Reader Agent Prompt Template

```
You are a {target reader profile} (Reader Agent). Please review the following article from the reader's perspective.

## Your Background
{Specific description of the target reader's knowledge level and reading habits}

## Full Article
{Complete first draft}

## Please answer the following questions
1. After reading the first 3 paragraphs, would you keep reading? Why?
2. Which parts are "hard to follow" or "require re-reading to understand"? Identify the exact sentences.
3. Did you understand the technical/formula sections? Did the plain-language explanations help?
4. Are the core analogies apt? Do you have better alternatives?
5. Too long or too short? Where would you lose patience?
6. After finishing, can you summarize the article's core point in one sentence?
7. Would you share this article? What would you say when sharing it?
8. Are there questions you wanted answered that the article didn't cover?
```

---

## Phase Four: Final Draft

### Step 1: Synthesize Feedback from Both Agents

Focus on the following high-frequency issues:

| Issue Type | Common Editor Feedback | Common Reader Feedback | How to Handle |
|---------|------------|------------|---------|
| Weak opening | Hook not strong enough | No motivation to continue past paragraph 3 | Rewrite opening with data or a counterintuitive conclusion |
| Technical section drives readers away | Formulas too dense | A section requires 3 re-reads | Remove formulas or visualize them; add a more intuitive analogy |
| Sluggish pacing | A section is too long | Lost patience at a specific point | Merge or cut (especially repeated technical explanations in the second half) |
| Weak closing | Lacks viral potential | Won't share | Rewrite as a single shareable, screenshot-worthy judgment |
| Conceptual jumps | Logic has gaps | "Suddenly lost the thread here" | Add transition sentences or background explanations |

### Step 2: Execute Revisions

Rewrite the article based on the feedback. Core revision principles:

1. **Issues flagged by both editor and reader must be fixed**
2. **Issues flagged only by the editor should generally be fixed** (the editor's professional judgment is usually accurate)
3. **Issues flagged only by the reader should be addressed case by case** (reader feedback reflects real experience, but not every comment needs a response)
4. **When they conflict, lean toward the reader** (the editor pursues perfection, but reader experience is the ultimate standard)

### Step 3: Extract Figures

For paper breakdown articles, complete figure extraction before finalizing:

1. **Render**: `pdftoppm -png -r 900 -f {page} -l {page} paper.pdf /tmp/page` (start at 900 DPI; if the image is under 500 KB, increase to 1200 or 1500 DPI)
2. **Locate**: First render the full page at 150 DPI, visually confirm pixel coordinates of each chart
3. **Crop**: Use PIL to crop by coordinates, save with `compress_level=1`, ensure each image is ≥ 500 KB
4. **Store**: Save to `assets/{topic-slug}/`, named `fig{number}-{description}.png`
5. **Embed**: Reference in the article with `![description](../../assets/{topic-slug}/fig{number}-{description}.png)`

### Step 4: Produce the Final File

Save the final draft as a .md file, with the original paper/source links appended at the end:

```markdown
**Original Paper:**
- arXiv: {link}
```

---

## File Naming and Storage

| Type | Path | Naming Format |
|------|------|---------|
| Technical topic | `reports/AI-Industry-Research/` | `WeChat-{topic-keyword}-{YYYYMMDD}.md` |
| Investment topic | `reports/{company-name}/` | `{company-name}-WeChat-{YYYYMMDD}.md` |
| General topic | `reports/` | `WeChat-{topic-keyword}-{YYYYMMDD}.md` |

---

## Writing Red Lines

1. **Do not fabricate data.** All cited data must have a source; if it can't be found, label it "estimated."
2. **Do not use AI-speak.** Banned phrases: "Let's take a look together," "It's worth noting that," "It must be said," and similar filler.
3. **Do not over-promise.** Technical articles must not use "groundbreaking" or "revolutionary" — let the data speak.
4. **Formulas must have plain-language companions.** Every formula must be followed by a paragraph that says "In plain terms, this means…"
5. **Formulas must use LaTeX.** `$$...$$` format — no plain-text formulas.
6. **Figures must actually be embedded.** For paper breakdowns, extract high-resolution originals from the PDF (≥ 500 KB); `[Figure X]` placeholders are forbidden.
7. **Table annotations must be precise.** Use accurate definitions when describing concepts — not vague verb phrases (e.g., "text sourced from the teacher model" not "text that learns from the teacher").
8. **Analogies must be consistent throughout.** Use one primary analogy for the entire article — do not introduce a new analogy in each section.
9. **The closing must have viral potential.** The final sentence must be worth screenshotting and sharing on its own.
