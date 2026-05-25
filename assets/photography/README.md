# SWFL Data Gulf — photography references

Curated by Ricky. 18 images across 5 folders, organized by which scene of the landing-page script they fit (see `docs/fiverr-briefs/handoff-landing-embeds.md`).

**Tell Ricky which ones to keep or kill** — these are intentionally a wide spread, not a final pick. Stock comps are watermarked on purpose so the licensing path stays honest.

---

## Licensing summary (read this first)

| Source                                        | License                                     | Safe to publish?                                             |
| --------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ |
| NASA (ISS, MODIS, Landsat, Aqua, Goddard SVS) | Public domain                               | ✅ Yes — credit "Image: NASA"                                |
| Wikimedia Commons                             | Creative Commons (attribution required)     | ✅ Yes — credit file's CC license + author per the file page |
| Earth@Home (uni-edu)                          | Likely free for educational use             | ⚠️ Verify license on the source page before use              |
| Naples Daily News, Gulfshore Business         | Editorial copyright                         | ❌ Reference only — needs paid license or removal            |
| prodrones.com                                 | Editorial / agency copyright                | ❌ Reference only — needs license                            |
| Alamy stock comps                             | Watermarked previews — explicitly comp-only | ❌ Reference only — license via Alamy or kill                |

Bottom line: **the NASA images and the Wikimedia Cape Coral shot are the only ones that can be published as-is.** Everything else is a "this is what we're aiming for" reference until licensing is sorted.

---

## Scene 1 — Hero (`scene1-hero-aerials/`)

The script calls for: _"A dark, near-black aerial view of the Gulf coastline — Naples, Marco Island, Fort Myers Beach rendered in a stylized 3D topographic map. Not photorealistic."_

These are the **base photographs** to inspire the stylized 3D treatment Saimum's team will build with three.js + GLSL. Don't use them raw — they're references for color, mood, and geographic accuracy.

| File                                              | Source                               | Why this one                                                                                                                                                       |
| ------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `01-nasa-iss069-florida-from-orbit-5568x3712.jpg` | NASA ISS Expedition 69 (PD)          | **Top pick.** Real orbital photo. Dark Gulf, peninsular outline, lighting matches the script's "dark, near-black" mood.                                            |
| `02-nasa-aqua-florida-peninsula-4000x4000.jpg`    | NASA Aqua satellite, 250m/pixel (PD) | Wider context — entire Florida peninsula. Useful as the Scene 2 "zoom-out" beat or a stylized basemap.                                                             |
| `03-nasa-landsat-tampa-gulf-2196x2196.jpg`        | NASA Landsat 7 ETM+ (PD)             | Sharper coastline detail than [01]. Tampa-region but the SWFL portion can be cropped.                                                                              |
| `04-nasa-iss041-florida-coast-2128x1416.jpg`      | NASA ISS Expedition 41 (PD)          | Alt orbital angle / lighting. Use as a transition frame between scenes 1 and 2.                                                                                    |
| `05-nasa-modis-florida-1956x1372.jpg`             | NASA MODIS (PD)                      | Wider context shot. Could be flattened + recolored as the Scene 2 data-river basemap.                                                                              |
| `06-florida-platform-bathymetry-2000x1125.jpg`    | Earth@Home (likely CC-edu)           | The carbonate-shelf bathymetric map. Direct reference for the script's "stylized 3D topographic map" call. **Verify the source page's license before publishing.** |

---

## Scene 1 / 5 — SWFL location specifics (`scene1-swfl-locations/`)

The script calls out specific data-node locations in Scene 1: _"An SBA loan cluster in Cape Coral. A CRE vacancy hotspot on the US-41 corridor. Storm surge risk rings around Estero Bay."_ These are direct references for those callouts.

| File                                               | Source                              | Why this one                                                                                                                               |
| -------------------------------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `07-wikimedia-cape-coral-canals-2816x2112.jpg`     | Wikimedia Commons (CC, attribution) | The canal grid IS Cape Coral's visual signature. Maps directly to the script's "SBA loan cluster in Cape Coral" node. **Safe to publish.** |
| `08-prodrones-fort-myers-beach-dji-2560x1706.webp` | prodrones.com (editorial)           | High-quality FMB drone HDR. **Reference only** — license check required before publishing.                                                 |

