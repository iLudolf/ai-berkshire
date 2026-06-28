# Investment Article: Author-Editor-Reader Collaboration

Write a well-structured investment analysis article on $ARGUMENTS. Three agents each play a distinct role: the author writes a deep-dive draft, the editor refines structure and expression, and the reader reviews the piece from the target audience's perspective.

**Supported input formats**: Topic or company descriptions, for example:
- `Why Petrobras pays extraordinary dividends`
- `FIIs vs. Tesouro Direto: where is the real risk-free?`
- `Earnings breakdown: Vale 2025Q4`
- `Is MXRF11 still worth holding with Selic at 14.75%?`

---

## Design Philosophy

A great investment article must satisfy three dimensions simultaneously:
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
| **Target audience** | Level of financial background | Intermediate retail investor — understands P/L and DY, not a quant |
| **Article depth** | Introductory / mid-depth / expert | Mid-depth (concepts explained, formulas included with plain-language translation) |
| **Article length** | Word count range | 1,500–2,500 words |
| **Language** | Portuguese or English | Portuguese (BR) for Brazilian-focused topics, English for global/comparative topics |
| **Writing style** | Formal / conversational / sharp | Conversational (like explaining to a smart friend who invests) |

### Step 2: In-Depth Research

Use the Agent tool to **simultaneously** launch 2–3 research agents to gather sufficient material:

**Research Agent A: Core Content Research**
- For earnings breakdowns: obtain DFP/ITR from CVM or company RI; extract key figures from Relatório Gerencial (FIIs)
- For thematic topics (e.g., "FII vs. Tesouro"): search for current Selic rate, historical FII DY data, tax rules (IR isento for FIIs), IPCA trend
- For company analysis: Fundamentus, Status Invest, FundsExplorer as primary; CVM filings as verification

**Research Agent B: Competitive / Sector Context**
- How does this topic compare across peers?
- What do other investors / analysts say? (XP Investimentos, BTG Pactual Research, Itaú BBA)
- Historical data for context (DY 3-year trend, P/VP vs. Selic chart, etc.)

**Research Agent C (optional): Counterargument and Risk Research**
- The strongest bear case for the thesis
- What could go wrong? What does the market fear?
- Historical precedents of similar situations

### Step 3: Organize the Material Framework

