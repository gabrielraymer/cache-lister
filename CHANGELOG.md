# Changelog

All notable changes to Cache Lister are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [Unreleased]

---

## [1.1.2] — 2026-05-18

### Fixed
- Drag and drop now works in Chrome on Windows — added `dragenter` prevention (Chrome requires this before it allows `drop` to fire) and window-level guards to stop Chrome from navigating to the file

---

## [1.1.1] — 2026-05-18

### Fixed
- CSP header removed from `netlify.toml` — was silently blocking file upload processing
- Market price column now reads `TCG Market Price` (actual TCGPlayer export column name) with fallback to `Market Price`

---

## [1.1.0] — 2026-05-17

### Added
- Favicon — GoblinCache TCG badge icon shown in browser tab
- Custom domain: `cache-lister.goblincachetcg.com`
- GitHub → Netlify continuous deployment (pushes to `main` auto-deploy)
- `netlify.toml` with security headers (CSP, X-Frame-Options, referrer policy)

### Fixed
- `Printing` and `Market Price` no longer required when uploading a TCGPlayer catalog export — both columns are optional and have safe defaults (`Normal` / empty). Fixes upload failure for catalog exports that omit these columns.

### Changed
- README: updated canonical URL, corrected required vs optional column list

---

## [1.0.0] — 2026-05-17

### Added
- Initial release
- Three-step progressive UI: upload TCGPlayer catalog → upload seller list → download import CSV
- Two-priority card matching: collector number + set + condition + printing, falling back to name + set + condition + printing
- Fuzzy set name matching (substring containment)
- Condition abbreviation mapping: NM / LP / MP / HP / DMG
- Foil normalization: `yes`, `foil`, `true`, `1` treated as Foil; absent/empty = Normal
- Deduplication by `TCGplayer Id` — quantities summed across matching rows
- Unmatched rows report (inline + downloadable CSV)
- Fully client-side — no server, no accounts, no data leaves the browser
- Papa Parse CDN for CSV parsing
- `SAMPLE_SELLER_LIST.csv` with MTG + Lorcana examples
