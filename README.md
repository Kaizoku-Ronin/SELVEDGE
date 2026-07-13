# SELVEDGE

**Live app → https://kaizoku-ronin.github.io/SELVEDGE/**

A single-file US HTS classification workbench for textile-chain goods — piece goods, apparel, made-ups, footwear, and headgear (HTSUS Chapters 50–65). One self-contained HTML page: no server, no build step, no install. Open it, describe the goods, and get ranked candidate tariff lines with the US-specific provisions and trade-remedy overlays already applied.

> **Decision support, not rulings.** Candidates come from the loaded HTS revision. Final classification, PGA treatment, and entry filing are the responsibility of the importer and their licensed customs broker. Verify rates and Chapter 99 overlays at [hts.usitc.gov](https://hts.usitc.gov) as of the entry date.

## What it does

Six tabs, one page:

- **Fabric (Ch 50–60)** — woven and knit piece goods: fiber blend, weave/knit type, g/m², width, average yarn number, finish, and Chapter 59 coating routing.
- **Apparel (Ch 61–62)** — garment type + construction + gender + fiber, with the US statistical provisions handled: the ≥23% wool-in-man-made provision, sweater-stitch counts (≤9 per 2 cm), worsted wool ≤18.5 micron dual codes, Chapter 62 water-resistant (Additional US Note 2) shown as both branches when unknown, unisex → women's, babies ≤86 cm, and the camisole and knit-blazer traps.
- **Made-ups (Ch 63)** — bed / table / toilet / kitchen linen and other made-ups, with printed / napped / terry / embroidery splits.
- **Footwear (Ch 64)** — upper + sole materials decide the heading; sports type, ankle coverage, gender/size run, and value-per-pair bands decide the line. EVA / GOMMA TR / MICRO soles read as rubber.
- **Headgear (Ch 65)** — including the 6504 (plaited strips) vs 6505 (textile) trap.
- **Data** — dataset manager (see below).

Every result carries an origin-aware trade-remedy overlay (Section 301 chapter-aware: List 4A +7.5% for apparel and made-ups, List 3 +25% for piece goods; IEEPA status including the pre–Feb 24 2026 refund note) plus amber "confirm before filing" flags for anything the inputs left ambiguous.

## Batch mode

One workbook, five sheets — Fabrics · Apparel · MadeUps · Footwear · Headgear — all with dropdown validation. Download the template from the app, fill one item per row, and upload it back. Results render on screen and export as a styled results workbook with per-row HTS options, top MFN rate, trade-remedy flags, and confirm-notes.

## Dataset

Chapters 50–63 ship embedded (4,166 tariff lines from the USITC schedule). Chapters 64–65 load through a one-time import in the **Data** tab:

```
https://hts.usitc.gov/reststop/exportList?from=6401&to=6506&format=CSV
```

JSON and XLSX exports work too. The import is parsed locally, persisted in the browser, and included in the merged-dataset download.

To bake 64/65 in for every visitor: **Data tab → Download merged dataset**, then commit the resulting `selvedge-data.json` next to `index.html` in this repo — the page auto-loads it. The same import path refreshes chapters 50–63 whenever a new HTS revision publishes.

## Repo layout & deploying

```
index.html            the entire app (~1.2 MB, ~200 KB gzipped)
selvedge-data.json    optional baked dataset (Ch 64–65 + any refreshed chapters)
```

Fork it, enable GitHub Pages (Settings → Pages → Deploy from a branch → `main`, root), done. Everything runs client-side; the only network calls are Google Fonts, the ExcelJS CDN (batch mode only), and whatever you import from hts.usitc.gov.

## Privacy

No analytics, no backend, nothing leaves the browser. Imported datasets live in `localStorage`.
