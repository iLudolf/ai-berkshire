# AI Berkshire - A Value Investment Research Framework for the AI Era

> "Price is what you pay, value is what you get." — Warren Buffett
>
> Redefining the depth and efficiency of investment research with AI.

**AI Berkshire** is a collection of investment research Skills compatible with both Claude Code and Codex. It systematizes and structures the methodologies of four value investing masters — Buffett, Munger, Duan Yongping, and Li Lu — enabling professional-grade investment research through AI Agents.

One person + Claude Code / Codex = An entire investment research team.

---

## Real Track Record

> Not theory. This framework is backed by a real-money validated investment system.

### 2024 Full-Year Return: +69.29%

<img src="assets/2024-returns.jpg" width="300" />

### 2025 Year-to-Date Return: +66.38%

<img src="assets/2025-returns.jpg" width="300" />

### Comparison Against Major Indices

| Metric | 2024 Full Year | 2025 YTD |
|--------|---------------|----------|
| **This Framework (Live)** | **+69.29%** | **+66.38%** |
| Hang Seng Index | +17.67% | +27.77% |
| S&P 500 | +23.31% | +16.39% |
| CSI 300 | +14.68% | +17.66% |
| NASDAQ | +28.64% | +20.36% |

**2024 Excess Return**: Outperformed S&P 500 by **46 percentage points**, outperformed Hang Seng by **52 percentage points**

**2025 Excess Return**: Outperformed S&P 500 by **50 percentage points**, outperformed Hang Seng by **39 percentage points**

**Two-year cumulative live return exceeds CNY 1.46 million**, significantly outperforming all major global indices for two consecutive years.

> *Disclaimer: Past returns do not represent future performance. Screenshots are from a real Futu Securities account.*

---

## Why Not Just Ask AI Directly?

You can certainly ask Claude directly: "Help me analyze whether Pinduoduo is worth buying." You'll get a balanced analysis of "on one hand... on the other hand...", ending with "investing carries risk, please use your own judgment."

**That kind of analysis looks right, but you can't make decisions with it.**

AI Berkshire doesn't solve the problem of "whether AI can analyze" — it solves the problem of **analysis quality and decision discipline**. Here are the core differences:

### 1. Forces Conclusions — No Hedging

Ask AI directly and you get analysis that tries to please both sides. AI Berkshire forces output: **Pass / Fail / Gray Area**, with specific price ranges and tiered recommendations.

> Typical AI answer: *"Pinduoduo has growth potential but also faces competitive pressures, investors need to weigh..."*
>
> AI Berkshire output:

> | Strategy | Recommendation | Price Range |
> |----------|---------------|-------------|
> | Aggressive | Build 20% position at current price | $95-105 |
> | Moderate | Wait for buyback policy clarity before entering | $85-95 |
> | Conservative | Doesn't meet 10-year certainty standard, watch | — |
>
> **Mirror Test**: Can't explain it in 5 sentences = Don't buy. No exceptions.

### 2. Four Masters Perspectives in Tension — Not a Single Analysis

It's not as simple as "analyze using Buffett's method." The four perspectives create **real contradictions and tensions** —

Using Pinduoduo as an example:
- **Duan Yongping** (business model): Good business, C2M model hard to replicate → Score 3.7/5
- **Buffett** (financial valuation): Ex-cash PE only 6.3x, money-printing machine → Score 4.4/5
- **Munger** (contrarian thinking): Economic moat shallower than imagined, Douyin reached CNY 4 trillion GMV in 3 years → Score 3.5/5
- **Li Lu** (long-term certainty): Management culture has hidden risks, uncertain after 10 years → Score 2.0/5

**Buffett says "genuinely cheap," Li Lu says "if uncertain, don't buy"** — this conflict is the true state of investment decision-making. A single prompt cannot generate this kind of multi-perspective tension, yet this is precisely the key to avoiding blind spots.

### 3. Structured Anti-Bias Mechanisms

The most dangerous thing AI does isn't giving wrong answers — it's giving answers that **look right but don't hold up under scrutiny**. AI Berkshire has multiple built-in "anti-deception" mechanisms in its workflow:

