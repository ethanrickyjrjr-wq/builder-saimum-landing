# Scroll Story v2 — "The Deal" (LOCKED)

**Status:** Locked, 2026-05-25
**Supersedes:** the 7-scene script in `docs/fiverr-briefs/handoff-landing-embeds.md`
**Reference assets:** `images/` in this review folder, plus existing `assets/photography/*` on the builder repo's `assets/photography-references` branch

---

## Status banner for the builder — read first

- **Live ingestion + tech specs are still being finalized on our side.** Don't wait on it. Every live-data slot in this doc has a static/fallback render that ships first and swaps to live when the API is ready. Framer build proceeds in parallel.
- **A dedicated "live data" next page** will be built after the landing to showcase the real-time intelligence in depth. The landing page only needs ONE live moment (Act 3 phone screen) to earn trust; the rest is the story.
- **All photography needs Ricky's approval before it enters the build.** See "Photo approval workflow" below — Saimum's team curates picks into a folder, Ricky greenlights, then build.
- **Where the spec gives multiple options, pick one and ship — don't try to ship all variants.** See "Builder options menu" at the bottom.

---

## One-line pitch

Pull in from orbit. Drop into the city. Watch real-world data fly into a phone. Watch it overwhelm. Watch Brains clean it into a one-line answer. Quiet send. The deal moves.

Same shape as a working professional's actual day. No abstract "data river." A literal phone, literal city, literal numbers, literal action.

---

## What changed from the concept draft

Pushback round with LittleBird (prior Sonnet) surfaced the following:

| Change                                                                           | Why                                                                                                                                                              |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Three-altitude opener (NASA orbit → drone Estero Bay → street level)             | Single altitude flattens the arc. Three altitudes earns the "we see everything" claim.                                                                           |
| Time-of-day arcs (golden hour Act 1 → blue hour Act 2 → night Act 4–5)           | Lighting carries the emotional shift. Blue-hour-everything was half-right and over-applied.                                                                      |
| Act 4 "DATA OVERLOAD" caps headline removed                                      | Telling the viewer it's overload breaks the spell. The visual chaos has to do the work.                                                                          |
| Pinned phone = clean device mockup, not Pexels hand-with-phone                   | Stock hand shots are composite hell and read as template. Mockup keeps the product as the hero.                                                                  |
| Act 5 = two rotating readouts (CRE + hospitality), scroll-triggered              | One persona boxes in the audience. Auto-rotate fights reading pace. Scroll-triggered keeps the visitor in control.                                               |
| Final beat = quiet "Sent to Maria — 2:47 PM" timestamp, not "DEAL CLOSED"        | "DEAL CLOSED" is broker-only language and on-the-nose. The confidence moment is the send, not the close.                                                         |
| Closer = "Built in Southwest Florida"                                            | "Real closes" is salesy. "Built between the bridges" is too local-inside. SWFL reads instantly for everyone.                                                     |
| Particles → Linear-style glowing connector lines                                 | Three.js particles are expensive and look cheap unless heavily polished. Lines from annotations to phone are cheaper, more intentional, and tell the same story. |
| Live data moment = Act 3 phone screen, real iframe of `/embed/cards/asking-rent` | The trust receipt. Inspect the freshness token, get a real value back. One live moment is enough; the rest can be static.                                        |

**Overruled from LittleBird's critique:**

- "$4.2B in CRE changed hands last year" opener — invented number, violates the Data Provenance rule. See Act 1 below for the conditional handling.
- Specific local vendor names (iSky Films, Deborah Sandidge, Jack Cook) — not verified, not actionable. Vendor selection is a separate vetting pass.
- "Kill the NASA orbital opener" — kept it as the highest altitude beat in a three-altitude arc.
- "Blue-hour everything" — kept blue-hour for Act 2, golden hour for Act 1, night for Acts 4–5.

---

## The arc — 5 acts, one continuous scroll

### ACT 1 — The altitude pull-in

Three altitudes in one scroll:

1. **Satellite (open).** NASA Black Marble — Florida glowing at night from orbit. Slow Ken Burns push in.
2. **Drone (mid-act).** Estero Bay at golden hour, 400 ft AGL, looking northeast. Mainland coastline glowing warm, Sanibel and the causeway clear in frame.
3. **Street level (act close).** Land on Fort Myers River District or Naples 5th Ave South, golden-hour ground level.

**Headline (fades in over satellite):**

> Every deal in Lee and Collier starts with a question nobody can answer fast enough.

**Subhead (drone altitude):**

> Most of it never leaves the spreadsheet it was born in.

**Conditional opener variant — only ship if backed by a real, citeable number from the brains:**

