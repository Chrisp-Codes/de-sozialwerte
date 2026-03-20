# de-sozialwerte
![Format](https://img.shields.io/badge/format-JSON-blue)
![Status](https://img.shields.io/badge/status-live-green)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
[![Deutsch](https://img.shields.io/badge/README-Deutsch-informational?style=flat-square)](README.md)

## Purpose

There is no official machine-readable data source for German social security and tax reference values.  
Every HR tool, every payroll software and every company maintains these values manually — every single year.  
This repo provides them in a structured, versioned, source-cited format, accessible via a single HTTP request.

## Included Values

- **Sachbezugswerte** (non-cash benefits) — breakfast, lunch, dinner, full board (daily + monthly)
- **Verpflegungspauschalen** (meal allowances, domestic) — full day, half day
- **Mindestlohn** (minimum wage) — gross hourly rate
- **Minijob threshold** — monthly + annual earnings limit

## Structure

```
data/
├── 2024.json
├── 2025.json
├── 2026.json
└── latest.json   → always points to the current year
schema/
└── values.schema.json
```

Each file contains all values for a calendar year, plus source references per field in the `meta.sources` object.

## Usage

**Current values (always the current year):**

```javascript
const res = await fetch(
  'https://Chrisp-Codes.github.io/de-sozialwerte/data/latest.json'
);
const data = await res.json();

data.sachbezugswerte.mittagessen.taeglich   // 4.57
data.minijob.verdienstgrenze_monat          // 603
data.mindestlohn.brutto_stunde              // 13.90
```

```python
import requests

data = requests.get(
    'https://Chrisp-Codes.github.io/de-sozialwerte/data/latest.json'
).json()

data['sachbezugswerte']['mittagessen']['taeglich']
data['minijob']['verdienstgrenze_monat']
```

**Pin to a specific version (recommended for production systems):**

```javascript
// Immutable — this value will never change
const res = await fetch(
  'https://cdn.jsdelivr.net/gh/Chrisp-Codes/de-sozialwerte@v2026.0/data/2026.json'
);
```

No auth, no SDK, no account — a single GET request.

## Stability

Field names are considered a stable API surface. Changes to existing keys will only happen with a major version bump. New fields may be added in minor versions without affecting existing consumers.

Versioning policy: see [CONTRIBUTING_en.md](CONTRIBUTING_en.md).

## Sources

- **Sachbezugswerte**: Sozialversicherungsentgeltverordnung (SvEV), published annually in the Bundesgesetzblatt
- **Verpflegungspauschalen**: BMF-Schreiben (Federal Ministry of Finance circular), issued annually in November
- **Mindestlohn**: Mindestlohngesetz (MiLoG) §1
- **Minijob threshold**: § 8 Abs. 1 Nr. 1 SGB IV, dynamically linked to the minimum wage since October 2022

## Contributing

New annual values or corrections are welcome — please read [CONTRIBUTING_en.md](CONTRIBUTING_en.md).  
Required: every PR must include a source reference in the `meta.sources` object. No source, no merge.

## Planned

- Add Beitragsbemessungsgrenzen (contribution assessment ceilings for health, pension, unemployment insurance)
- Add international meal allowances (Verpflegungspauschalen Ausland)
- Optional: thin API wrapper on top of the JSON data

## Disclaimer

The values in this repo are maintained carefully and backed by source references. However, no warranty is given for accuracy, completeness or timeliness. This repo does not constitute legal or tax advice. When in doubt, always refer to the official sources (Bundesgesetzblatt, BMF). Use at your own risk.

## License

MIT License — free to use, modify and distribute, including commercially.
