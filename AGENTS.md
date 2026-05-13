# AGENTS.md — calculadorasofipos-files

Data-only repo for the "Calculadora de Sofipos" app. No code, no build, no tests, no CI.

## Active branch

Work and commit on **`dev`**. `main` is the production branch and should only receive merges from `dev`.

## Repo structure

- `config.json` — institution manifest with IDs, display names, image/tasa filenames. Update `actualizacion` timestamp on data changes.
- `files/` — institution logo images (`.png` / `.jpeg` / `.jpg` / `.webp`).
- `tasas/*.json` — per-institution rate data. Array of `{tipo, dias, tasa, tope}`. `tipo` is `"vista"` (demand) or `"plazo"` (term). Some files are empty arrays (`[]`).
- `tasas/resumen.csv` — flattened summary of all rates. Must be kept in sync with the JSON files.

## Adding or updating an institution

1. Add entry to `config.json` (sequential `id` prefix matching filename order).
2. Place logo image in `files/` with the filename from `config.json`.
3. Add/update tasa JSON in `tasas/`.
4. Update `resumen.csv` to reflect all rates.
5. Bump `actualizacion` in `config.json` to ISO 8601.
6. Commit on `dev`.

## Notes

- No `.gitignore` exists — watch for stray files.
- `resumen.csv` columns: `institucion,descripcion,tipo,dias,tasa,tope,tasaTope,restricciones,notas`
- Some JSON tasa files intentionally empty when an institution has no structured products yet.
