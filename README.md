# Cache Lister

**Sort your bulk. Not your sanity.**
*by [GoblinCache TCG](https://goblincachetcg.com)*

---

## Use it now

**[cache-lister.goblincachetcg.com](https://cache-lister.goblincachetcg.com)**

No installs, no accounts. Open the link and go.

---

## What it does

Cache Lister takes two CSV files — your TCGPlayer catalog export and a simple card list you make yourself — and produces a clean, ready-to-import TCGPlayer upload CSV. It matches each card by collector number + set + condition + foil status, handles condition abbreviations (NM/LP/MP/HP/DMG), fuzzy set name matching, and merges duplicate entries. Everything runs entirely in your browser; your files never touch a server.

---

## The two input files

### File 1 — TCGPlayer Catalog CSV

Export this from TCGPlayer's **Pricing** tab using **"Export Filtered CSV"** or **"Export from Live"**. This is the full catalog of everything you have listed or could list — Cache Lister reads from it to pull TCGplayer IDs, set names, and market prices.

Required columns (TCGPlayer provides these automatically):
- `TCGplayer Id` — unique SKU per card + condition + foil variant
- `Product Name`, `Set Name`, `Number`, `Condition`, `Add to Quantity`

Optional columns (used when present, safely ignored when absent):
- `Printing` — defaults to `Normal` if missing
- `Market Price` — used as fallback listing price if your card list omits `Price`

### File 2 — Your Card List CSV

A simple spreadsheet you create. Minimum required columns:

| Column | Notes |
|--------|-------|
| `Name` | Card name. Case-insensitive, trimmed. |
| `Number` | Collector number. Most reliable match key. |
| `Set` | Set name. Fuzzy-matched against TCGPlayer's set names — "Foundations" matches "Magic: The Gathering Foundations". |
| `Condition` | Accepts `NM`, `LP`, `MP`, `HP`, `DMG` or full words. |
| `Quantity` | Number of copies. |

Optional columns:

| Column | Notes |
|--------|-------|
| `Foil` | `yes`, `foil`, `true`, `1` = Foil. Absent or empty = Normal. |
| `Price` | Your listing price. Falls back to TCGPlayer market price if omitted. |

A sample file is included in this repo: [`SAMPLE_SELLER_LIST.csv`](SAMPLE_SELLER_LIST.csv)

---

## How to run locally

For sellers who want to work offline or developers who want to contribute:

```bash
git clone https://github.com/gabrielraymer/cache-lister
# then just open the file:
open cache-lister/index.html        # macOS
start cache-lister\index.html       # Windows
xdg-open cache-lister/index.html    # Linux
```

No `npm install`. No build step. It's one HTML file.

---

## How to contribute

1. Fork the repo
2. Make your changes to `index.html`
3. Open the file in a browser and test with a real TCGPlayer export + your own card list
4. Submit a PR with a brief description of what you changed and why

Bug reports and feature requests welcome via [GitHub Issues](https://github.com/gabrielraymer/cache-lister/issues).

---

## License

MIT License — Copyright GoblinCache TCG

See [LICENSE](LICENSE) for full text. Free to use, fork, and redistribute.

---

*Built by [GoblinCache TCG](https://goblincachetcg.com) — the TCG inventory and pricing platform for collectors and sellers.*
