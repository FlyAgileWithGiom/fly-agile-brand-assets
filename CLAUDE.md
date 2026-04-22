# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Nature

This is a **brand assets repository**, not a code project. It contains design source files, a brand guide (PDF + rendered pages), and the written design system. There is no build, lint, test suite, or package manager. Standard dev workflow rules (CI, testing, deployment) do not apply here — commits are documentation/asset updates.

## Source of Truth

`design-system.md` is the **canonical brand reference**. Any brand question (colours, typography, tone, logo usage, art direction anti-patterns) must be answered from that file, not inferred from assets. When editing it, treat it as a spec — changes propagate to how the brand is applied everywhere else.

Live example of the brand in use: https://giom.blog

## Logo Taxonomy

The `Logo/` folder is organised by brand/entity, then by layout variant, then by colour treatment. Pick the right variant by matching three axes:

- **Entity** — pick the top-level folder matching the audience:
  - `Fly Agile Logo/` — generic Fly Agile brand (square + horizontal)
  - `Fly Agile Pro Services/` — B2B/consulting services tagline
  - `Fly Agile with Giom/`, `Giom - Fly Agile/` — co-branded (Fly Agile + Giom the person)
  - `Giom - Agile Coach/` — Giom personal brand, coaching positioning
  - `Fly the Agile Life/` — lifestyle/content positioning
  - `From Raf/` — original designer source files (keep as archive, do not edit)
- **Layout** — square vs horizontal (inside `Fly Agile Logo/`)
- **Colour treatment** — default / `Monochrome/` / `dark Background/` (or `dark bg/`, `Dark background/` — naming is inconsistent across folders) / `bnw/` / `black_tagline/` / `Clear font/`

**Format convention** :

- `.ai` — editable source, **internally a PDF 1.5** (Illustrator's PDF-compatibility default). Readable by any PDF tool without Illustrator.
- `.svg` / `.png` — web-consumable exports. SVG preferred when present. Rapatriated from Google Drive in 2026-04.
- `.eps` / `.psd` — **removed in 2026-04**. They duplicated `.ai` content and were never hand-edited. Regenerable on demand (see recipes below).

When adding a new variant: start from the `.ai`, produce the `.svg`/`.png` exports.

## Non-obvious Brand Rules

These come from `design-system.md` but are easy to miss and are the most common violation points when generating new assets or content:

- **Fresh Green (`#4B9408`) is an accent, never dominant.** "Flashy but gets away with it because it's never over-present." If a mockup has more than a small punctuation of green, it's wrong.
- **Dark Green (`#222D27`), not black, is the primary anchor.** Using pure black as a background reads as generic/corporate and breaks the brand.
- **Paper plane logo must have its line pointing to the tip.** It's a hand-folded-paper gesture, not a geometric arrow — orientation matters.
- **Art direction is photo + collage + handmade, NOT flat illustration or geometric vectors.** Stock photography, clean geometric shapes, and cold palettes are explicit anti-patterns.
- **Typography is Montserrat only** (Bold / Medium / Regular by role). No secondary typeface.

## Working with `.ai` Source Files

Illustrator files can't be diffed and should not be hand-edited without Illustrator. But they **can be read**: an `.ai` is a PDF 1.5 under the hood, so any PDF tool works. The Brand Guide is already committed in both forms (`Brand Guide/Giom brand guide.ai` and `Brand Guide/Giom brand guide.pdf` — byte-identical) plus rendered page PNGs in `Brand Guide/pages/`.

## Conversion recipes

`pdftocairo` (via Homebrew's `poppler`) handles `.ai` directly — no Illustrator needed:

```bash
# .ai → SVG (logos, 1-page files)
pdftocairo -svg "Logo/.../file.ai" out.svg

# .ai → high-res PNG
pdftocairo -png -r 300 "Logo/.../file.ai" out    # produces out-1.png

# Multi-page .ai (e.g. brand guide) → one PNG per page
pdftocairo -png -r 150 "Brand Guide/Giom brand guide.ai" "Brand Guide/pages/page"
```

For the removed legacy formats:

```bash
brew install ghostscript imagemagick
# .ai → .eps (legacy consumers)
gs -sDEVICE=eps2write -o out.eps in.ai
# .ai → .psd (flatten, loses layers)
magick in.ai out.psd
```

## Web consumption (Claude Design, browsers)

All files are accessible via raw GitHub URLs:

```
https://raw.githubusercontent.com/FlyAgileWithGiom/fly-agile-brand-assets/main/<path>
```

`.md` files and `.svg`/`.png` exports are directly consumable. The Brand Guide PDF and `pages/*.png` are the most useful for visual reference by AI tools.

## Commits

Follow the Fly Agile conventional commit format already in use (`feat:`, `fix:`, `refactor:`, `docs:`). For asset-only additions, `feat:` fits a new logo variant or brand extension; `docs:` fits edits to `design-system.md` or `README.md`.
