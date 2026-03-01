# Contributing

## Submitting a new year's values

1. Fork the repository
2. Create a new file `data/YEAR.json` — use the most recent year as a template
3. Update all values
4. **Required**: add the official source for each changed field in the `meta.sources` object (regulation name + Bundesgesetzblatt reference or BMF-Schreiben date)
5. Update `latest.json` to reflect the new year (simply copy the new year's file)
6. Open a pull request

## Fixing incorrect values

Please include the source for the correct values in your PR description. No source, no merge.

## Adding new fields

Please open an issue first and briefly describe which value you'd like to add and why. This keeps the data structure consistent across contributors.

## Versioning policy (SemVer)

| Version | When |
|---------|------|
| **Patch** `v2026.1` | Correction of an already published value |
| **Minor** `v2026.x` | New field added, backwards compatible |
| **Major** `v2027.0` | Existing key renamed or removed — breaks consumers |

Field names are considered a stable API surface. Changes to existing keys will only happen with a major version bump.

## Schema changes

Changes to `schema/values.schema.json` must be backwards compatible, or all existing data files must be migrated in the same PR.

## Quality assurance

The GitHub Actions workflow automatically validates all `data/*.json` files against the JSON Schema on every pull request. A PR can only be merged once validation passes.
