# Selvedge — single-file HTS classifier (v4.0)

A self-contained `index.html` that routes and classifies goods across **HTSUS Chapters 42, 50–65, 71 and 94**, encoding a working entry writer's methodology: heading routing, line-level discrimination, statistical-suffix logic, trade-remedy overlays and confirm-before-filing flags. It runs entirely in the browser (GitHub Pages friendly), with a sidecar dataset `selvedge-data.json` carrying the full 2026 tariff schedule (23,514 leaf lines, 98 chapters).

Everything it produces is a **candidate, not a ruling** — the licensed broker signs the entry.

## What's new in v4.0 (Tier 2)

Three methodology engines join the original textile stack, each built from a line-by-line study of the real tariff tree:

- **Leather goods — Ch 42** (`Leather` tab)
- **Furniture & lighting — Ch 94** (`Furniture` tab)
- **Jewelry — Ch 71** (`Jewelry` tab)

The batch workbook grows from five category sheets to **eight**. Chapters 42/71/94 are not embedded in the HTML — they load from `selvedge-data.json` (auto-fetched when hosted beside the page) or a one-time USITC import in the **Data** tab.

## Tabs

**Fabric 50–60 · Apparel 61–62 · Made-ups 63 · Footwear 64 · Headgear 65 · Search** — unchanged from v3.1: fiber-blend chief-weight logic with the wool-in-MMF provision, sweater-stitch and worsted dual codes, unisex→women's and babies ≤86 cm routing, coat/jacket splits, knit-blazer trap, EVA/rubber sole logic, ankle dual flag, 6504-vs-6505 trap, and a full-schedule keyword/prefix Search across all 98 chapters (Ch 98/99 excluded from keyword results unless targeted by prefix).

### Leather — Ch 42

Sixteen article families route through group tokens (trunks/attachés · handbags · pocket-and-handbag articles · second-enumeration containers), then the outer-surface lanes split leather/composition, sheeting of plastics, textile (with a cotton / other-vegetable / man-made / silk ≥85% / paper-yarn fiber picker) and other materials. Encoded line logic includes the handbag **$20 value band** (4202.21.60 vs .90), **reptile** exclusivity with prefix conflicts, the **braid** lane (shown but ranked below its mainstream twin when unknown), **structured-rigid** luggage splits, leather travel bags living in **4202.91** (not .92), the MMF **backpack** statistical line 4202.92.3120, insulated/musical-instrument/jewelry-box/CD lanes, glove sports lanes (baseball/batting, ski, cross-country, hockey, golf) plus the horsehide-cowhide branch, lined × gender dress-glove splits and the not-seamed line, belts at 4203.30.0000, leather apparel with anorak and gender splits, pet articles in 4201, and straps/shoelaces in 4205 with machinery-use lines excluded.

Flags raised: **CITES + FWS Form 3-177** wildlife clearance for exotic skins, the **coated-canvas visible-surface** determination (sheeting vs textile — the duty gap is large), the fourchette/sidewall construction split on horsehide gloves, the **watch-strap → 9113.90** trap, and pocket-article scope notes for spectacle cases.

### Furniture & lighting — Ch 94

Nine families (seats, case goods, mattresses, bedding, luminaires, medical, and three parts lanes). Seats: special-use aircraft/motor-vehicle/child-safety routing with reverse conflicts, swivel-height and convertible-into-bed lines, the frame matrix (wood / metal / rubber-plastics ± reinforced-laminated / bamboo / rattan / cane), upholstered-vs-unlabeled-sibling logic, outdoor with textile-cushion splits, household default-on, children's-article lines (highchairs, walkers, bouncers, swings, activity centers), bent-wood, and the **teak / plantation-harvested teak** statistical splits. Case goods: office/kitchen/bedroom room routing, beds · dining tables · permanent-install cabinets · filing cabinets · racks/shelving · storage lockers · ironing boards, and the wood-species statistical lines (**rosewood/Dalbergia, padauk/narra, wenge, teak**). Mattresses split by cellular rubber-plastics / cotton / uncovered innerspring and by crib vs **>91×184 cm** sizes. Bedding: comforters (plain cotton 4.4% vs outer-shell cotton/MMF/silk lanes at 12.8%), sleeping bags on the **≥20% feathers** split, pillows by cotton covering and foam/other fill, mattress supports. Luminaires: the **LED-solely × brass/base-metal × household** grid across ceiling/wall, lamps, other-electric (incl. photovoltaic), non-electric, illuminated signs, and parts.

