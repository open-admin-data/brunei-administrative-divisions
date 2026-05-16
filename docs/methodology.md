# Methodology

## Data Sources

This dataset is compiled from multiple open sources:

- **Bruneiverse/bruneimap** (CC BY 4.0) — R package providing kampong names, IDs, and hierarchy derived from Nadi.BN (Brunei's official geospatial data catalogue)
- **geoBoundaries** (CC BY 4.0) — District and mukim polygon boundaries for centroid computation
- **Qoyyuum/Tulus** — Postal code mapping for kampongs
- **OpenStreetMap** (ODbL) — Village-level coordinates via Overpass API
- **OpenStreetMap Nominatim** — Geocoding for kampongs not found in OSM

## Processing

1. District boundaries from geoBoundaries ADM1 → centroid computation
2. Mukim boundaries from geoBoundaries ADM2 → centroid computation
3. Kampong list from bruneimap CSV → matched with OSM + Nominatim for coordinates
4. Postal codes joined from Tulus JSON on kampong name
5. Parent assignment via point-in-polygon spatial join
6. Multi-format export: JSON, NDJSON, CSV
7. Hierarchy folder structure with READMEs generated via EJS templates

## ID Scheme

- District: ISO 3166-2 codes (`BN-BE`, `BN-BM`, `BN-TU`, `BN-TE`)
- Mukim: `{district}-MK{nn}` (numbered within parent district)
- Kampong: `{mukim}-KP{nnn}` (numbered by bruneimap source ID)

## Accuracy

- All division names and hierarchy from official Nadi.BN data via bruneimap
- Coordinates: 100% at all levels (332 precise + 106 mukim-centroid fallback for kampongs)
- Postal codes: ~70% coverage at kampong level
- Build script is idempotent: same input always produces same output