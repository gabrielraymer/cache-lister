# Cache Lister

**Sort your bulk. Not your sanity.**
*by [GoblinCache TCG](https://goblincachetcg.com)*

---

## Use it now

**[cache-lister.goblincachetcg.com](https://cache-lister.goblincachetcg.com)**

No installs, no accounts. Open the link and go.

---

## What it does

Cache Lister takes two CSV files — your TCGPlayer catalog export and a simple card list you make yourself — and produces a clean, ready-to-import TCGPlayer upload CSV. It matches each card by collector number + set + condition + foil status, handles condition abbreviations (NM/LP/MP/HP/DMG), resolves set codes to full set names automatically (including Scryfall lookup for MTG), flags uncertain matches for your review before download, and merges duplicate entries. Everything runs entirely in your browser; your files never touch a server.

### Price Adjuster

A built-in pricing tool (third tab, or go directly to [cache-lister.goblincachetcg.com/#price-adjuster](https://cache-lister.goblincachetcg.com/#price-adjuster)) that lets you reprice your matched inventory before export. After running a match, your results auto-populate the Price Adjuster. You can also paste any TCGPlayer catalog CSV directly into the tab without running a match first. Controls include a market adjustment slider (50%–150%), a floor price (default $0.25), an optional ceiling price, and psychological rounding options (none / $0.25 / $0.49 / $0.99). A live preview table shows every card's market price, new price, and dollar change. When you're happy with the numbers, export a TCGPlayer-compatible CSV — cards with TCGplayer IDs are exported as price-update rows (quantity 0); paste-only imports produce a clean summary CSV.

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
| `Set` | Set name or code. Fuzzy-matched — short codes like `ECC` or `[CMD]` are resolved against Scryfall set data and your catalog automatically. |
| `Condition` | `NM`, `LP`, `MP`, `HP`, `DMG`, `DM`, `SP`, `EX`, `VG` or full words. TCGPlayer combined values like `Near Mint Foil` also accepted. |
| `Quantity` | Number of copies. |

Optional columns:

| Column | Notes |
|--------|-------|
| `Foil` | `yes`, `foil`, `true`, `1` = Foil. Absent or empty = Normal. Foil is also detected automatically from `Near Mint Foil`-style condition values. |
| `Price` | Your listing price. Falls back to TCGPlayer market price if omitted. |

A sample file is included in this repo: [`SAMPLE_SELLER_LIST.csv`](SAMPLE_SELLER_LIST.csv)

---

## How matching works

Cache Lister uses a four-priority matching strategy, from most to least confident:

1. **Collector number + set + condition + foil** — exact match on all four. No review needed.
2. **Collector number + name + condition + foil** — number and name agree. No review needed.
3. **Name + set + condition + foil** — no collector number; card flagged for **review**.
4. **Name + condition + foil, set-agnostic** — short set code (2–6 chars) with a single possible match in the catalog; flagged for **review**.

Cards requiring review appear in a **Review Queue** before download. You can approve each match, skip it (sends to unmatched), or approve all at once. Unmatched cards are shown with per-field diagnostics (set code, card name, condition — green = found, red = not found) and can be downloaded as a separate CSV.

Set codes in your seller list are resolved automatically:
1. Scryfall lookup (e.g. `cmd` → `Commander 2011`)
2. Catalog initialism matching (e.g. `ECC` → first catalog set whose initials match)
3. Passes through unchanged if unresolvable

The **Set Mapping Diagnostics** section (collapsible, shown after running) shows exactly how each of your set codes resolved and whether it was found in your catalog.

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
