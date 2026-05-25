# Screenshots + standalone prototypes

Ricky's local screenshots + the standalone HTML prototype for the asking-rent chart.

| File                             | What it is                                                                                                                                                                                                                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `01-logo-current.png`            | Current SWFL Data Gulf wordmark in use — "SWFL DATA GULF" all caps with the three-wave glyph and "LEE • COLLIER" eyebrow. Pair with the official `wordmark.svg` / `mark.svg` in `docs/fiverr-briefs/assets/`.                                                                                    |
| `02-charts-dashboard-mockup.png` | Multi-panel dashboard mockup — tiled chart layout showing how multiple cards (hbar, sankey, area, scatter, gauge) sit together. Reference for how the Scene 3 cards relate to a full-page layout.                                                                                                |
| `03-tourism-claude-output.png`   | Screenshot of a Claude Code session answering "what is the tourism like in SWFL?" — shows the brain output format (freshness token, key-metrics table, caveats, report-page link) that the platform is supposed to produce. This is the **kind of output** the landing page exists to advertise. |
| `04-hbar-chart-with-tooltip.png` | Live screenshot of the asking-rent horizontal bar chart with the hover tooltip showing "Pine Ridge Rd — $38.00/sqft, Neutral, vs Median +$5.50." Source of truth for the chart's interaction design.                                                                                             |
| `hbar-chart-standalone.html`     | **Self-contained HTML version** of the chart in `04`. Open in any browser, no build step. Vanilla JS + CSS — same animations and hover/tooltip behavior as the React component in `../../reference/hbar-chart/HBarChart.tsx`. Use this if Framer's React Code Component path isn't right.        |

## How these connect

The React production code lives in `../../reference/hbar-chart/` — that's what runs at `https://www.swfldatagulf.com/embed/cards/asking-rent`. The standalone HTML here is a prototype Ricky built alongside the React version on 2026-05-24; both produce the chart in screenshot `04`. Pick whichever path fits the build:

- **Framer + React Code Component** → use `../../reference/hbar-chart/HBarChart.tsx`
- **Framer Embed block / iframe** → host the standalone HTML or embed `/embed/cards/asking-rent`
- **Vanilla HTML pages** → adapt `hbar-chart-standalone.html` directly