| Mechanism | What Problem It Solves | Example |
|-----------|----------------------|---------|
| **Information Richness Rating (A/B/C)** | Prevents the illusion that "more data = higher certainty" | Pop Mart rated B: limited data, derived metrics labeled with confidence levels |
| **Munger-Style Inversion Test** | Forces thinking about failure scenarios | "Under what circumstances would Pinduoduo die?" → 5 major scenarios with probabilities |
| **Quick Rejection Checklist** | 8 red-line one-veto criteria | Management integrity issues → immediate rejection, regardless of how cheap the valuation |
| **Anti-Consensus Check** | Avoids thinking like the market | "Why are smart people shorting?" → uncovers overlooked risks |
| **Blank Space Principle** | Prefers to say "don't know" | Labels "gray areas" when data is insufficient, doesn't dress uncertainty as certainty |

### 4. Precision in Financial Data

LLM mental math is unreliable. Getting a PE decimal wrong or confusing HKD and CNY market cap units can lead to wrong investment decisions.

**Real case**: When analyzing Tencent, market cap data from different sources used both "HKD hundred millions" and "CNY hundred millions." AI Berkshire's approach:

```bash
# Manual market cap verification: price × total shares, compare against reported data
python3 tools/financial_rigor.py verify-market-cap \
  --price 510 --shares 9.11e9 --reported 4.65e12 --currency HKD
# ✅ Verification passed, deviation only 0.08%
```

All calculations use Python `decimal.Decimal` (precise decimal), not `float`. Key data requires cross-validation from at least 2 independent sources.

### 5. Reproducible Research Process

Ask AI directly and each output differs in format, depth, and coverage — today's Tencent analysis has an economic moat score, tomorrow's Meituan analysis may omit it entirely.

AI Berkshire ensures: **Same input → Consistently structured, consistently deep output**. This means you can:
- Compare 7 companies side by side with completely consistent scoring standards
- Re-analyze the same company 6 months later and directly compare changes
- Align research results across team members

> Real output — 7 companies screened with the same standard Checklist:
>
> | Company | Pass? | Circle of Competence | Good Business | Economic Moat | Management | Margin of Safety | Overall |
> |---------|:-----:|:--------------------:|:-------------:|:-------------:|:----------:|:----------------:|:-------:|
> | Moutai | ✅ Pass | ★★★★★ | ★★★★★ | ★★★★★ | ★★★☆☆ | ★★★★☆ | 4.7 |
> | Tencent | ✅ Pass | ★★★★☆ | ★★★★★ | ★★★★★ | ★★★★★ | ★★★★☆ | 4.7 |
> | NVIDIA | ✅ Conditional | ★★★★☆ | ★★★★★ | ★★★★★ | ★★★★★ | ★★★☆☆ | 4.3 |
> | Meituan | ✅ Conditional | ★★★★☆ | ★★★★☆ | ★★★★☆ | ★★★★☆ | ★★★★☆ | 4.0 |
> | Kuaishou | ✅ Conditional | ★★★☆☆ | ★★★★☆ | ★★★★☆ | ★★★★☆ | ★★★★★ | 4.0 |
> | Pinduoduo | ❓ Gray | ★★★★☆ | ★★★★☆ | ★★★☆☆ | ★★★☆☆ | ★★★★★ | 3.8 |
> | Pop Mart | ❓ Gray | ★★★☆☆ | ★★★★☆ | ★★★★☆ | ★★★★★ | ★★★☆☆ | 3.7 |

### 6. Multi-Agent Parallelism = Multiplied Research Depth

`/investment-team` launches 4 independent Agents to research a company **simultaneously**. Each Agent searches the web independently, cross-validates data, and reaches independent conclusions. This is not splitting one prompt into four sections — it's 4 "analysts" each doing complete research, with the Team Lead then synthesizing.

One person asking AI directly has one context window. 4 Agents in parallel equals 4x the search volume, 4x the information sources, 4 independent perspectives.

```
┌─────────────────────────────────────────────┐
│              Team Lead (You)                  │
│         Coordination · Synthesis              │
├──────┬──────┬──────────┬───────────┤
│ Agent 1    │ Agent 2    │ Agent 3        │ Agent 4         │
│ Business   │ Financial  │ Industry       │ Risk &          │
│ Model      │ Valuation  │ Competition    │ Management      │
│ Duan YP    │ Buffett    │ Munger         │ Li Lu           │
└──────┴──────┴──────────┴───────────┘
        ↓ Parallel research, real-time progress reporting ↓
              Final Consolidated Report
```

