# Open Infrastructure Map

Web map of the world's power, telecoms, oil/gas, and water infrastructure, built from OpenStreetMap data. Almost all work happens in `web/` (TypeScript, Vite, MapLibre). In dev it loads tiles and data from openinframap.org, so no local backend is needed.

## Layout

- `web/src/style/style_oim_*.ts`: map layers, one file per layer group. `web/src/key/key.ts`: the legend.
- `imposm/` → `schema/` → `tegola/`: data import, database, and tile server. Layer names must match all the way through to `source-layer` in the web styles. See `docs/architecture.md`.
- `web-backend/`: Python stats pages. Needs the production database, so it can't run locally.

## Verify changes (from `web/`)

- `npm run lint`
- `npm test`: IMPORTANT: start `npm start` in the background and wait for http://localhost:5173 first. The tests load the running site in Puppeteer and fail without it.
- `npx tsc` already fails on main, and CI doesn't run it. Don't fix those errors unless asked.

## Rules

- User-visible text goes through i18next `t()`. Add new keys only to `web/locales/en/translation.json`; Weblate generates the other languages.
- Don't change `imposm/` mapping files. A change needs a full database re-import, so the maintainer wants an issue, not a PR.
