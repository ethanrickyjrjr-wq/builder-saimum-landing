# Builder Setup

## Install & run

```bash
npm install
npm run dev
```

Then open http://localhost:3000/embed/charts — you'll see the ZHVI area chart and the CRE corridor rent bar chart live with real fixture data.

## What's in this repo

```
components/viz/
  CorridorMarketScatter.tsx  ← 2D animated ECharts scatter (vacancy vs. rent)
  CorridorRentChart.tsx      ← horizontal bar chart, ECharts + GSAP scroll
  ZHVIAreaChart.tsx          ← Recharts area chart, Framer Motion
  RadialConfidenceGauge.tsx  ← radial gauge, ECharts + GSAP

app/embed/charts/page.tsx    ← wired page: ZHVIAreaChart + CorridorRentChart
app/embed/waitlist/page.tsx
app/embed/footer-token/page.tsx

types/viz.ts                 ← shared TypeScript interfaces for all components
fixtures/corridors.json      ← 26 SWFL CRE corridors (rent, vacancy, absorption)
fixtures/zhvi-trend.json     ← Zillow home value trend (Cape Coral, Fort Myers, Naples)
```

## Wiring up CorridorMarketScatter

The scatter chart is built and typed but not wired into a page yet — that's your next task.

It takes the same `CorridorEntry[]` data as `CorridorRentChart`. You can add it to `app/embed/charts/page.tsx`:

```tsx
import { CorridorMarketScatter } from "@/components/viz";

// Inside the grid, add a third section:
<section
  style={{
    background: "#152832",
    border: "1px solid #22414F",
    borderRadius: 12,
    padding: 24,
  }}
>
  <header style={{ marginBottom: 16 }}>
    <h2 style={{ margin: 0, fontSize: 18, fontWeight: 600, color: "#F0EDE6" }}>
      Market positioning
    </h2>
    <p
      style={{
        margin: "4px 0 0",
        fontSize: 13,
        color: "#807E76",
        fontFamily: "ui-monospace, SFMono-Regular, Menlo, monospace",
      }}
    >
      Vacancy % vs. NNN asking rent · click a dot for detail
    </p>
  </header>
  <CorridorMarketScatter data={corridors} loading={false} />
</section>;
```

The chart filters out any corridor where `vacancy_pct` or `nnn_asking_rent_per_sqft` is null, so sparse data won't break it.

## Types

All component props come from `@/types/viz.ts`. Key interfaces:

- `CorridorEntry` — one CRE corridor row (id, name, submarket, rent, vacancy, absorption)
- `ZHVIMonth` / `ZHVITrendEntry` — monthly home value row (nulls filtered before chart render)

## Need something?

Just ask.
