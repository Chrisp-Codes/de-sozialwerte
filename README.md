# de-sozialwerte
![Format](https://img.shields.io/badge/format-JSON-blue)
![Release](https://img.shields.io/github/v/release/Chrisp-Codes/de-sozialwerte)
![Validation](https://img.shields.io/github/actions/workflow/status/Chrisp-Codes/de-sozialwerte/validate.yml?label=validation)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
[![English](https://img.shields.io/badge/README-English-informational?style=flat-square)](README_en.md)

## Ziel

Es gibt keine offizielle maschinenlesbare Datenquelle für deutsche Sozial- und Steuerkennzahlen.  
Jedes HR-Tool, jede Lohnbuchhaltungssoftware und jedes Unternehmen pflegt diese Werte manuell — jedes Jahr aufs Neue.  
Dieses Repo stellt sie einmalig strukturiert bereit: versioniert, quellenbelegt und per einfachem HTTP-Request abrufbar.

## Enthaltene Werte

- **Sachbezugswerte** — Frühstück, Mittagessen, Abendessen, Vollverpflegung (täglich + monatlich)
- **Verpflegungspauschalen Inland** — voller Tag, halber Tag
- **Mindestlohn** — Brutto-Stundenlohn
- **Minijobgrenze** — Verdienstgrenze monatlich + jährlich

## Aufbau

```
data/
├── 2024.json
├── 2025.json
├── 2026.json
└── latest.json   → immer das laufende Jahr
schema/
└── values.schema.json
```

Jede Datei enthält alle Werte für ein Kalenderjahr sowie Quellenangaben je Datenfeld im `meta.sources`-Objekt.

## Nutzung

**Aktuelle Werte (immer aktuelles Jahr):**

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

**Auf eine bestimmte Version pinnen (empfohlen für Produktivsysteme):**

```javascript
// Unveränderlich — dieser Wert ändert sich nie mehr
const res = await fetch(
  'https://cdn.jsdelivr.net/gh/Chrisp-Codes/de-sozialwerte@v2026.0/data/2026.json'
);
```

Kein Auth, kein SDK, kein Account — ein einziger GET-Request.

## Stabilität

Feldnamen gelten als stabile API-Oberfläche. Änderungen an bestehenden Keys erfolgen ausschließlich mit einem Major-Version-Bump. Neue Felder können in Minor-Versionen hinzukommen, ohne dass bestehende Consumer betroffen sind.

Versionsschema: siehe [CONTRIBUTING.md](CONTRIBUTING.md).

## Quellen

- **Sachbezugswerte**: Sozialversicherungsentgeltverordnung (SvEV), jährlich im Bundesgesetzblatt
- **Verpflegungspauschalen**: BMF-Schreiben, jährlich im November
- **Mindestlohn**: Mindestlohngesetz (MiLoG) §1
- **Minijobgrenze**: § 8 Abs. 1 Nr. 1 SGB IV, dynamisch an den Mindestlohn gekoppelt seit Oktober 2022

## Mitmachen

Neue Jahreswerte oder Korrekturen sind willkommen — bitte [CONTRIBUTING.md](CONTRIBUTING.md) lesen.  
Pflicht: Jeder PR muss eine Quellenangabe im `meta.sources`-Objekt enthalten. Ohne Quelle kein Merge.

## Geplant

- Erweiterung um Beitragsbemessungsgrenzen (KV, RV, AV)
- Erweiterung um Verpflegungspauschalen Ausland
- Optional: Thin API-Wrapper auf Basis der JSON-Daten

## Haftungsausschluss

Die Werte in diesem Repo werden sorgfältig gepflegt und mit Quellenangaben belegt. Es wird jedoch keine Gewähr für Richtigkeit, Vollständigkeit oder Aktualität übernommen. Dieses Repo stellt keine Rechts- oder Steuerberatung dar. Im Zweifel sind stets die offiziellen Quellen (Bundesgesetzblatt, BMF) maßgeblich. Nutzung auf eigenes Risiko.

## Lizenz

MIT License – freie Nutzung, Veränderung und Weitergabe erlaubt.
