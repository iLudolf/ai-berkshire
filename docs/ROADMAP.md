# ai-berkshire Roadmap

## P0: Near-term (1–2 months)

### A-Share Data Source Integration
- Integrate free data sources such as akshare and East Money
- Cover A-share financial data, market quotes, and top-trader rankings
- No changes needed to existing Skills — extend at the data layer only

## P1: Mid-term (3–6 months)

### HTML Report Output
- Add HTML report format on top of the existing Markdown output
- Support dark mode, navigation bar, and chart visualizations
- Improve report shareability and reading experience

### Multi-depth Research Modes
- `lite`: 5-minute quick judgment — rapidly returns valuation range and core conclusions
- `standard`: Current default mode — full multi-agent research
- `deep`: Additional cross-validation and historical analogies — institutional-grade depth

### Multi-stock Side-by-Side Comparison
- Support 2–4 stocks compared across the same dimensions
- Valuation benchmarking against peers in the same industry
- Output comparison matrix and stock-selection recommendation

## P2: Long-term (6 months+)

### Test Coverage
- Add unit tests for core tools (financial_rigor.py, etc.)
- Add regression tests for Skill outputs
- Ensure iterations do not break existing functionality

### Portfolio-level Analysis
- Portfolio health assessment
- Industry/geography concentration analysis
- Correlation risk detection
