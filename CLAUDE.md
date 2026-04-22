# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Nature

This is a **brand assets repository**, not a code project. It contains design source files (Adobe Illustrator, EPS, PSD), a brand guide, and the written design system. There is no build, lint, test suite, or package manager. Standard dev workflow rules (CI, testing, deployment) do not apply here — commits are documentation/asset updates.

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

**Format convention** — `.ai` is the editable source; `.eps` and `.psd` are derived exports. When adding a new variant, produce the `.ai` first, then regenerate the other formats from it. Never hand-edit an `.eps` or `.psd` independently.

## Non-obvious Brand Rules

These come from `design-system.md` but are easy to miss and are the most common violation points when generating new assets or content:

- **Fresh Green (`#4B9408`) is an accent, never dominant.** "Flashy but gets away with it because it's never over-present." If a mockup has more than a small punctuation of green, it's wrong.
- **Dark Green (`#222D27`), not black, is the primary anchor.** Using pure black as a background reads as generic/corporate and breaks the brand.
- **Paper plane logo must have its line pointing to the tip.** It's a hand-folded-paper gesture, not a geometric arrow — orientation matters.
- **Art direction is photo + collage + handmade, NOT flat illustration or geometric vectors.** Stock photography, clean geometric shapes, and cold palettes are explicit anti-patterns.
- **Typography is Montserrat only** (Bold / Medium / Regular by role). No secondary typeface.

## Working with `.ai` Source Files

Illustrator files are binary and can't be diffed. When asked to modify them, do not attempt to edit directly — describe the change and expect the user to handle it in Illustrator, or delegate to a tool that can rasterise/export. Track changes by committing the updated `.ai` plus regenerated `.eps`/`.psd` exports together.

## Commits

Follow the Fly Agile conventional commit format already in use (`feat:`, `fix:`, `refactor:`, `docs:`). For asset-only additions, `feat:` fits a new logo variant or brand extension; `docs:` fits edits to `design-system.md` or `README.md`.
