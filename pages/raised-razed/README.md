# Raised/Razed

**Live URL:** https://vpmnews.kinsta.cloud/raised-razed/
**Shape:** `acf-split` (Code Block — HTML + CSS fields)
**Namespace:** `vpm-rr-`

## Purpose

Documentary page for *Raised/Razed*, a feature film about the destruction of Vinegar Hill, an
African American neighborhood in Charlottesville, VA, under the federal Urban Renewal program.
Consolidates the 32 stacked `page-hero` / `page-rich-text` / `page-split` sections on the live
page into one namespaced Code Block, following the same pattern used for
`racism-challenging-perceptions`.

## Files

| File | Purpose |
|---|---|
| `html.html` | ACF HTML field — paste into the Code Block's HTML field |
| `css.css` | ACF CSS field — paste into the Code Block's CSS field |
| `preview.html` | Generated — full browser preview, simulates wpp-base chrome |
| `.build-preview.py` | Regenerates `preview.html` from `html.html` + `css.css` |

Paste order: `html.html` → HTML field, `css.css` → CSS field. No JS field needed.

## Provenance table

Every source section, where it landed, and what changed.

| # | Source section | Destination | Notes |
|---|---|---|---|
| 1 | `page-hero` (no image) | `.vpm-rr-hero` | Title only, straightforward carry-over |
| 2 | `page-rich-text` — bold centered lede | `.vpm-rr-intro__lede` | |
| 3 | `page-rich-text` — PBS viral player iframe | `.vpm-rr-player` | Added `loading="lazy"` + real `title` (source iframe had neither) |
| 4 | `page-rich-text` — intro paragraph | `.vpm-rr-intro` body copy | |
| 5 | `page-section-header` "Raised/Razed Articles" | `.vpm-rr-articles` heading | Square marker replicated as `.vpm-rr-section-title__marker` |
| 6 | `page-split` — appraisal-reports image, **no headline/text** | `.vpm-rr-press-card--image-only` | Kept image-only per decision below — see Known issues |
| 7–10 | `page-split` × 4 — image + `<h2>` headline | `.vpm-rr-press-card` × 4 | Theme-supplied `page-split-image`/`page-split-text` replaced with namespaced BEM; no source `<a>` existed on any of these, headline-only teasers carried as-is |
| 11 | `page-rich-text` "The Team" `<h2>` | `.vpm-rr-team` heading | Stripped Brightspot `data-state` JSON attribute (CMS internal metadata, not content) |
| 12–29 | `page-rich-text` × 18 — 6× (photo / name+role / bio) triplets + `<hr>` dividers | `.vpm-rr-member` × 6 | Collapsed each 3-section stack (photo, name/role, bio) plus its trailing `<hr>` into one `<article>`; dividers now `border-bottom` on all but the last member |
| 30 | `page-rich-text` — show logo image | `.vpm-rr-about__logo` | |
| 31 | `page-rich-text` "About" `<h2>` + 4 paragraphs | `.vpm-rr-about` body | Stripped Brightspot `data-state` JSON attribute |
| 32 | `page-rich-text` — social follow links | `.vpm-rr-follow` | |

## What changed and why

- **Un-namespaced globals removed.** Source relied on theme-supplied `.page-split-image` /
  `.page-split-text` / `.page-rich-text-inner` classes; a Code Block inherits none of that, so
  every rule is now scoped under `.vpm-rr`.
- **Type scale matches the theme's measured rich-text scale** — 16px root, 17px body (Public
  Sans), 30px section headings (Oswald 700). Measured live via computed styles on
  `vpmnews.kinsta.cloud` 2026-08-11 (not inferred from source markup, which used no inline
  `rem` overrides on this page — unlike `racism-challenging-perceptions`, there was no 10px-root
  inflation bug here).
- **Iframe a11y/perf:** the PBS viral player now gets `loading="lazy"` and a real `title`; source
  had neither.
- **Brightspot CMS metadata stripped** from two `<h2>` elements ("The Team", "About") that
  carried large inline `data-state` JSON blobs — internal publishing metadata, not content.
- **Press grid restructured** from single-column stacked `page-split` sections into a responsive
  CSS grid (`auto-fit`, min 240px) so all 5 items sit together instead of full-width rows.

## Known issues — blocking, need your input before shipping

1. **Randall R. Taylor Jr.'s headshot 404s on the live page right now.**
   Source `src="https://vpmnews.kinsta.cloud/wp-content/uploads/optimized/c13b8a4c-90.90"` —
   filename has lost its real extension (`.90` instead of `.jpg`/`.png`) and returns HTTP 404.
   **Per your decision, this build ships a placeholder** (`.vpm-rr-member__photo--placeholder`,
   shows "RT" initials) instead of a broken-image icon. **A real replacement photo is still
   needed** — swap the placeholder markup for a real `<img>` once one is supplied.

2. **One press card has no headline or link.** The 4th "Articles" item (appraisal-reports
   screenshot) has always been image-only on the live page — no `<h2>`, no `<a>`, nothing in its
   text panel. **Per your decision, this ships as-is** (`.vpm-rr-press-card--image-only`).

3. **None of the 5 press cards link anywhere.** All five are headline-over-image with no `<a>`
   wrapping either — this matches current live behavior exactly, but means the "Articles" section
   has no functional links. Worth confirming with editorial whether that's intentional (teaser-only
   design) or a missed migration step, independent of issue #2 above.

## Uses widget

None.
