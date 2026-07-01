# Seismic Risk and Actual Damage Analysis for General Santos City

**Program:** Data Engineering Pilipinas — Open Track (Cohort 1)  
**Builder:** Adriane Abunda  
**GitHub:** [AdrianeJone](https://github.com/AdrianeJone)  
**Timeline:** June 2026 – December 2026 (24 weeks)

---

## The Problem

On June 8, 2026 at 7:37 AM, a magnitude 7.8 tectonic earthquake struck offshore Maasim, Sarangani, one of the strongest to hit the Philippines. The earthquake was felt at intensities of I–VIII across Regions VIII, IX, X, XI, XII, BARMM, and CARAGA. A tsunami warning followed, with confirmed wave heights recorded at multiple coastal stations across Mindanao.

According to NDRRMC Situational Report No. 22 (as of July 1, 2026), the earthquake resulted in **88 deaths, 1,316 injuries, and 24 missing persons** across Mindanao. A total of 1,679,152 persons across 391,275 families were affected. Across the region, 113,279 houses were damaged, 18,360 of them totally destroyed, along with 1,539 infrastructure items costing an estimated ₱1.47 billion in damage. General Santos City was among the worst affected areas, sustaining widespread structural damage including collapsed buildings, a damaged university, and disruption to the city's airport and seaport.

What makes this event uniquely significant from a data perspective is that **PHIVOLCS had already done the risk assessment work.** In May 2025, just one year before the earthquake, DOST-PHIVOLCS officially turned over city-scale liquefaction and tsunami hazard maps specifically for General Santos City to the local government. These maps were developed using advanced geophysical, geotechnical, and AI-driven methodologies under the ACER-DeLTA Project.

This raises a question worth answering with data:

> **Did the damage from the June 8, 2026 M7.8 earthquake actually occur where PHIVOLCS predicted it would?**

Specifically: do the barangays in General Santos City identified as high liquefaction and seismic risk zones match the barangays that reported the most damage after the earthquake?

---

## Why This Matters

If the hazard maps accurately predicted where damage occurred, that validates them as reliable planning tools for rebuilding and future-proofing the city. If they did not match, that is equally important, it tells engineers, urban planners, and LGUs where the maps need to be updated before the next earthquake.

The Cotabato Trench has produced multiple destructive earthquakes historically, including the 1976 Moro Gulf earthquake that killed roughly 8,000 people. The same PHIVOLCS DeLTA mapping project is being rolled out to other vulnerable cities nationwide. A data-driven validation of these maps for General Santos City could serve as a replicable framework for other cities across the Philippines.

---

## Data Sources

| Data | Source | Format |
|------|--------|--------|
| Historical earthquake catalog (2016–2026) | PHIVOLCS Earthquake Bulletins / USGS API | CSV / API |
| Liquefaction and seismic hazard maps (GenSan) | PHIVOLCS GIS Web Portal | KMZ / Shapefile |
| Post-earthquake damage reports by barangay | NDRRMC Situational Reports (No. 1–22) | PDF |
| Satellite damage and landslide imagery | Philippine Space Agency (PhilSA) | GIS imagery |
| Barangay boundary reference | PSA Philippine Standard Geographic Code (PSGC) | Shapefile / CSV |

**Primary sources:**
- PHIVOLCS Earthquake Bulletins: https://earthquake.phivolcs.dost.gov.ph/
- PHIVOLCS GIS Hazard Maps: https://gisweb.phivolcs.dost.gov.ph/gisweb/earthquake-volcano-related-hazard-gis-information
- NDRRMC Situational Reports: https://ndrrmc.gov.ph/
- USGS Earthquake API: https://earthquake.usgs.gov/fdsnws/event/1/
- PSA PSGC: https://psa.gov.ph/classification/psgc/

---

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

## Live Dashboard

*To be deployed in Phase 6.*

`https://adrianejone.github.io/dep-data-engineering-open-track-adriane/`

---

## References

- NDRRMC. (2026, July 1). *Situational Report No. 22 — Effects of the Magnitude 7.8 Earthquake in Maasim, Sarangani.* National Disaster Risk Reduction and Management Council.
- DOST-PHIVOLCS. (2026, June 8). *Primer on the 08 June 2026 Magnitude (Mw) 7.8 Offshore Sarangani Earthquake.* https://www.phivolcs.dost.gov.ph/primer-on-the-08-june-2026-magnitude-mw-7-8-offshore-sarangani-earthquake/
- DOST-PHIVOLCS. (2025, May 28). *Press Release: PHIVOLCS Turns Over Enhanced Liquefaction and Tsunami Hazard Maps to General Santos LGU.* https://www.phivolcs.dost.gov.ph/press-release-phivolcs-turns-over-enhanced-liquefaction-and-tsunami-hazard-maps-to-general-santos-lgu/

---

## Acknowledgements

- DOST-PHIVOLCS for publicly available seismic and hazard data
- NDRRMC for situational reports
- Philippine Space Agency (PhilSA) for satellite damage imagery
- Data Engineering Pilipinas Open Track organizing team and volunteers