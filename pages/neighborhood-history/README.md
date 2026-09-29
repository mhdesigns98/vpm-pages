# Neighborhood History

**Live URL:** https://www.vpm.org/neighborhood-history (currently an unpublished draft at `?page_id=490005`)
**Shape:** `acf-split` — native Page Hero + one Code Block (HTML + CSS + JS fields)
**Namespace:** `vpm-nh-`

## Purpose

Tells the story of the site of VPM's headquarters at 15 E. Broad St. — Cohen Co. (1886), Charles
Stores (1936), the 1948 façade, the 1987 fire, the parking-lot years, and VPM's 2026 move — as a
captioned timeline, then shows where it sits on a full-bleed map and closes with the Weekly Update
signup. To be linked from vpm.org/about and forward.vpm.org/we-moved once it's live — don't add
those links until the paste steps below are done. See `BRIEF.md`.

## Files

| File | Purpose |
|---|---|
| `html.html` | ACF HTML field — timeline, map band, closing band |
| `css.css` | ACF CSS field — the whole stylesheet, scoped to `.vpm-nh` |
| `js.js` | ACF JS field — newsletter iframe resize listener |
| `preview.html` | Browser preview — loads the three files into a Code Block wrapper under the live `wpp-base` CSS; flags missing CSS and broken images |
| `BRIEF.md` | Requirements, done criteria, open questions |
| `DEV-REQUEST.md` | Unsent draft of layout questions for the `wpp-base` theme developers |

## ⛔ Do not paste until

Every item is a `TODO` comment in `html.html` — comments don't render, so a straight paste ships
the placeholder instead:

- [ ] 2026 timeline entry has its current-day building photo (it renders a "Photo to come" box)
- [ ] 2026 photo has a credit line and alt text
- [ ] Closing copy is refreshed — the current text ("This summer…", "coming weeks and months") is dated
- [ ] Chevron swapped for marketing's own file (the SVG in `html.html` is an approximation)
- [ ] `grep -n TODO html.html` returns nothing
- [ ] `/ship-page neighborhood-history` passes

## Paste steps

Order matters: verify on a draft before touching the old sections, and keep a copy of what you delete.

1. **Preview.** From the repo root, `python3 -m http.server`, open
   `/pages/neighborhood-history/preview.html` with network access and wait for the status bar at
   the bottom: green means the theme CSS loaded and every image resolved (each `src`, every `srcset`
   candidate, and each full-size link target); red lists what failed.
2. **Back up the old sections.** Before deleting anything, copy out of the editor: the gray `page-grid`
   row (rich-text PNG + copy, and the newsletter Code Block including its **JS field**), the
   `page-gallery` (with its captions), and the map image block. Save them outside the repo.
3. **Add one Code Block** directly below the native Page Hero: `html.html` → HTML field,
   `css.css` → CSS field, `js.js` → JS field.
4. **Preview the draft.** The page is an unpublished draft and nothing links to it yet, so WordPress
   preview is the staging step here. Clear the Kinsta
   cache if what you see looks stale. Check:
   - the navy map band reaches both window edges (if it stops at the container, a theme ancestor
     has `overflow: hidden` — see `DEV-REQUEST.md` #7)
   - clicking a timeline image opens the full-size file, and the Stream Player / `pjax.js` and the
     theme lightbox don't hijack the click
   - the newsletter iframe resizes to its content (no inner scrollbar) — both on a full page load
     **and** after arriving from another vpm.org page (pjax navigation), since pjax may not run the
     Code Block's JS field
   - 320px wide: no horizontal page scroll
5. **Delete the old sections** only after step 4 passes.

## Uses widget

<!-- None. The iframe is the existing newsletter-signup embed, not a vpm-widgets widget.
     Timeline and lockup are page-local; promote to vpm-widgets if a second page wants them. -->