### Summary in One Sentence

> **Asking AI directly gets you "analysis that looks right." Using AI Berkshire gets you "investment research reports you can actually make decisions with."**

---

## Overall Architecture

<p align="center">
  <img src="assets/architecture.png" alt="AI Berkshire Overall Architecture" width="600" />
</p>

> Source: [`assets/architecture.mmd`](assets/architecture.mmd) (Mermaid editable source)

**Three-Layer Design Philosophy**:
- **Skill Layer**: Abstracts "what you want to do" into 16 clear entry points — deep research, earnings analysis, industry screening, portfolio management, thinking tools, chosen by scenario
- **Agent Layer**: Each skill internally runs 4 Agents in parallel — they each search independently, judge independently, challenge each other, and the Team Lead synthesizes at the end
- **Tools Layer**: Precise calculations, real-time retrieval, report spot-checking — ensuring data rigor across every report is verifiable

---

## Skills Overview (18 Total)

### 🔬 Deep Research

| Skill | Purpose | Best For |
|-------|---------|---------|
| [`/investment-research`](skills/investment-research.md) | Four Masters comprehensive deep analysis | All-around investment research on a listed company |
| [`/investment-team`](skills/investment-team.md) | Multi-Agent parallel investment research team | 4 Agents in parallel — fastest and most comprehensive |
| [`/management-deep-dive`](skills/management-deep-dive.md) | In-depth management research | "Buying stock is buying people" — deep dive when management is the key variable |
| [`/private-company-research`](skills/private-company-research.md) | Private company deep research | Researching information-scarce private companies like Ant Group, SpaceX |
| [`/deep-company-series`](skills/deep-company-series.md) | 8-article long-form series on one company | WeChat public account-level deep series, 120,000 words from cognitive reset to decision closure |

### 📊 Earnings Analysis

| Skill | Purpose | Best For |
|-------|---------|---------|
| [`/earnings-review`](skills/earnings-review.md) | Earnings deep read (primary sources) | Reading original financial reports only, not secondary research reports — read annual reports like Buffett |
| [`/earnings-team`](skills/earnings-team.md) | Earnings team + WeChat article publication | Four Masters parallel earnings interpretation → editorial polish → reader review → publishable article |

### 🏭 Industry Screening

| Skill | Purpose | Best For |
|-------|---------|---------|
| [`/industry-research`](skills/industry-research.md) | Industry chain panoramic scan | Research all investment opportunities in an industry (sliced by supply chain segment) |
| [`/industry-funnel`](skills/industry-funnel.md) | Industry funnel screening | Full market → coarse filter ≤10 companies → final selection of 3 for deep analysis |
| [`/quality-screen`](skills/quality-screen.md) | Quality screening (7 hard criteria) | Quickly eliminate non-tier-one companies; supports individual stocks/industries/indices/themes in batch |
| [`/bottleneck-hunter`](skills/bottleneck-hunter.md) | Supply chain bottleneck hunter | Starting from mega-trends, find physical bottlenecks and arbitrage opportunities in the supply chain |
| [`/investment-checklist`](skills/investment-checklist.md) | Buffett pre-purchase Checklist | Six-gate rapid screening, decide in 10 minutes whether a company is worth deeper research |

### 📈 Portfolio Management

| Skill | Purpose | Best For |
|-------|---------|---------|
| [`/portfolio-review`](skills/portfolio-review.md) | Portfolio management and optimization | Upgrade from "researching companies" to "managing a portfolio" — position sizing, concentration, rebalancing |
| [`/thesis-tracker`](skills/thesis-tracker.md) | Investment thesis tracking | Discipline system after buying: continuously track whether the thesis has been falsified |
| [`/news-pulse`](skills/news-pulse.md) | Rapid attribution of stock price moves | Understand "what happened" in 10 minutes when a stock makes a big move |

### 🧠 Thinking Tools