Flags raised: wooden bedroom furniture from China → **ADD A-570-890**; mattresses → multi-country AD orders (**A-570-092** China plus the 2021 KH/ID/MY/RS/TH/TR/VN orders); metal furniture, racks and lockers → **Section 232 derivatives** with the metal-content **value-split** and melt-and-pour reporting; wooden furniture → **TSCA Title VI** composite-wood certification and **Lacey PPQ 505**; Dalbergia → **CITES App. II**; plantation-teak claims → chain-of-custody; and the **GRI 3(b) configured-unit** note (a complete configured article — e.g. a Montana Pos line — classifies as one unit).

### Jewelry — Ch 71

Precious-metal articles (7113): the silver **$18/dozen** band, gold necklaces split **rope / mixed-link / other**, clasps, **ISO-platinum** per-article lines, the gold-articles 7113.19.5091 line (with exclusionary-clause-safe token matching), and the **continuous-length chain** lines that separate unfinished chain from finished necklaces; base-metal-clad lanes in 7113.20. Pearl and stone articles (7116): natural vs cultured pearls, and stone jewelry on the **$40/piece** band. Imitation jewelry (7117): base-metal vs other lanes, cuff links, chain **33¢/meter** bands, religious articles and rosaries, toy-jewelry lines, **20¢/dozen** and 30¢/dozen bands, and plastics costume jewelry landing **Free** at 7117.90.7500 while plated base metal takes 11%.

Flags raised: the **clad-vs-plated Note 7** trap (plated base metal is imitation jewelry in 7117; clad is 7113.20), silver value-band prompts, and **EO 14068 Russian-diamond** + **Kimberley Process** notes on stone articles. Loose stones, pearls and bullion route to a 7101–7110 information card — browse them with the Search tab.

## Batch mode

Download the eight-sheet template (Fabrics · Apparel · MadeUps · Footwear · Headgear · Leather · Furniture · Jewelry — every categorical column has dropdown validation from a hidden Lists sheet), fill it, and upload. Single-category CSVs also work; the category is auto-detected from a distinctive header (`Leather_article`, `Article_family`, `Jewelry_article`, …). Results come back as a workbook: Ref · Category · Item · Origin · Heading(s) · HTS options · Top MFN rate · Trade-remedy flags · Confirm-before-filing notes.

## Data tab

Chapters 50–63 are embedded (4,166 lines). The full schedule loads from `selvedge-data.json` when hosted alongside; anything can also be imported once from `hts.usitc.gov/reststop/exportList?from=XXXX&to=YYYY&format=CSV` and persists in localStorage (memory-only fallback when the quota is hit). Precedence: embedded < repo file < your imports.

## Trade remedies

Section 301 (China) renders as +25% (List 3) for Chapters 50–60 and +7.5% (List 4A) for 61–65; other chapters get an honest "line-specific — verify" with no invented estimate. The IEEPA reciprocal-tariff overlay was struck down Feb 20, 2026 and terminated Feb 24, 2026 — pre-Feb 24 China entries may be refund-eligible via reliquidation, PSC or protest; the info line stays in the remedy panel. Chapter 99 overlays appear in the remedy panel only, never as classification candidates.

## Deploy

Commit three files at the repo root and enable Pages:

```
index.html            (~1.30 MB — the entire app)
selvedge-data.json    (~7.09 MB — full-schedule dataset)
README.md
```

## Tests

200 assertions across five jsdom suites run against the real dataset: 69 core (textile methodology, batch, data layer) · 28 search · 27 leather · 42 furniture · 34 jewelry.

## Honest limits

Candidates, not rulings — amber flags defer to the licensed broker. Statistical suffixes are best-effort from the loaded revision. There is no CBP rulings database behind this; value bands need values; unknown toggles show both branches with the mainstream line ranked first. ADD/CVD and 232 flags are prompts to scope-check, not scope determinations.
