# Neighborhood History — Paste order

Page: `vpm.org/neighborhood-history` (currently `?page_id=490005`), Section Builder template.

| # | Block | File |
|---|---|---|
| 1 | **Page Hero (native theme block)** — keep as-is; image swap is an open question in `BRIEF.md` | — (editor) |
| 2 | Code Block — Timeline. **Carries the entire stylesheet.** | `01-timeline.html` |
| 3 | Code Block — Map band | `02-map.html` |
| 4 | Code Block — Closing band: lockup, copy, newsletter signup | `03-closing.html` |

## Remove from the current page

These sections are replaced by the blocks above — delete them once the new blocks are in:

- The `page-grid` row (gray band) holding the rich-text "Media that moves us forward" PNG + copy
  and the newsletter Code Block → replaced by block 4
- The `page-gallery` (four photos) → replaced by block 2
- The image block holding the map → replaced by block 3

## Rules that matter

- **All CSS lives in block 2 (`01-timeline.html`).** Blocks 3 and 4 carry no `<style>`. Removing or
  reordering block 2 strips styling from all three.
- **No global selectors.** Everything is scoped under `.vpm-nh`; tokens are declared there, not on
  `:root`.
- **Full-bleed bands** use `box-shadow` + `clip-path` on `.vpm-nh-band--inverse` / `--muted`, so they
  never cause horizontal scroll. Don't swap in `width: 100vw` or `margin-inline: calc(50% - 50vw)` —
  both size to the viewport including the scrollbar.
- The newsletter resize listener lives in block 4 and is guarded by `window._vpmNlResizeListener`.
  Delete the old newsletter Code Block's JS along with it.

## Verifying

1. Open `../preview.html` (it loads these three files in order under simulated theme chrome).
2. Check 1440 / 980 / 760 / 320px: no horizontal page scroll, bands reach both edges.
3. Exactly one `<h1>` (the native hero); fragments start at `<h2>`.
4. Paste on staging, clear the Kinsta cache, and check the seams between the theme's section padding
   and the navy/gray bands — the theme's own padding around each Code Block is not controlled here.