| Skill | Purpose | Best For |
|-------|---------|---------|
| [`/dyp-ask`](skills/dyp-ask.md) | Duan Yongping Q&A | Think through any question the way Duan Yongping would — business, investing, life |
| [`/financial-data`](skills/financial-data.md) | Financial data sourcing and cross-validation standards | Ensure key data comes from 2 independent sources, alert when error >1% |
| [`/wechat-article`](skills/wechat-article.md) | WeChat public account articles | Author, editor, and reader Agents collaborate to produce publishable articles |

---

## Quick Start

### 1. Install the AI Client

This repository maintains a single canonical workflow, with both Claude Code commands and Codex skills provided separately. Install based on whichever client you use.

Claude Code users:

```bash
npm install -g @anthropic-ai/claude-code
```

Codex users:

```bash
# macOS / Linux
curl -fsSL https://chatgpt.com/codex/install.sh | sh

# Or using npm
npm install -g @openai/codex

# Or using Homebrew
brew install --cask codex

# Verify installation
codex --version
```

Windows users can use the official PowerShell install command: `powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"`.

If `codex --version` outputs a version number correctly, you can proceed to install this project's Codex skills.

### 2. Install Skills

Claude Code installation:

```bash
# Clone the repository
git clone https://github.com/xbtlin/ai-berkshire.git

# Copy skills to Claude Code global commands directory
cd ai-berkshire
./scripts/install-claude-commands.sh
```

Codex installation:

```bash
# Clone the repository
git clone https://github.com/xbtlin/ai-berkshire.git

# Generate and install Codex skills to ~/.codex/skills
cd ai-berkshire
./scripts/install-codex-skills.sh

# Optional: install Codex slash prompts to ~/.codex/prompts
# For a Claude Code-like /investment-research experience
./scripts/install-codex-prompts.sh
```

The repository maintains three entry points simultaneously: `skills/*.md` are the Claude Code command source files; `codex-skills/*/SKILL.md` are Codex skill packages generated from `skills/*.md` by `scripts/sync-codex-skills.py`; `codex-prompts/*.md` are optional Codex slash prompt compatibility layers.

### 3. Usage

Call directly in Claude Code:

```bash
# Deep research
/investment-research Tencent
/investment-team Meituan
/management-deep-dive Wang Xing Meituan
/private-company-research SpaceX
/deep-company-series Pinduoduo

# Earnings analysis
/earnings-review Tencent 2025Q4
/earnings-team PDD 2025 Annual Report

# Industry screening
/industry-research nuclear power
/industry-funnel AI compute
/quality-screen Hang Seng Index constituents
/bottleneck-hunter AI infrastructure
/investment-checklist Moutai, NVIDIA, Apple

# Portfolio management
/portfolio-review Tencent 30%, Meituan 20%, Moutai 20%, Cash 30%
/thesis-tracker Pinduoduo
/news-pulse Tencent

# Thinking tools
/dyp-ask Where exactly is Pinduoduo's economic moat?
/wechat-article Large model OPD technology explained
```

After installing in Codex, restart Codex and describe the task by skill name, for example:

```text
Use investment-research to research Tencent
Use earnings-review to analyze PDD 2025 Annual Report
Use industry-funnel to screen AI compute
Use bottleneck-hunter to scan AI infrastructure bottlenecks
Use wechat-article to write a large model OPD technology explainer
```

If you installed Codex slash prompts, after restarting Codex you can also search for these prompts in the `/` menu. Codex's official custom prompt entry point is typically shown as `prompts:<name>`, for example:

```text
/prompts:investment-research Tencent
```

---

## Detailed Skill Descriptions

### 1. `/investment-research` — Four Masters Comprehensive Analysis

The most comprehensive single-company deep research framework. Executed sequentially across seven modules:

```
Data Collection → Business Essence (Duan Yongping) → Economic Moat (Buffett) → Contrarian Thinking (Munger)
    → Management Assessment (Duan YP + Buffett) → Civilizational Trends (Li Lu) → Valuation & Margin of Safety
```

**Core Features**:
- AI research bias awareness mechanism (A/B/C information richness rating)
- Key data multi-source cross-validation (manual market cap verification, at least 2 independent sources)
- "Follow-up questions" from the four masters woven throughout
- Three-scenario valuation (optimistic/neutral/pessimistic) + reverse DCF

**Sample Output Excerpt**:

