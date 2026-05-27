# Brunei Administrative Divisions / Brunei Darussalam

Open dataset of Brunei Darussalam's complete administrative hierarchy — from districts (daerah) through subdistricts (mukim) down to villages (kampong). This repository provides structured reference data for all three levels of Brunei's administrative divisions, including geographic coordinates and postal codes. Designed for developers, researchers, government agencies, and AI agents.

Licensed under CC-BY-4.0. Browse the hierarchy through GitHub's folder navigation, download aggregate files in JSON/CSV/NDJSON, or integrate directly via raw URLs.

## Overview

| Item | Details |
|------|---------|
| District | 4 |
| Subdistrict | 42 |
| Village | 438 |
| Coordinates | ✅ Included (all levels) |
| Postal Codes | ✅ Included (village level) |
| Formats | JSON, NDJSON, CSV |
| License | CC-BY-4.0 |
| Last Updated | 2026-05-27 |
| Website | [openadmindata.org/bn](https://openadmindata.org/bn/) |
| API | [openadmindata.org/api/bn](https://openadmindata.org/api/bn/) |

## Browse by District

| # | District | Subdistricts | Villages | Link |
|---|----|----|----|------|
| 1 | Belait | 8 | 83 | [Browse](divisions/belait-bn-be/) |
| 2 | Tutong | 9 | 84 | [Browse](divisions/tutong-bn-tu/) |
| 3 | Brunei-Muara | 19 | 197 | [Browse](divisions/brunei-muara-bn-bm/) |
| 4 | Temburong | 6 | 74 | [Browse](divisions/temburong-bn-te/) |

## Data Files

| File | Format | Description |
|------|--------|-------------|
| [all-district.json](data/all-district.json) | JSON | All 4 district records |
| [all-mukim.json](data/all-mukim.json) | JSON | All 42 subdistrict records |
| [all-kampong.json](data/all-kampong.json) | JSON | All 438 village records |
| [all-flat.json](data/all-flat.json) | JSON | Levels 1-2 flat array |
| [all-flat.ndjson](data/all-flat.ndjson) | NDJSON | Streaming format |
| [all-flat.csv](data/all-flat.csv) | CSV | Spreadsheet format |
| [hierarchy.json](data/hierarchy.json) | JSON | Nested tree |
| [schema.json](data/schema.json) | JSON Schema | Data schema |

## Quick Start

### Python

```python
import json

with open("data/all-district.json", "r", encoding="utf-8") as f:
    data = json.load(f)

for r in data:
    print(f"{r['name']['local']} ({r['name']['en']}) — {r['children_count']['mukim']} subdistricts")
```

### JavaScript

```javascript
import { readFileSync } from "fs";

const data = JSON.parse(readFileSync("data/all-district.json", "utf-8"));
console.log(`Total: ${data.length} districts`);
```

## Schema

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier |
| `level` | integer | 1=district, 2=subdistrict, 3=village |
| `level_name` | object | Level label (local + English) |
| `name.local` | string | Name in local script |
| `name.en` | string | English name |
| `name.slug` | string | URL-safe slug |
| `parent` | object/null | Parent division reference |
| `ancestors` | array | Full ancestor chain |
| `children_count` | object | Count of children per level |
| `zip_codes` | array | Postal codes (where available) |
| `geo.lat` | string | Latitude (WGS84) |
| `geo.lon` | string | Longitude (WGS84) |

Full schema: [data/schema.json](data/schema.json)

## Hierarchy Browse

```
divisions/{district-slug}/
divisions/{district-slug}/{mukim-slug}/
```

Villages are listed inline in each subdistrict's README.

## AI Integration

- [llms.txt](docs/llms.txt) — Quick reference for AI agents
- [llms-full.txt](docs/llms-full.txt) — Summary with per-district links
- [Per-district data](docs/llms-full/) — Full data by district

## Citation

```
Brunei Administrative Divisions Dataset (CC-BY-4.0)
URL: https://github.com/open-admin-data/brunei-administrative-divisions
```

See [CITATION.cff](CITATION.cff) for machine-readable citation.

## License

- **Data**: [CC-BY-4.0](LICENSE)

## Related

- [Open Admin Data](https://openadmindata.org) — Browse, search and explore administrative divisions for every country
- [open-admin-data](https://github.com/open-admin-data) — GitHub organization with all country repos
- [ListBase](https://www.listbase.org) — Structured reference data for every country