---

## Scene 6 — Origin story (`scene6-downtown/`)

The script calls for: _"a photo or stylized illustration of downtown Naples + Fort Myers skyline."_ Two editorial references; both need licensing before use.

| File                                         | Source                         | Why this one                                                                            |
| -------------------------------------------- | ------------------------------ | --------------------------------------------------------------------------------------- |
| `09-naples-news-5th-ave-south-5472x3648.jpg` | Naples Daily News (editorial)  | Highest-res Naples downtown shot in the search. **Editorial — license required.**       |
| `10-gulfshore-business-naples-1024x576.jpg`  | Gulfshore Business (editorial) | Lower-res Naples downtown. Use as backup if [09] can't be licensed. **Editorial only.** |

> **Gap:** No usable downtown Fort Myers / Caloosahatchee shot landed in the searches. The Fort Myers searches returned mostly stock-watermarked comps. If you need a downtown Fort Myers reference, either license one from Alamy/Getty or have Saimum's 3D team illustrate it from the wordmark/style guide.

---

## Scene 7 — Footer water texture (`scene7-water-texture/`)

The script calls for: _"Gulf water texture (subtle, slow CSS animation)."_

| File                                                 | Source                | Why this one                                                                                                                                                           |
| ---------------------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `11-nasa-gulf-of-mexico-phytoplankton-4104x2304.png` | NASA Goddard SVS (PD) | False-color Gulf phytoplankton bloom. **Desaturate to gulf-midnight (#0A1419)** and the swirl reads as an abstract dark-water texture. Public domain, safe to publish. |

---

## Reference — stock comps (`reference-stock-watermarked/`)

These are **watermarked Alamy previews — REFERENCE ONLY**. They show what kinds of shots are commercially available for licensing. Pick the ones that work for the build, then either license via Alamy or commission Saimum's drone designer to recreate the shot.

| File                                              | Maps to                                                                              |
| ------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `alamy-fort-myers-beach-aerial-comp-1300x956.jpg` | FMB direct overhead — general hero/map use                                           |
| `alamy-fmb-sanibel-estero-bay-comp-1300x956.jpg`  | **Best location-bundle frame in the search.** FMB + Sanibel + Estero Bay in one shot |
| `alamy-marco-island-aerial-comp-1300x956.jpg`     | Marco Island — Scene 1 hero coastline callout                                        |
| `alamy-sanibel-san-carlos-bay-comp-1300x956.jpg`  | Sanibel + San Carlos Bay + Tarpon Bay (Lee County water inlet)                       |
| `alamy-sanibel-captiva-pair-comp-1300x956.jpg`    | Sanibel + Captiva — Lee County barrier islands                                       |
| `alamy-estero-bay-comp-1300x952.jpg`              | Estero Bay direct — Scene 1 "storm surge risk rings" callout                         |
| `alamy-fmb-sunset-comp-1300x843.jpg`              | FMB at sunset — mood reference for the script's dark/atmospheric tone                |

---

## Sourcing notes for Ricky / Saimum

What's missing from the search that we may want to commission or license:

- **Downtown Fort Myers skyline / Caloosahatchee** — no clean editorial-or-PD shot. Stock has comps; license via Alamy or Getty.
- **I-75 corridor aerial** — Scene 1 calls for "Traffic flow lines on I-75 glowing like fiber optic strands." We have no direct I-75 shot; this is probably a Mapbox/deck.gl render rather than photography.
- **Naples Airport-Pulling industrial corridor (the live data nub)** — would pair with Scene 5's map layer, but no aerials surfaced.
- **Bonita Springs / Estero (the "next ring out" growth zone)** — nothing in the results.

Anything in the "Reference — stock comps" folder we like enough to keep: I (Ricky) handle the Alamy licensing. Don't ship the watermarked comps to production under any circumstance.