> #### Comprehensive Decision Memo
>
> | Dimension | Conclusion | Confidence |
> |-----------|-----------|------------|
> | Business Quality (Duan Yongping) | Excellent: platform business, bilateral network effects, marginal cost approaching zero | ★★★★★ |
> | Economic Moat (Buffett) | Wide and widening: network effects + switching costs + scale economics, triple overlay | ★★★★☆ |
> | Management (Duan YP + Buffett) | Excellent: founder-led, strong capital allocation discipline | ★★★★☆ |
> | Biggest Risk (Munger) | Regulatory policy uncertainty, new business losses dragging overall profit | ★★★☆☆ |
> | Civilizational Trend (Li Lu) | Aligned with digital consumption trend, but not a "civilization-level paradigm shift" | ★★★★☆ |
> | Valuation (Buffett + Duan YP) | Current PE 18x, at historical median-low, some margin of safety present | ★★★★☆ |
>
> **Duan Yongping**: "The essence of this business is connecting consumers and merchants, earning money from efficiency improvements. The hallmark of a good business is: more users = more merchants; more merchants = more users. Once the flywheel starts spinning, it's very hard to stop."
>
> **Munger**: "Think backwards — if this company disappeared tomorrow, what would users and merchants do? If the answer is 'find alternatives quickly,' then the economic moat isn't deep enough. If the answer is 'life would become very inconvenient,' then it's worth attention."

---

### 2. `/investment-team` — Multi-Agent Investment Research Team

Launches 4 AI Agents to research in parallel, simulating real investment research team collaboration. Each Agent searches independently, analyzes independently, and gives scores independently; the Team Lead then synthesizes the assessment.

**Sample Output Excerpt**:

> #### One-Sentence Conclusion
> Meituan is the absolute leader in China's local life services, with multiple network effect economic moats. Current valuation is at a historically low level, long-term investment value is significant, recommend building a position on dips.
>
> #### Four-Dimension Score Summary
>
> | Dimension | Framework | Score | Core Judgment |
> |-----------|-----------|-------|--------------|
> | Business Model & Economic Moat | Duan Yongping | ★★★★☆ | Strong bilateral network effects, food delivery + in-store form a flywheel |
> | Financials & Valuation | Buffett | ★★★★☆ | Core business profit margins continuously improving, valuation at historical lows |
> | Industry & Competition | Munger | ★★★☆☆ | Douyin encroaching on in-store business, competitive landscape at risk of deterioration |
> | Risk & Management | Li Lu | ★★★★☆ | Wang Xing's strategic vision outstanding, but new business cash burn needs monitoring |
>
> **Overall Score: 3.8 / 5**
>
> #### Investment Recommendation
>
> | Strategy | Recommendation | Price Range (HKD) |
> |----------|---------------|-----------------|
> | Aggressive | Build 30% position at current price | 120-140 |
> | Moderate | Wait for pullback to 100-110 to enter | 100-120 |
> | Conservative | Wait for quarterly report to confirm profit margin trend before entering | <100 |

---

### 3. `/investment-checklist` — Buffett Pre-Purchase Checklist

Six-gate rapid screening to help you decide in 10 minutes whether a company is worth deeper research:

```
Gate 1: Circle of Competence (Can I understand it?)
    ↓ Pass
Gate 2: Good Business (What are the economic characteristics?)
    ↓ Pass
Gate 3: Economic Moat (How deep is the competitive advantage?)
    ↓ Pass
Gate 4: Management (Is it trustworthy?)
    ↓ Pass
Gate 5: Margin of Safety (Is the price cheap?)
    ↓ Pass
Gate 6: Decision Discipline (Is this rational or FOMO?)
    ↓ Pass
   ✅ Mirror Test
```

**Supports multi-company comparison** — screen multiple candidates at once:

```
/investment-checklist Tencent, Alibaba, Meituan, Pinduoduo
```

**Sample Output Excerpt**:

> #### Mirror Test
>
> "I am buying **Tencent** at HKD 380 because:
> 1. The essence of this business is a **social network + digital content platform**, and I understand it;
> 2. Its economic moat is **1.2 billion users' social relationship graph**, and it's widening;
> 3. Management — **Pony Ma is low-key and pragmatic, excellent capital allocator** — is trustworthy;
> 4. The current price represents approximately an **80% discount to intrinsic value**, providing some margin of safety;
> 5. Even if I'm wrong, downside risk is manageable because **net cash on hand exceeds CNY 200 billion, gaming cash flows are strong**."
>
> ✅ Passes Mirror Test
>
> **Can't explain it in 5 sentences = Don't buy. No exceptions.**