Once all research agents are done, produce:
1. **Core thesis** (summarize the article's central message in one sentence)
2. **Key data points** (3–5 most impactful numbers with sources)
3. **Article outline** (section titles and core content for 5–7 sections)

---

## Phase Two: Author Agent Writes the First Draft

Use the Agent tool to launch the **Author Agent** with detailed writing instructions.

### Author Agent Prompt Template

```
You are a sharp investment writer (Author Agent) writing a well-structured investment article.

## Target Audience
{Reader profile confirmed in Step 1 — e.g., "intermediate Brazilian retail investor familiar with DY, P/VP, and Selic but not with CRI indexation structures"}

## Language and Style
- Language: {Portuguese (BR) / English}
- Conversational but precise — like writing for a smart investor friend, not an academic journal
- Use analogies to aid understanding, but keep them apt and non-clichéd
- Key formulas/data must be included, but each must come with a plain-language explanation
- No filler phrases ("it's worth noting," "in conclusion," "to summarize")
- Paragraphs should be concise — 3–4 sentences max; white space aids readability
- Numbers must be sourced; estimates must be labeled [Est.]

## Core Content
{Organized materials, data, and arguments from research agents}

## Article Structure Requirements
1. **Opening (first 2–3 paragraphs)**: Must have a strong hook — open with a counterintuitive finding, a striking data point, or a framing question. Do NOT open with background context.
2. **Thesis**: State clearly what this article will argue and why it matters
3. **Core analysis (2–3 sections)**: Where the depth lives; every technical claim needs a plain-language companion sentence
4. **Evidence and data**: Let numbers do the talking — no vague generalizations ("good growth" → give the %)
5. **The bear case**: Acknowledge the strongest counterargument honestly — this is what separates rigorous analysis from advocacy
6. **Conclusion**: A clear, opinionated verdict — not a hedge. The reader should finish knowing what you actually think.

## Output
Write a complete draft of approximately {target word count} words.
```

---

## Phase Three: Editor Agent + Reader Agent Parallel Review

Once the first draft is complete, launch the Editor Agent and Reader Agent **simultaneously**.

### Editor Agent Prompt Template

```
You are a sharp financial editor (Editor Agent). Review and refine the following investment article.

## Review Criteria
1. **Opening**: Do the first 3 paragraphs demand attention? Is the hook strong enough?
2. **Structure**: Is the logic chain smooth? Any jumps or gaps the reader would notice?
3. **Data density**: Is every key claim backed by a number? Any unsupported assertions?
4. **Balance**: Is the bear case presented honestly, or is it a strawman?
5. **Pacing**: Any sections that overstay their welcome? Any that feel rushed?
6. **Closing**: Does the conclusion give a clear, opinionated verdict?
7. **Headline**: Does it accurately represent the article? Would it attract a serious investor?

## Full Article
{Complete first draft}

## Output Format
1. Overall assessment (3–5 sentences)
2. Headline revision suggestions (provide 2–3 alternatives)
3. Section-by-section revision suggestions (specific "original → suggested" comparisons for the 3 most critical issues)
```

### Reader Agent Prompt Template

```
You are a {target reader profile} (Reader Agent). Review the following investment article from a reader's perspective.

## Your Profile
{e.g., "You invest in B3 stocks and FIIs, have been investing for 3 years, understand DY and P/VP but haven't deeply studied FII credit risk or IPCA indexation"}

## Full Article
{Complete first draft}

## Please answer the following questions
1. After reading the first 3 paragraphs, would you keep reading? Why or why not?
2. Which sections required re-reading to understand? Quote the exact sentences.
3. Did the bear case feel honest, or like the author was going through the motions?
4. Are there questions you wanted answered that the article didn't cover?
5. After finishing, can you state the article's core conclusion in one sentence?
6. Would you share this article? What would you say when sharing it?
```

---

## Phase Four: Final Draft

### Step 1: Synthesize Feedback

| Issue Type | How to Handle |
|---------|---------|
| Flagged by both editor and reader | Must fix |
| Flagged only by editor | Fix unless it conflicts with author intent |
| Flagged only by reader | Evaluate case-by-case; reader experience is the ultimate test |
| Editor and reader conflict | Lean toward reader (editor pursues perfection, reader reflects reality) |

### Step 2: Execute Revisions and Produce Final File

Save the final draft as a `.md` file:

| Topic Type | Path | Naming Format |
|------|------|---------|
| Company analysis | `reports/{CompanyName}/` | `{CompanyName}-article-{YYYYMMDD}.md` |
| FII analysis | `reports/{FII-ticker}/` | `{FII-ticker}-article-{YYYYMMDD}.md` |
| Thematic / sector | `reports/` | `{topic-slug}-article-{YYYYMMDD}.md` |

---

## Writing Red Lines

1. **Do not fabricate data.** All cited data must have a source; estimates must be labeled `[Est.]`
2. **No filler language.** Banned phrases: "It's worth noting that," "In conclusion," "As we can see," "It must be said"
3. **No vague claims.** "Revenue grew strongly" → give the number. "Valuation is cheap" → state P/L, P/VP, DY, or FCF yield vs. peers
4. **The bear case cannot be a strawman.** Present the strongest version of the counterargument, not the weakest
5. **The conclusion must have a verdict.** If the article ends with "it depends," rewrite it — investors need a position, not a hedge
6. **All financial metrics must be defined on first use.** (e.g., "DY — dividend yield, the sum of the last 12 months of distributions divided by current unit price")
