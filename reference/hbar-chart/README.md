# HBar chart — reference code from brain-platform

The horizontal-bar "Asking rent (NNN, $/sqft)" card we built on 2026-05-24 (commit `48e07ab` in brain-platform). Live at https://www.swfldatagulf.com/embed/cards/asking-rent.

Two files in this folder — drop into your Next.js project, or use as a pattern for porting the design to Framer / vanilla HTML.

| File                   | What it is                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `HBarChart.tsx`        | Standalone React component. Pure CSS (styled-jsx) + GSAP animation. No chart libs. Source on main: `components/charts/HBarChart.tsx` |
| `asking-rent-page.tsx` | The embed-route page that wires the component to corridor fixture data. Source on main: `app/embed/cards/asking-rent/page.tsx`       |

A vanilla-HTML/JS variant of the same chart sits in `../../assets/screenshots/hbar-chart-standalone.html` — open it in a browser, no build needed. Useful if Framer's React Code Component path isn't desired.

## Design contract

- **Card width:** `max-width: 620px; min-width: 320px;`
- **Row grid:** `148px label  |  1fr bar track  |  76px value` (right-aligned mono value)
- **Tier colors:**
  - `bullish` → full teal `#3ecfb2` + glow (10px box-shadow @ 45% alpha)
  - `neutral` → teal @ 55% alpha, no glow
  - `bearish` → amber `#e8a84c` + glow
- **Fonts:** IBM Plex Sans for labels/title, IBM Plex Mono for the eyebrow, value, footer, and tooltip rows
- **Animation:** GSAP `power2.out` stagger — `0.11s` between rows, `0.75s` per fill. The numeric value tweens in parallel via a `proxy` object so the $ counter counts up from $0.00.
- **Hover behavior:** non-hovered rows drop to 35% opacity; hovered row stays at 100% and the bar fill brightens (`filter: brightness(1.25)`). Tooltip follows cursor with `+14px / -48px` offset.
- **Optional separator:** `separatorAfter={N}` with `separatorLabel` injects a dashed-line divider after row N — used in the asking-rent card to split "top 5" from "bottom 2."

## Component API

```tsx
type HBarTier = "bullish" | "neutral" | "bearish";

type HBarCorridor = {
  name: string;
  value: number;
  tier: HBarTier;
};

type HBarChartProps = {
  title: string; // "Asking rent (NNN, $/sqft)"
  corridors: HBarCorridor[];
  median: number; // shown in footer
  range: { min: number; max: number }; // bar widths normalized to range.max
  eyebrow?: string; // defaults to "{count} corridors"
  separatorAfter?: number; // dashed divider after this row index
  separatorLabel?: string; // label rendered inside the divider
  detailHref?: string; // optional "View all → " link in footer
  detailLabel?: string;
};
```

## Tier assignment (from `asking-rent-page.tsx`)

```ts
const BULLISH_MULTIPLIER = 1.2;
const BEARISH_MULTIPLIER = 0.7;

function tierFor(value: number, median: number): HBarTier {
  if (value >= median * BULLISH_MULTIPLIER) return "bullish";
  if (value <= median * BEARISH_MULTIPLIER) return "bearish";
  return "neutral";
}
```

So a $45/sqft corridor in a $32.50 median market is bullish (>$39); $16.50 is bearish (<$22.75); everything between is neutral.

## Dependencies

If you drop `HBarChart.tsx` into a Next.js 15 / React 19 project, you need:

```bash
npm install gsap
```

For the fonts to load via `next/font/google` (as `asking-rent-page.tsx` does):

```tsx
import { IBM_Plex_Sans, IBM_Plex_Mono } from "next/font/google";

const plexSans = IBM_Plex_Sans({
  subsets: ["latin"],
  weight: ["400", "600", "700"],
  variable: "--font-plex-sans",
  display: "swap",
});

const plexMono = IBM_Plex_Mono({
  subsets: ["latin"],
  weight: ["400", "600"],
  variable: "--font-plex-mono",
  display: "swap",
});
```

The component uses `--font-plex-sans` and `--font-plex-mono` CSS variables internally, falling back to literal `"IBM Plex Sans"` / `"IBM Plex Mono"` strings if the variables aren't bound.

## Data

`asking-rent-page.tsx` reads from `fixtures/corridor-rents.json` at the project root — a `CorridorEntry[]` shape:

```ts
type CorridorEntry = {
  id: string;
  name: string;
  submarket: string;
  lat: number;
  lng: number;
  nnn_asking_rent_per_sqft: number | null;
  vacancy_pct: number | null;
  absorption_sqft: number | null;
  saturation_index: number;
  permit_zscore: number;
};
```

Live data (26 corridors): see `data/cre-corridors.{csv,json}` on the `data/scene3-tables` branch.

## medianOf helper

The page imports `@/lib/stats` for `medianOf`. If you don't want the dep, here's the whole function:

```ts
export function medianOf(xs: number[]): number | null {
  if (xs.length === 0) return null;
  const sorted = [...xs].sort((a, b) => a - b);
  const mid = Math.floor(sorted.length / 2);
  return sorted.length % 2 === 1
    ? sorted[mid]
    : (sorted[mid - 1] + sorted[mid]) / 2;
}
```

## Note on palette

This chart's palette is different from the original handoff brief's "Gulf palette" in `docs/fiverr-briefs/handoff-landing-embeds.md`:

| Token       | Original Gulf palette   | This card's palette |
| ----------- | ----------------------- | ------------------- |
| Card bg     | `gulf-slate #152832`    | `#162030`           |
| Page bg     | `gulf-midnight #0A1419` | `#0f1923`           |
| Accent teal | `gulf-teal #3DC9C0`     | `#3ecfb2`           |
| Amber       | — (not in original)     | `#e8a84c`           |

The original brief had no amber; this card introduced it as the "bearish" tier color. Tell Ricky if you want both palettes consolidated — straightforward find/replace if so.