---

### 4. `/industry-research` — Industry Chain Panoramic Scan

Starting from an investment theme, complete a panoramic industry chain research:

```
Investment Logic Chain Construction → Industry Chain Panorama → Global Listed Company Scan
    → Four Masters Analysis of Leading Companies per Segment → Portfolio Allocation Recommendations
```

**Sample Output Excerpt**:

> #### Investment Logic Chain: Nuclear Power
>
> Underlying trend: AI data center electricity demand explosion + carbon neutrality goals
> → Leads to: Surge in demand for stable, clean baseload power
> → Creates: Certain demand for nuclear power restart/new construction/SMR
> → Beneficiaries: Uranium mining → Fuel processing → Equipment manufacturing → Operators
>
> #### Recommended Portfolio
>
> | Tier | Position | Target | Segment | Core Logic |
> |------|----------|--------|---------|-----------|
> | Core | 50% | CGN, Cameco | Operations + Uranium | Highest certainty |
> | Satellite | 30% | China National Nuclear, Dongfang Electric | Operations + Equipment | Domestic substitution beneficiaries |
> | Option | 15% | NuScale, Nano Nuclear | SMR | High risk, high elasticity |
> | ETF | Alternative | URA, URNM | Full chain | Lazy investor solution |

---

### 5. `/industry-funnel` — Industry Funnel Screening

Starting from an industry/direction, **full market → ≤10 companies → 3 companies** with progressive selection:

```
Full market scan (activity + price change + top 30 by market cap union, 30-60 companies)
    ↓ 5 hard value investing criteria
Coarse filter ≤ 10 companies
    ↓ Detailed analysis (300-500 words per company)
Detailed analysis ≤ 10 companies
    ↓ Final selection (by portfolio complementarity, not top-3 by score)
Four Masters deep analysis of 3 companies (800-1200 words each)
    ↓
Recommended portfolio (core / satellite / option) + action signals
```

**Core Features**:
- Each layer has clear keep/discard criteria; eliminated candidates have their rejection rationale recorded (not a black box)
- Final 3 companies selected by "portfolio complementarity" (high certainty + medium elasticity + high elasticity), not top-3 ranking
- Mandatorily lists "future IPO candidates" to avoid missing key private market players
- AI bias awareness: addresses large-cap bias / English-language bias / narrative bias / listed-company bias

**Difference from `/industry-research`**:
- `industry-research` focuses on supply chain structure and panorama (sliced by segment)
- `industry-funnel` focuses on individual stock screening funnel (progressive selection from full market down to 3 companies)

**Real test: 4 AI sub-sectors in parallel (2026-05-09)**:

| Sub-Sector | Final 3 | Core Position Recommendation |
|-----------|---------|--------------------------|
| AI Compute | TSMC / NVIDIA / SK Hynix | TSMC ★★★★★ |
| AI Models | Alphabet / Meta / Alibaba | Alphabet ★★★★★ |
| AI Applications | Microsoft / Adobe / AppLovin | Microsoft + Adobe ★★★★ |
| AI Infrastructure Power | Eaton / TBEA / Talen Energy | Eaton + TBEA ★★★★ |

**Key finding**: The biggest winner at the AI application layer isn't AI Native companies, but established giants with channel + data + workflow embeddedness — echoing the historical pattern of "selling shovels" during the 1995-2000 internet bubble (Amazon and Apple won, Pets.com lost).

*(Reports archived — project focus pivoted to Brazilian equities and FIIs)*

---

### 6. `/private-company-research` — Private Company Deep Research

A "detective-style" research framework designed for information-scarce private companies:

**Core Differentiators**:
- **Financial data assembly**: Piecing together from prospectuses, parent company reports, funding news, and industry data from multiple sources
- **Confidence labeling**: Each data point labeled 🟢 High / 🟡 Medium / 🔴 Low confidence
- **Multi-method valuation cross-check**: Funding valuation method + comparable company method + DCF + terminal value back-calculation
- **Exit path analysis**: Full path assessment of IPO / M&A / secondary transfer