> Lee and Collier moved **[$X.XB]** in commercial real estate last year.
> Most of the numbers behind it never left the spreadsheet they were born in.

`[$X.XB]` becomes a clickable inline citation linking to `/r/master` or the provenance page (`/r/source/[table]`). If the brain cannot produce a defensible figure with a source chain in time for launch, ship the qualitative version. **Do not ship a magic number on the hero.**

**Image references:**

- `images/act1-gulf-into-cities/naples-historic-downtown-wikimedia.jpg` — street-level land
- `images/act1-gulf-into-cities/naples-bayside-panorama-wikimedia.jpg` — alt street-level
- Existing builder branch `assets/photography/scene1-hero-aerials/` — for the satellite/drone beats
- Drone-altitude footage is a **gap** — see "Outstanding gaps" below

**Scroll trigger:** continuous scrub across the three altitudes; no hard cuts.

---

### ACT 2 — Drop into the city, data populates around you

Camera is now at street level (blue hour now — the sun has set, the city is lit, the day's work is on). Real Fort Myers / Naples backdrop. As the user scrolls, **data annotations fade in around the buildings**, each one connected to its subject by a **thin glowing teal line**:

- Construction crane on a skyline → **`+47 permits this month`**
- Storefront → **`survival rate 78%`**
- Beach with tourists → **`TDT +12.5% YoY`**
- Storm cloud in the sky → **`flood AAL $18,400/yr`**
- Highway in the distance → **`AADT +4.2%`**

Same teal-glow treatment as `components/charts/HBarChart.tsx`. **All numbers are pulled live from the brains, not invented.** Each annotation hover/tap reveals the source citation.

The connector lines are the visual seed for Act 3 — they're already pointing at where the phone will appear.

**Background plates (multi-image cross-fade as the user scrolls):**

- `images/act1-gulf-into-cities/` (blue-hour treated)
- Builder branch `assets/photography/beautiful-swfl/fort-myers-river-district-*.jpg`
- Builder branch `assets/photography/beautiful-swfl/naples-5th-avenue-south-*.jpg`

**Data subject insets (starter references — final picks come from Saimum's curation per "Photo approval workflow"):**

- `images/act2-data-populating/fort-myers-beach-tourists-emilymkrause-2500x1667.jpeg` → tourism annotation (personal-blog source, license check required)
- `images/act2-data-populating/nasa-hurricane-irma-night-satellite-1336x1736.jpg` → weather/storm annotation (NASA PD)
- `images/act2-data-populating/nasa-black-marble-florida-night-lights-1024x576.jpg` → "cities lit from data" mood frame (NASA PD)
- **Construction-crane shot for the permits annotation: gap** — needs to be sourced or shot fresh. Tampa Bay Times image was downloaded as a license-required reference; not committed.

**Headline (mid-scroll):**

> Permits. Storms. Tourism. Cap rates. Traffic.
> Every block has a number behind it — and nobody's connected them.

---

### ACT 3 — The phone enters, the lines collapse inward

A **clean iPhone device mockup** (Figma Apple device library, transparent PNG, tilted ~15°) enters the frame from below and pins to the center of the viewport. From here through Act 5, **the phone stays pinned** — the city background continues to scroll behind it.

As the phone arrives, the glowing connector lines from Act 2 **shorten and collapse toward the phone screen**. The annotations disappear into the device. Linear-style, not particle-based.

**The phone screen is live.** It renders an actual iframe of `/embed/cards/asking-rent`:

- Real corridor names
- Real asking-rent values
- Real freshness token visible at the bottom of the card
- Inspect-the-page check passes — the trust receipt

This is the one live-data moment in the whole scroll. Everything else can be static/animated.

**Headline:**

> Until now.

(Two words. The visual does the work.)

**Reference for phone composition:** the Pexels phone-in-hand shots in `images/act3-phone-pov/` are **for inspiration only** — we are NOT compositing on top of a stranger's hand. Use a clean device mockup instead.

---

### ACT 4 — Overload → black → thinking

The phone screen begins to fill. Charts overlap. Numbers stack. The teal glow flickers and dims. The scroll velocity of the user is creating the mess — the more they scroll, the more chaotic the screen.

**No headline. No "DATA OVERLOAD" text.** The visual carries the beat.

One full beat of black on the phone screen.

Three dots appear, iMessage-style, in teal.

**Label under the dots:**

> Asking Brains…

(Not "Connecting to your AI" — that's product-agnostic and vague. Not "Thinking" — that's bland. "Asking Brains" names the product and makes the wait feel earned.)

**Reference:** iMessage typing-indicator (3 teal dots) — visual model only; render in Framer/CSS, no committed image asset needed.

---

### ACT 5 — The clean readout (rotating), then the quiet send

The phone screen wipes to a clean Claude-style chat readout. The visual model is `assets/screenshots/03-tourism-claude-output.png` on the builder repo's `ref/hbar-chart-and-screenshots` branch — same format, tightened to phone aspect ratio, Gulf palette.

**Two readouts rotate on scroll-triggered swap** (not auto-rotate — auto-rotate fights the user's reading pace and implies one readout is the "real" one). The user scrolls past readout A, scrolls back to it, then scrolls forward and readout B appears.

#### Readout A — CRE

```
Should I close on Capones for $1.2M at 6.5% cap?

Brains says: Conditional yes.

Cap is 30 bps tight to corridor median ($1.18M
implied at 6.2%) but tourism is +12.5% YoY and
the corridor sits below permit saturation.

Walk if the seller won't budge on the storm
addendum. Otherwise, sign.

Freshness: SWFL-7421-v52-20260525
```

#### Readout B — Hospitality

```
Should I renew the Naples Beach Hotel franchise at
the proposed royalty bump?

Brains says: Push back.

Tourism is up but room-night ADR is flat — the
royalty bump compresses your margin by ~80 bps
in a year where occupancy hasn't recovered to
pre-Ian baseline at the property type.

Counter with a 2-yr step-up tied to ADR recovery.

Freshness: SWFL-7421-v52-20260525
```

Both readouts are placeholders. **Before launch, run both questions through `/api/b/master?view=speak&tier=2` and quote the actual responses verbatim** — including the real freshness token. If the brain can't yet answer the hospitality question with conviction, swap in a different vertical (franchise, environmental) that it can.

The freshness token at the bottom of each readout is **rendered as a visible UI element**, not a footnote — it's the trust receipt that lets a skeptical visitor verify the answer is live.

**The quiet send (final beat):**

A timestamp line animates in below the readout:

> Sent to Maria — 2:47 PM

(Not "DEAL CLOSED." The confidence beat is the send — the moment of action taken on a good answer. The close is what happens next, off-screen.)

**Final headline below the phone:**

> Real data. Real answers. Built in Southwest Florida.

**CTAs stacked beneath — three distinct, named slots:**

1. **Live data slot →** "See the live intelligence" — links to `/r/master` today. When the dedicated live-data next page ships, this CTA re-points there. The button label can stay; the destination is the variable.
2. **Email capture slot →** "Get the next read drop" — embed `/embed/waitlist` as an iframe directly inline (form lives on the page, no second click). This is the must-have conversion surface; do not let it bury below the fold.
3. **MCP install slot →** "Install Brains in Claude Desktop" — currently placeholder, label reads "coming soon". When MCP submission gets approved, this slot swaps to a real `claude://` deeplink + a copy-paste config snippet inside an expandable `<details>` block. Builder should leave a clearly named container (`#cta-mcp-install`) so the swap is a one-line content edit, not a rebuild.

**Email capture should also appear mid-scroll** — a sticky compact form (email field + "Get the drop" button) pinned to the bottom-right of the viewport from Act 2 onward, dismissable. Don't rely on the visitor making it to Act 5 to convert. **Builder option:** if the sticky feels intrusive, alternative is a single interstitial between Act 3 and Act 4 — "Want this in your inbox? Drop your email." with the same `/embed/waitlist` iframe. Pick one.

---

## Mobile + scroll-depth handling

**Do NOT pre-build a 3-act compressed mobile mode.** Ship the full 5-act version, instrument scroll-depth in PostHog, watch for 2–3 weeks. If mobile users are bailing in Act 2 at high rates, _then_ design a `?short=1` variant. Designing the fix before confirming the disease doubles Framer scope for a problem we haven't seen yet.

**Instrument the following events from day one:**

- `scroll_depth_25` / `50` / `75` / `100`
- `act_1_completed` … `act_5_completed`
- `readout_a_viewed` / `readout_b_viewed`
- `cta_master_click` / `cta_waitlist_submit` / `cta_mcp_click`
- Device class on every event (mobile / tablet / desktop)

---

## Visual constants (the whole scroll)

- **Phone pinned center** from Act 3 onward — background scrolls behind it, phone screen content changes
- **Real SWFL imagery in every background plate** — Naples / Fort Myers / Cape Coral / Sanibel / Fort Myers Beach. No generic stock cities.
- **Time-of-day arc:** golden hour (Act 1) → blue hour (Act 2) → night-with-screen-glow (Acts 4–5)
- **Teal `#3ecfb2` glow** for all annotations, connector lines, chart fills (matches `HBarChart.tsx`)
- **Dark mode throughout** — `#0F1923` page bg, `#162030` cards. Never flips to white.
- **Freshness token visible** on the live HBar chart (Act 3) and both Claude readouts (Act 5)
- **Real-data-or-animate rule (NEW).** Any photograph or scene that _displays a number_ must do one of two things:
  - **(a)** Show a real, current value pulled from the brains (preferred — matches Data Provenance rule), OR
  - **(b)** Animate the value as the user scrolls — counters tick up, charts redraw, annotations refresh. The "I'm walking through the city and getting better information the further I go" feel.
  - **Never** show a static fake number on a photo. A still photo with a frozen invented stat reads as a stock-template fake; a still photo with a number that ticks as the user scrolls reads as live intelligence.

---

## Technical build notes

### Framer path (if Saimum keeps the scope)

- **Scroll Effects + Pin** on the phone element from Act 3 onward
- Background plates: parallax stack with cross-fades on scroll progress
- Connector lines (Act 2 → Act 3 collapse): Framer Motion `useMotionValue` driving SVG `path` `stroke-dashoffset`
- Three dots: Framer Motion variants with staggered children
- Readout rotation in Act 5: scroll-progress-driven opacity swap on two stacked text blocks
- **Live HBar chart on the phone screen:** Framer's iframe embed pointed at `/embed/cards/asking-rent`. Test on mobile first — iframes inside pinned elements have known quirks.

### React / Next.js path (if v2 ports into the platform repo)

- **GSAP ScrollTrigger** for pin + scrubbed timeline — already a dependency (`HBarChart.tsx` uses it)
- **Framer Motion** for in-element animations
- **No Three.js needed** — the three-altitude opener is a CSS transform + image stack with parallax depth. Three.js is overkill.

### Reusable from the existing platform

| What                                                     | Where                             |
| -------------------------------------------------------- | --------------------------------- |
| HBar chart (Act 3 phone screen, live iframe)             | `/embed/cards/asking-rent`        |
| Footer freshness token (visual reference)                | `/embed/footer-token`             |
| Waitlist form (Act 5 CTA)                                | `/embed/waitlist`                 |
| Live brain API for Act 5 Claude readouts                 | `/api/b/master?view=speak&tier=2` |
| Provenance page (Act 1 conditional opener citation link) | `/r/source/[table]`               |

---

## Outstanding gaps before build

1. **Drone footage of Estero Bay at golden hour (Act 1, mid-altitude beat).** Not in inventory. Needs a local drone op shoot — half-day. Vendor selection is a separate vetting pass; don't commit to any specific operator without quote-and-reel review.

2. **Original SWFL phone-POV photography (Act 3 device entrance, optional flair).** The pinned phone is a clean mockup, but if we want a quick handheld shot at the moment the phone enters frame, it should be shot in Fort Myers or Naples — not a Pexels stock shot from an unknown city. Optional; skippable for v1.

3. **Clean iPhone device mockup PNG (Acts 3–5 pinned phone).** Free sources confirmed available:
   - Figma Apple Device Library — https://www.figma.com/community/file/1014241558865541418
   - Mockuups Studio — https://www.mockuuups.studio/
   - Apple's own 3rd-party device images — https://www.apple.com/legal/intellectual-property/guidelinesfor3rdparties.html
     Pick one before Framer build; mockup choice affects scene composition.

4. **Real Act 1 opener number.** Decision: pull a defensible Lee + Collier transaction-volume figure from the brains with a source chain that survives inspection. If not available by launch, ship the qualitative opener.

5. **Real Act 5 readouts.** Both readouts (CRE + hospitality) need to be regenerated from `/api/b/master?view=speak&tier=2` immediately before launch so the freshness tokens and numbers are real. Plan to re-run them on a quarterly cadence so they don't go stale visually.

6. **"Sent to Maria — 2:47 PM" — confirm the name + time pattern.** Two options: (a) static name + time (current spec, simpler), or (b) personalized to local timezone with rotating names from a small approved list. Default to (a) for v1.

---

## Image inventory in this review folder

```
images/
├── act1-gulf-into-cities/
│   ├── naples-historic-downtown-wikimedia.jpg
│   └── naples-bayside-panorama-wikimedia.jpg
├── act2-data-populating/
│   ├── fort-myers-beach-tourists-emilymkrause-2500x1667.jpeg  (personal blog — ask)
│   ├── nasa-hurricane-irma-night-satellite-1336x1736.jpg      (NASA PD)
│   └── nasa-black-marble-florida-night-lights-1024x576.jpg    (NASA PD)
├── act3-phone-pov/
│   ├── pexels-phone-in-hand-city-pov-4000x6000.jpg            (REFERENCE ONLY — using mockup instead)
│   └── pexels-phone-in-hand-city-pov-alt-4000x6000.jpg        (REFERENCE ONLY)
├── act4-overload-to-clean/
│   └── dribbble-dark-dashboard-mobile-4804x3602.png           (REFERENCE ONLY — designer copyright)
├── act5-deal-closed/                                          (empty — render in Framer)
└── iphone-mockup-references/                                  (empty — to be added from Figma library)
```

Already on builder repo, reused from `assets/photography-references` branch:

- `assets/photography/scene1-hero-aerials/` — Act 1 satellite + drone-altitude options
- `assets/photography/beautiful-swfl/` — Act 2 city plates (apply blue-hour color grade)
- `assets/screenshots/04-hbar-chart-with-tooltip.png` — Act 3 chart visual reference (live iframe is the real render)
- `assets/screenshots/01-logo-current.png` — Act 4/5 logo
- `assets/screenshots/03-tourism-claude-output.png` — Act 5 readout visual model

---

## Photo approval workflow — must follow

**No photograph enters the build until Ricky has signed off on it.** The images in this review folder are starting references, not approved assets.

**Workflow:**

1. **Saimum's team curates picks** into a new folder at `assets/scroll-story-v2/curated-picks/` on the builder repo. Subfolder per act (mirrors the structure in `images/`). Each pick is named `actN-shortdescription-WIDTHxHEIGHT.ext` so Ricky can scan filenames at a glance.
2. **Each pick gets a one-line caption** in a `picks-notes.md` file alongside the images — what it's for (which act/beat), source URL, license posture (PD / CC / editorial / paid).
3. **Ricky reviews the folder**, marks `APPROVED` or `REJECTED` in `picks-notes.md`, and adds short reason on rejects.
4. **Only approved picks go into the Framer build.** Rejected picks stay in the folder for audit but don't enter scenes.
5. **For any photo showing data** (data overlay on a real photo), the data values must follow the **real-data-or-animate rule** in Visual Constants — Ricky also greenlights the data values themselves before they're hardcoded anywhere.

**Why this matters:** the wrong photo (generic stock, miscredited, low-res, off-brand, not actually SWFL) is the fastest way for a $5M-look landing to read like a Fiverr template. Confirmation gate is cheap; mis-shipped images are expensive to roll back.

---

## Builder options menu — pick one per row

Saimum has flexibility on the following; pick what fits the build budget and the Framer scope, don't try to ship all variants:

| Slot                     | Option A (lighter lift)                                            | Option B (more polish)                                                        |
| ------------------------ | ------------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| Act 1 satellite opener   | Static NASA Black Marble image with Ken Burns CSS push             | Animated 3D Earth → zoom-to-Florida (CesiumJS / Mapbox globe)                 |
| Act 1 drone mid-altitude | Stock golden-hour Estero Bay shot from Pexels/Unsplash placeholder | Original commissioned drone footage from a local SWFL operator                |
| Act 2 connector lines    | Static SVG paths with stroke-dashoffset scroll-scrubbed            | Animated particle stream along the same paths                                 |
| Act 2 data annotations   | Hand-authored placeholder values (later real)                      | Pulled from `/api/b/master` live at page-load (no value if API is down)       |
| Act 3 phone screen       | Static screenshot of HBar chart rendered as phone-sized PNG        | Live iframe of `/embed/cards/asking-rent` rendered in the device              |
| Act 5 readouts source    | Hardcoded placeholder JSON of two readouts                         | Fetched from `/api/b/master?view=speak&tier=2` at build-time, regen quarterly |
| Email capture placement  | Sticky bottom-right compact form from Act 2 onward                 | Single full-width interstitial between Act 3 and Act 4                        |
| Mobile rendering         | Identical scroll, scaled responsively                              | Tuned mobile variant with shortened pinned sections                           |

**Default recommendation for a fast first ship: all Option A's, then upgrade to Option B's on slots that earn the engagement in PostHog data.**

---

## Decision to make before push

**Replace or augment the 7-scene script?**

Recommended: **replace.** The 7-scene script advertises depth. v2 advertises outcome. Outcome closes more visitors on the landing page than depth does — and the depth still lives one click deep at `/r/master` for anyone who wants to inspect it.

If approved, the next step is pushing this doc + the images folder to the builder repo on a `concept/scroll-story-v2` branch, paired with a rewrite of `docs/fiverr-briefs/handoff-landing-embeds.md` that points Saimum at the v2 arc.
