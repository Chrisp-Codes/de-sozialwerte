# Contributing

## Neuen Jahreswert einreichen

1. Fork des Repos erstellen
2. Neue Datei `data/JAHR.json` anlegen — als Vorlage das letzte Jahr kopieren
3. Alle Werte aktualisieren
4. **Pflicht**: Im `meta.sources`-Objekt für jedes geänderte Feld die offizielle Quelle angeben (Verordnung + BGBl-Fundstelle oder BMF-Schreiben)
5. `latest.json` auf das neue Jahr aktualisieren (einfach Kopie der neuen Jahres-Datei)
6. Pull Request öffnen

## Fehler korrigieren

Bitte Quelle der korrekten Werte im PR angeben. Ohne Quellenangabe kein Merge.

## Neue Felder hinzufügen

Bitte erst ein Issue eröffnen und kurz beschreiben, welchen Wert du ergänzen möchtest und warum. So können wir die Struktur abgestimmt halten.

## Versionsschema (SemVer)

| Version | Wann |
|---------|------|
| **Patch** `v2026.1` | Korrektur eines bereits veröffentlichten Jahreswerts |
| **Minor** `v2026.x` | Neues Feld hinzugefügt, rückwärtskompatibel |
| **Major** `v2027.0` | Bestehender Key umbenannt oder entfernt — bricht Consumer |

Feldnamen gelten als stabile API-Oberfläche. Änderungen an bestehenden Keys erfolgen ausschließlich mit einem Major-Version-Bump.

## Schema-Änderungen

Änderungen am `schema/values.schema.json` müssen rückwärtskompatibel sein oder alle bestehenden Datendateien werden gleichzeitig migriert.

## Qualitätssicherung

Der GitHub Actions Workflow validiert alle `data/*.json` Dateien automatisch gegen das JSON Schema bei jedem PR. Ein PR kann erst gemergt werden, wenn die Validierung grün ist.