**Sample Output Excerpt**:

> #### Company Profile Snapshot: SpaceX
>
> | Item | Content |
> |------|---------|
> | Latest Valuation | ~$350B (2025 secondary market) 🟡 |
> | Estimated Revenue | ~$13B (2024) 🟡 |
> | Starlink Users | 4M+ (end of 2024) 🟢 |
> | Launch Frequency | 100+ times/year (2024) 🟢 |
>
> #### Valuation Assessment
>
> | Method | Valuation Range | Notes |
> |--------|----------------|-------|
> | Latest Funding | $350B | Secondary market quote, includes liquidity premium |
> | Comparable Company | $200-280B | Benchmarked against telecom + aerospace + defense |
> | DCF (Neutral) | $250-350B | Assumes Starlink $30B revenue in 2027 |
> | Terminal Value Back-calc | $400-600B | Assumes Starlink becomes global telecom infrastructure |
>
> **Combined Fair Valuation Range: $250B - $400B**

---

### 7. `/news-pulse` — Rapid Stock Price Move Attribution

An intelligence-response Skill designed for "quickly understanding what happened when a stock makes a big move." **Not deep investment research — it's rapid attribution in 10-15 minutes** — avoiding anxiety spirals or blind stop-losses when portfolio positions move sharply.

**Core Differentiators**:
- **4-dimensional parallel reconnaissance**: Company events / Regulatory policy / Industry peers / Market sentiment (sell-side + opinion leaders + southbound flows)
- **Attribution over listing**: Not just listing all news, but judging "which event accounts for this stock price move"
- **Mandatory nature judgment**: Value event / Sentiment volatility / **True cause unknown** / Mixed — "True cause unknown" is the most valuable output (potential insider front-running)
- **Clear action recommendations**: Whether to trigger deep research, whether to re-examine the thesis, whether to just observe

**Difference from Other Skills**:
| Scenario | Use What |
|----------|---------|
| Complete investment research (hours) | `/investment-team` or `/investment-research` |
| Earnings deep read | `/earnings-review` |
| Long-term thesis tracking | `/thesis-tracker` |
| **Stock price move 10-minute attribution** | **`/news-pulse`** |

**Sample Output Excerpt** (Tencent 4/17-5/01 real test, 14 days -10.47%):

> #### One-Sentence Attribution
> This -10.47% decline was approximately 70-80% driven by capital flows + sentiment (buyback blackout period + southbound selling + sector beta + AI narrative hijacked), with 20-30% from deferred digestion of doubled AI investment — **no fundamental negative catalysts**, sell-side maintains buy consensus; nature is "liquidity + sentiment-driven pullback," not a value event.
>
> #### Move Attribution Table
>
> | Candidate Explanation | Estimated Contribution | Confidence |
> |----------------------|----------------------|------------|
> | Buyback blackout period (structural, before 5/13 earnings) | -3% ~ -4% | High |
> | Southbound capital shifted to net selling Tencent | -2% ~ -3% | High |
> | AI narrative hijacked by competitors (DeepSeek V4/Qwen3.6/Moonshot 1T) | -1% ~ -2% | Medium |
> | Sector/macro beta (oil prices + geopolitics + Fed Warsh hawkish) | -2% ~ -3% | High |
> | Pre-Q1 report risk-off | -1% ~ -2% | Medium |
> | Fundamental deterioration | **0%** | Very High (eliminated) |
>
> #### Nature Judgment: ✅ Mixed
> 70% capital flow/sentiment + 20% AI long-term narrative concern + 10% pre-Q1 report uncertainty
>
> **Key counter-evidence**: Duan Yongping sold Tencent puts on 4/8 (bullish); 24 sell-side consensus Strong Buy; NetEase rose 2% on 4/30 against the market (eliminates gaming industry issue); Tencent underperformed Hang Seng Tech by 7 percentage points (Hang Seng Tech actually rose 4% for the month).

Usage:

```
/news-pulse Tencent
/news-pulse Pinduoduo drop 12% within one week
/news-pulse miHoYo
```

---

## Real-World Research Reports

> Below are real investment research reports generated using this framework, demonstrating the actual output quality of AI-powered investment research.

