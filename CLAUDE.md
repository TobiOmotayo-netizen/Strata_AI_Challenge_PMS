# CLAUDE.md

Guidance for Claude when working in this repository. The owner is a PM, not a developer — explain changes in plain, non-technical language.

## What's here

- `public/index.html` — the entire UI in one file: a `<style>` block (shared styles), six stacked cards (org selector, parent goal, KPI scorecard, approval workflow + signatures, notification router, audit log), and a `<script>` block with the hard-coded org chart and page logic. It currently makes **no API calls**; everything runs in the browser.
- `public/rules_config.json` — policy source of truth (roles, KPI weight rules, rating bands, approval stages, sign-offs, notification routing, org hierarchy). Git-ignored; `public/rules_config.json.example` is the committed sample. Currently read only by `seed.js`, not by the UI.
- Backend: `server.js` (Express: serves `public/`, `GET /api/v1/health`), `api/index.js` + `vercel.json` (Vercel entry), `routes/`, `config/`, `seed.js`, `schema.sql` (PostgreSQL tables).

## Standing rules

1. **UI work happens in `public/` only** (mainly `public/index.html`).
2. **Never hand-edit `public/rules_config.json`** (or `rules_config.json.example`). If a policy value looks wrong, tell the user instead of changing it.
3. **Don't change backend files** — `server.js`, `routes/`, `api/`, `schema.sql` (and likewise `seed.js`, `config/`, `vercel.json`) — unless the user explicitly asks.
4. **Reuse existing styles.** Use the classes already defined in the `<style>` block of `index.html` (`.container`, `.card`, `table`, `button`, `.badge` + `.bg-green`/`.bg-yellow`/`.bg-red`, `.stepper`/`.step`, `.signature-grid`/`.sig-box`, `.alert-box`, `.audit-log`) and the existing color palette. Don't add CSS frameworks, libraries, or one-off styles when an existing class fits.

## Notes

- `index.html` duplicates some rules from `rules_config.json` (rating bands, notification routing, org chart). If you notice the two disagree, point it out to the user rather than silently "fixing" either side.
