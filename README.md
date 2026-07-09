# Seismic Risk and Actual Damage Analysis for General Santos City

**Program:** Data Engineering Pilipinas — Open Track (Cohort 1)  
**Builder:** Adriane Abunda  
**GitHub:** [AdrianeJone](https://github.com/AdrianeJone)  
**Timeline:** June 2026 – December 2026 (24 weeks)

---

## The Problem

On June 8, 2026 at 7:37 AM, a magnitude 7.8 tectonic earthquake struck offshore Maasim, Sarangani, one of the strongest to hit the Philippines. The earthquake was felt at intensities of I–VIII across Regions VIII, IX, X, XI, XII, BARMM, and CARAGA. A tsunami warning followed, with confirmed wave heights recorded at multiple coastal stations across Mindanao.

According to NDRRMC Situational Report No. 28 (as of July 8, 2026), the earthquake resulted in **94 deaths, 1,316 injuries, and 18 missing persons** across Mindanao. A total of 1,679,382 persons across 391,321 families were affected. Across the region, 113,415 houses were damaged, 95,029 of them totally destroyed, along with 1,964 infrastructure items costing an estimated ₱1.47 billion in damage. General Santos City was among the worst affected areas, sustaining widespread structural damage including collapsed buildings, a damaged university, and disruption to the city's airport and seaport.

What makes this event uniquely significant from a data perspective is that **PHIVOLCS had already done the risk assessment work.** In May 2025, just one year before the earthquake, DOST-PHIVOLCS officially turned over city-scale liquefaction and tsunami hazard maps specifically for General Santos City to the local government. These maps were developed using advanced geophysical, geotechnical, and AI-driven methodologies under the ACER-DeLTA Project.

This raises a question worth answering with data:

> **Did the damage from the June 8, 2026 M7.8 earthquake actually occur where PHIVOLCS predicted it would?**

Specifically: do the barangays in General Santos City identified as high liquefaction and seismic risk zones match the barangays that reported the most damage after the earthquake?

---

## Why This Matters

If the hazard maps accurately predicted where damage occurred, that validates them as reliable planning tools for rebuilding and future-proofing the city. If they did not match, that is equally important, it tells engineers, urban planners, and LGUs where the maps need to be updated before the next earthquake.

The Cotabato Trench has produced multiple destructive earthquakes historically, including the 1976 Moro Gulf earthquake that killed roughly 8,000 people. The same PHIVOLCS DeLTA mapping project is being rolled out to other vulnerable cities nationwide. A data-driven validation of these maps for General Santos City could serve as a replicable framework for other cities across the Philippines.

---

## Data Source Notes

### Primary Source — Earthquake Catalog Data
- Name: PHIVOLCS Earthquake Bulletins
- URL: https://earthquake.phivolcs.dost.gov.ph/
- Format: HTML table (per-day bulletin), scrapeable
- Coverage: Daily seismic events nationwide, including magnitude, depth, location, and date/time, updated in near real-time
- Why it fits the problem: Provides the aftershock sequence and historical seismicity around General Santos/Sarangani needed for context and trend analysis.
- Known limitations: Published as daily HTML pages, not a single downloadable file — requires scraping across many days to build a full catalog.

### Fallback Source — Earthquake Catalog Data
- Name: USGS Earthquake API
- URL: https://earthquake.usgs.gov/fdsnws/event/1/
- Format: REST API (JSON/CSV/GeoJSON output)
- Coverage: Global earthquake catalog, filterable by location, date range, and magnitude — decades of history
- Why it could still work: Structured, direct API access with no scraping needed; can cross-check PHIVOLCS bulletin data or fill gaps.
- Known limitations: May report slightly different magnitude/depth values than PHIVOLCS due to different calculation methods.

---

### Primary Source — Hazard Prediction Data
- Name: PHIVOLCS Earthquake and Volcano-Related Hazard Maps (Liquefaction & Ground Shaking, General Santos City)
- URL: https://gisweb.phivolcs.dost.gov.ph/gisweb/earthquake-volcano-related-hazard-gis-information
- Format: KMZ (GIS-ready), some PDF/JPG previews
- Coverage: Barangay-level liquefaction and ground-rupture susceptibility for General Santos City and Sarangani, published 2018–2023
- Why it fits the problem: This is the actual pre-earthquake risk prediction I'm testing against real outcomes — the core comparison of my project.
- Known limitations: Requires submitting a request form (gisweb.phivolcs.dost.gov.ph/hazardmap) to receive a download link by email; some map layers are dated 2018–2021, not updated post-2026 quake.

### Fallback Source — Hazard Prediction Data
- Name: HazardHunterPH
- URL: https://hazardhunter.georisk.gov.ph
- Format: Interactive hazard-assessment tool (input a location/coordinates, get a hazard report back — not a bulk downloadable dataset)
- Coverage: Nationwide, point-based hazard lookup including liquefaction and ground shaking
- Why it could still work: Draws on the same underlying PHIVOLCS hazard data, accessible instantly without the email request step — usable to spot-check or fill gaps barangay by barangay.
- Known limitations: Must be queried one location at a time; not suited for bulk/automated ingestion.

---

### Primary Source — Actual Damage Data
- Name: NDRRMC Situational Report No. 28, Effects of M7.8 Earthquake in Maasim, Sarangani
- URL: https://ndrrmc.gov.ph/wp-content/uploads/2026/07/Situational_Report_No._28_for_the_Effects_of_Magnitude_7.8_Earthquake_in_Maasim_Sarangani_2026.pdf
- Format: PDF (latest of 28+ sequential reports)
- Coverage: Barangay/city-level casualty, housing, and infrastructure damage across affected regions, June 8 – ongoing (as of July 8, 2026)
- Why it fits the problem: This is my actual damage outcome data, to be joined against the hazard maps above.
- Known limitations: Figures are revised across reports as validation continues (deaths alone have shifted 19 → 35 → 46 → 65 → 77 → 88 → 94 across reports); requires parsing PDF tables; granularity mixes barangay, city, and provincial level.

### Fallback Source — Actual Damage Data
- Name: DSWD-DROMIC Report #58 on the Effects of Mw 7.8 Earthquake Incident in Maasim, Sarangani
- URL: https://dromic.dswd.gov.ph/wp-content/uploads/2026/07/DSWD-DROMIC-Report-58-on-the-Effects-of-Mw-7.8-Earthquake-Incident-in-Maasim-Sarangani-as-of-09-July-2026-6AM.pdf
- Format: PDF
- Coverage: Family/persons displaced and assisted, by barangay and evacuation center, updated near-daily
- Why it could still work: Independent agency data that can cross-validate NDRRMC's damage figures if the primary source has gaps.
- Known limitations: Focused on displacement/relief, not structural damage severity — less directly useful for the hazard-vs-damage comparison.

## Project Phases

| Phase | Weeks | What I will build |
|-------|-------|-------------------|
| 1 — Foundations | 1–4 | Define problem, confirm data sources, set up repo |
| 2 — Data Collection | 5–6 | Ingest earthquake catalog via PHIVOLCS/USGS, download hazard map KMZ files, collect NDRRMC situational reports |
| 3 — Data Processing | 7–12 | Parse PDFs, clean and standardize barangay names, join hazard zone data with actual damage data |
| 4 — Analysis & Insights | 13–16 | Compare predicted vs actual damage per barangay, identify matches and mismatches, produce charts |
| 5 — Project Packaging | 17–20 | Polish pipeline, connect all scripts end-to-end, write documentation |
| 6 — Deployment | 21–24 | Deploy interactive geospatial dashboard via GitHub Pages |

---

## How to Run

*To be updated as the project progresses.*

```bash
# Phase 2 — Data ingestion
python scripts/ingest.py

# Phase 3 — Data transformation
python scripts/transform.py
```

---

## Key Findings

*To be updated after Phase 4.*

---

## Final Dashboard

*To be deployed in Phase 6.*

`https://adrianejone.github.io/dep-data-engineering-open-track-adriane/`


---

## Acknowledgements

- DOST-PHIVOLCS for publicly available seismic and hazard data
- NDRRMC for situational reports
- Philippine Space Agency (PhilSA) for satellite damage imagery
- Data Engineering Pilipinas Open Track organizing team and volunteers