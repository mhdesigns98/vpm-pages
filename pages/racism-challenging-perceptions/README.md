# Racism: Challenging Perceptions

The *Racism: Challenging Perceptions* series page — intro, five season groups, 14 PBS viral
players, the Issuu audience toolkit, and the Airtable feedback form.

**Source page:** https://vpmnews.kinsta.cloud/racism-challenging-perceptions/ (page id `411300`,
`section-builder` template)

This build consolidates the **19 separate ACF Rich Text sections** that make up the live page into
one Code Block. Nothing was cut — see the provenance table below.

## Files

| File | Purpose |
|---|---|
| `preview.html` | Full browser preview. **Generated** — do not edit by hand |
| `html.html` | Paste into the Code Block's HTML field |
| `css.css` | Paste into the Code Block's CSS field |
| `.build-preview.py` | Regenerates `preview.html` from the two above |

No JS field — the page has no behavior.

```bash
cd pages/racism-challenging-perceptions && ./.build-preview.py
```

All classes namespaced `vpm-rcp-`, BEM within it, everything scoped under a single `.vpm-rcp` root.

## Paste order

One block, replacing all 19 Rich Text sections:

1. Delete the 19 `page-rich-text` sections (leave the Page Hero — it supplies the `<h1>`)
2. Add a **Code Block** section in their place
3. `html.html` → HTML field, `css.css` → CSS field
4. Leave width/alignment at the section default; `.vpm-rcp` sets its own `max-width: 1100px`,
   matching the `width-wide` the Rich Text sections used

## Provenance

| Source section | Where it went |
|---|---|
| 1 (Page Hero) | **Left in place.** Not part of the paste |
| 2 | `.vpm-rcp-intro` |
| 3 | `.vpm-rcp-season--featured` (Season 5 card, 2 players, Issuu toolkit) |
| 4–6 | Season 4 group |
| 7–9 | Season 3 group |
| 10–14 | Season 2 group |
| 15–19 | Season 1 group |
| 20 | `.vpm-rcp-feedback` |

## What changed, and why

Faithful in content and order. Four classes of fix:

- **Un-namespaced globals removed.** Section 3 carried a `<style>` block — nested inside a `<p>` —
  declaring bare `.video-container`, `.video-column` and `.pbs-viral-player-wrapper`. Those leaked
  to every other block on the page. They are now `.vpm-rcp-videos`, `.vpm-rcp-video`,
  `.vpm-rcp-player`.
- **Type scale corrected.** The source's inline `1.6rem`–`3rem` sizes were authored against a 10px
  root and render ~60% oversized on `wpp-base`, whose root is 16px — body copy was computing to
  **25.6px**, season headings to 36.8px (verified in-browser against the live page). The rebuild
  uses the theme's own rich-text scale: 17px body, 34px season headings, 22–26px sub-headings.
- **Markup repaired.** Stray `</p>` closers after `</div>`, an unclosed `<img>`, `width="600px"`
  (invalid — the attribute is unitless), and the `<br style="clear:both">` float hack, which is now
  `display: flow-root`.
- **Performance and a11y.** All 16 iframes get `loading="lazy"` and a `title`. Season headings are
  real `<h2>`s instead of bold paragraphs, so the page has a document outline. Seasons 1–4 now use
  the same two-column grid Season 5 had, rather than one block per video.

The `2.3rem` "Season 5" and `3rem` "Season N" headings are uppercase Oswald here, matching the
theme's own section-header treatment.

## ⚠️ Two things to resolve before this goes live

1. **The Season 3 discussion-guide PDFs 404.** Both links on the current live page are dead:
   - `/wp-content/uploads/optimized/794d9883-rcp301-discussion-questionsupdate.pdf`
   - `/wp-content/uploads/optimized/465652b5-rcp3-discussion-questionsupdate8-10.pdf`

   They return 404 on staging and 403 on vpm.org (which is still Brightspot, different media path).
   The links are carried over as-is so nothing is silently dropped — either re-upload the PDFs or
   remove the two `.vpm-rcp-video__links` paragraphs before publishing.

2. **Media paths are root-relative** (`/wp-content/uploads/…`) in `html.html`, so they resolve on
   whichever host serves the page. `preview.html` rewrites them to staging-absolute so the preview
   works from `file://` or a local server. If production media ends up on a different host, it's one
   find/replace.

## Verified

`/ship-page` run 2026-08-07 — clean pass. Checked at 1280 / 768 / 375 / 320px via chrome-devtools
MCP (320px under real device emulation, not a narrowed window):

- **Scoping** — all six live `wpp-base` stylesheets loaded on top of the block change *nothing*
  inside `.vpm-rcp`: type, color, font, float, decoration, widths, heights, grid and total block
  height all byte-identical before and after. Zero selectors match outside `.vpm-rcp`, audited over
  `document.styleSheets`.
- No horizontal overflow at any width; grid collapses to one column below 900px, floats stack
  below 640px; no clipped text at 320px
- All 16 iframes load — both Season 5 PBS players, the Issuu toolkit (paginates, 20 pages), the
  Airtable form. All lazy, all titled
- Contrast: lowest ratio is 6.01:1 (`.vpm-rcp-meta`); links 8.06–8.5:1, headings 11.36:1
- One `<h1>` (theme hero), no heading-level skips, both images have real `alt` and intrinsic
  `width`/`height`
- Visible 3px focus outline on every link; `prefers-reduced-motion` block present
- No console errors. (The lone 404 in local testing is `/favicon.ico` from `python3 -m http.server`;
  the `videojs.mergeOptions` and `AdsLoader` warnings originate inside the PBS player iframes)

### Checklist items that don't apply

- **Jump-link anchors / `scroll-margin-top`** — the page has no in-page links and supplies no
  anchors for a widget below it.
- **Consumed widgets** — none; no `Uses widget:` lines.
- **Sticky Stream Player** — `.persistent-player` is `position: relative` on `wpp-base`; verified on
  the live page that it scrolls away with the header and that the only fixed element is the closed
  mobile menu overlay. There is no pinned bottom player on this theme to collide with.

### Notes

- Tab order runs column-major through the 2-up grid (left article complete, then right). That reads
  as three "backward jumps" to a naive top-coordinate check but is correct reading order.
- The two inline links in the Season 5 sentence ("PBS App", "YouTube") are 19px tall, under the 44px
  target size. They fall under WCAG 2.5.8's explicit exemption for links inside a block of text. The
  seven *standalone* links each get a 44px target via `min-height`.
- Font stacks match the theme's `--font-primary` / `--font-condensed` rather than `tokens.css`'s
  `--font-sans` / `--font-display`, which carry GT America in the fallback chain. Deliberate: this
  block should render in the same faces as the surrounding page. All nine color values trace to
  `tokens.css`.