| Company | Skill Used | Core Conclusion | Report Link |
|---------|-----------|----------------|------------|
| — | — | Reports coming soon — project now focused on Brazilian equities and FIIs | — |

> *PRs welcome to submit research reports you generate using this framework.*

---

## Design Philosophy

### Four Masters Methodology Integration

```
              ┌──────────────────┐
              │   Duan Yongping   │
              │  "Right Business" │
              │  Business Essence │
              └────────┬─────────┘
                       │
    ┌──────────────────┼──────────────────┐
    │                  │                  │
    ▼                  ▼                  ▼
┌────────┐     ┌──────────┐      ┌────────┐
│ Buffett │     │  Munger   │      │ Li Lu  │
│ Economic│     │ Inversion │      │ Civ.   │
│  Moat  │     │ Thinking  │      │ Trends │
│ Margin │     │ Risk List │      │Paradigm│
│of Safety│    │ Bias Check│      │ Shifts │
└────────┘     └──────────┘      └────────┘
```

The four masters are not simply divided into roles — they are designed to **challenge each other**:
- Duan Yongping says "good business," Munger asks "how could it die"
- Buffett says "cheap enough," Li Lu asks "will it still be here in 10 years"
- What you get is not four stitched-together reports, but the collision of four ways of thinking

### Financial Rigor Tools (`tools/financial_rigor.py`)

| Function | Command | Problem It Solves |
|----------|---------|-----------------|
| **Market Cap Verification** | `verify-market-cap` | Precise price × total shares calculation, detects unit errors |
| **Valuation Verification** | `verify-valuation` | Precise decimal calculation for PE/PB/ROE/FCF Yield |
| **Multi-Source Cross-Validation** | `cross-validate` | Auto-compares same data from N sources, alerts when tolerance exceeded |
| **Three-Scenario Valuation** | `three-scenario` | Precise calculation of target prices for optimistic/neutral/pessimistic scenarios |
| **Benford's Law Detection** | `benford` | Detects anomalies in first-digit distribution of financial data |
| **Precise Calculator** | `calc` | Precise calculation of any financial expression, replacing LLM mental math |

**Design Principle**: All calculations use Python `decimal.Decimal` (precise decimal), not `float` (floating point approximation). `0.1 + 0.2 = 0.3` is not allowed to fail in financial contexts.

---

## Project Roadmap

- [x] Four Masters comprehensive analysis framework (`/investment-research`)
- [x] Multi-Agent parallel investment research team (`/investment-team`)
- [x] Buffett pre-purchase Checklist (`/investment-checklist`)
- [x] Industry chain panoramic scan (`/industry-research` + `/industry-funnel`)
- [x] Private company research framework (`/private-company-research`)
- [x] Financial rigor tools (precise arithmetic, market cap verification, multi-source cross-validation, Benford's Law detection)
- [x] Rapid stock price move attribution (`/news-pulse` 4-dimensional parallel reconnaissance)
- [x] Earnings deep read (`/earnings-review` + `/earnings-team` Four Masters parallel interpretation)
- [x] Portfolio management (`/portfolio-review` position review and rebalancing)
- [x] Investment thesis tracking (`/thesis-tracker` post-purchase discipline system)
- [x] Management in-depth research (`/management-deep-dive`)
- [x] Quality rapid screening (`/quality-screen` 7 hard criteria elimination)
- [x] Duan Yongping thinking simulation (`/dyp-ask`)
- [x] Deep-dive long-form series (`/deep-company-series` 8 articles, 120,000 words)
- [ ] Historical backtesting: AI research reports vs. actual stock price performance
- [ ] Macroeconomic cycle analysis framework
- [ ] Real-time data integration via MCP (Wind/Bloomberg/Yahoo Finance)

---

## Disclaimer

This project is for learning and research purposes only and does not constitute any investment advice. Investing carries risk; decisions require careful consideration. Always do your own due diligence (DYOR).

---

## License

MIT License

---

> "The best investment you can make is in yourself." — Warren Buffett
>
> AI Berkshire: Giving everyone their own investment research team.

## Star History

If this project has been helpful to you, please give it a Star!

[![Star History Chart](https://api.star-history.com/svg?repos=xbtlin/ai-berkshire&type=Date)](https://star-history.com/#xbtlin/ai-berkshire&Date)
