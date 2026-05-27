# Data tables for Scene 3 chart cards

Three tables, two formats each (CSV + JSON twin). Schema documented below.

**Contract:**

- **Column names + types are fixed.** Don't rename columns or change types when row values update — downstream chart components are bound to the schema below.
- **Row values change over time.** New brain refresh runs produce new row values, new rows, or removed rows — but the table shape stays the same.
- **Each table has a `TOTAL` row at the bottom of the CSV** and a corresponding `totals` object in the JSON twin. Treat the TOTAL row as a separate record — your chart filter logic should drop any row where the identifier column equals `TOTAL`.
- **Freshness token + brain source URL are in each JSON's header.** When you re-fetch, the token changes; otherwise the data is the same.

If a column or type ever needs to change, that's a v2 schema bump — it'll come with a CHANGELOG entry in this folder, not a silent edit.

---

## 1. `cre-corridors.{csv,json}` — Card 2 (CRE Vacancy Corridor)

**Source:** Supabase `corridor_profiles` table (verified, non-deleted rows)
**Brain:** `cre-swfl` — `https://www.swfldatagulf.com/api/b/cre-swfl?view=speak&tier=2`
**Row count:** 26 (Lee + Collier counties)
**Refresh cadence:** weekly

| Column                | Type          | Notes                                                                      |
| --------------------- | ------------- | -------------------------------------------------------------------------- |
| `corridor_id`         | string        | URL-safe slug — stable identifier, use this as React key                   |
| `corridor_name`       | string        | Display name                                                               |
| `city`                | string        | One of: Naples, Fort Myers, Estero, Bonita Springs, Cape Coral, Fort Myers Beach |
| `county`              | string        | Derived from city — Naples → Collier, all others → Lee                     |
| `corridor_type`       | string        | One of: highway-strip-mall, beachfront-tourism, anchor-dependent, mixed-use-downtown, suburban-residential, industrial-flex, medical-anchored, unknown |
| `seasonal_index`      | number (0–1)  | 0 = no seasonality, 1 = extreme seasonality                                |
| `cap_rate_pct`        | number\|null  | Cap rate, percent (e.g. `6.7` means 6.7%). Nullable.                       |
| `vacancy_rate_pct`    | number\|null  | Vacancy rate, percent. Nullable.                                           |
| `absorption_sqft`     | int\|null     | Net absorption in square feet, signed (negative = give-back). Nullable.    |
| `asking_rent_psf_nnn` | number\|null  | Asking rent per sqft, NNN. Nullable.                                       |
| `metrics_period`      | string        | Quarter the metrics reflect, e.g. `2026-Q1`                                |

**TOTAL row in CSV:** averages for cap/vacancy/rent, sum for absorption_sqft.

---

## 2. `franchise-survival.{csv,json}` — Card 1 (Franchise Survival Map)

**Source:** SBA 7(a)/504 franchise loan outcomes — Lee + Collier counties, FL (`sba_loans_franchise_outcomes` materialized view)
**Brain:** `franchise-outcomes` — `https://www.swfldatagulf.com/api/b/franchise-outcomes?view=speak&tier=3`
**Row count:** 15 brands (14 assessable + 1 unassessable)
**Refresh cadence:** quarterly

| Column              | Type         | Notes                                                                                       |
| ------------------- | ------------ | ------------------------------------------------------------------------------------------- |
| `franchise_name`    | string       | Display name (Subway, Dunkin', etc.)                                                        |
| `resolved_loans`    | int          | Count of resolved loans (paid_in_full + charged_off). Excludes still-active loans.          |
| `charged_off`       | int          | Loans charged off                                                                           |
| `survival_rate_pct` | number\|null | `paid_in_full / resolved_loans × 100`. Null when `resolved_loans = 0` (Mathnasium).         |

**TOTAL row in CSV:** `resolved_loans` and `charged_off` summed; `survival_rate_pct` is the **overall** rate across all brands (78.1%), not the average of per-brand rates.

**Important:** small-sample rates (e.g. Cold Stone Creamery with 1 resolved loan) are directional, not definitive — the brain stays honest about this in the source. If the chart shows these brands, consider sizing the marker by `resolved_loans` so the eye reads sample weight.

---

## 3. `freight-flows.{csv,json}` — Card 3 (Freight Flow Sankey)

**Source:** FAF5.7.1 freight flows (ORNL/FHWA Cold Lane Parquet; year 2024; dms_dest=129, trade_type=1) — `https://faf.ornl.gov/faf5/`
**Brain:** `logistics-swfl` — `https://www.swfldatagulf.com/api/b/logistics-swfl?view=speak&tier=3`
**Row count:** 4 origin rows + 4 commodity rows + 1 TOTAL = 9 rows
**Refresh cadence:** annual (next FAF5 vintage drops late 2026)

**CSV columns** (single table, two row types distinguished by `type`):

| Column                 | Type         | Notes                                                                  |
| ---------------------- | ------------ | ---------------------------------------------------------------------- |
| `type`                 | string       | `origin`, `commodity`, or `TOTAL`                                      |
| `rank`                 | int\|empty   | 1, 2, 3, or 4 (4 = the rolled-up "Other" bucket). Empty on TOTAL.      |
| `name`                 | string       | Display name                                                           |
| `faf_zone_code`        | int\|empty   | FAF5 zone code (origins only)                                          |
| `sctg_code`            | int\|empty   | SCTG commodity class code (commodities only)                           |
| `state`                | string\|empty | State abbreviation (origins only)                                     |
| `tons_thousands`       | number       | Inbound tonnage, thousands of tons                                     |
| `value_usd_millions`   | number       | Inbound value, millions of USD                                         |
| `share_of_tons_pct`    | number       | Share of total tons, percent                                           |

**JSON twin** separates this into `top_origins` and `top_commodities` arrays plus a `sankey_flows` array shaped for d3-sankey:

```json
{
  "source": "Tampa-St. Petersburg",
  "target": "SWFL (FAF zone 129)",
  "tons_thousands": 4411.1
}
```

The `sankey_flows` array routes through SWFL as a central hub node so every flow value ties back to a published aggregate (origins on the left, commodities on the right, SWFL in the middle). If you need a true bipartite Sankey (origin → commodity directly), it requires reading the FAF5 Parquet — not exposed via the brain API today. Tell Ricky and a separate row-level export can be wired.

---

## How to refresh

When numbers go stale (`freshness_token` changes on the brain), Ricky re-runs the brain on his end and re-pushes this folder. Column names + types stay fixed across refreshes. If they ever need to change, it'll come with a `CHANGELOG.md` entry in this folder.

## Live data alternative

If you'd rather fetch live than work from static files, every table here has a brain endpoint:

- `https://www.swfldatagulf.com/api/b/cre-swfl?view=speak&tier=2`
- `https://www.swfldatagulf.com/api/b/franchise-outcomes?view=speak&tier=3`
- `https://www.swfldatagulf.com/api/b/logistics-swfl?view=speak&tier=3`

These return text+JSON. Two iframe-ready embeds also exist:

- `https://www.swfldatagulf.com/embed/charts` (already styled in Gulf palette)
- `https://www.swfldatagulf.com/embed/footer-token` (freshness card)

Pick whichever delivery channel works for your build — static tables or live fetch.
