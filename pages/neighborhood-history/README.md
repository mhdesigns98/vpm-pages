# Neighborhood History

**Live URL:** https://www.vpm.org/neighborhood-history (currently `?page_id=490005`)
**Shape:** `sections` — native hero + three Code Blocks
**Namespace:** `vpm-nh-`

## Purpose

Tells the story of VPM's headquarters building at 13–17 E. Broad St. — Cohen Co. (1886), Charles
Stores (1936), the 1948 façade, the 1987 fire, and VPM's 2026 move — as a captioned timeline, then
shows where it sits on a full-bleed map and closes with the Weekly Update signup. Linked from
vpm.org/about. See `BRIEF.md`.

## Paste order

Read `sections/PASTE-ORDER.md` before pasting — it also lists the current sections to remove.

1. Native Page Hero (unchanged)
2. `sections/01-timeline.html` — carries the stylesheet
3. `sections/02-map.html`
4. `sections/03-closing.html`

## Files

| File | Purpose |
|---|---|
| `BRIEF.md` | Requirements, done criteria, open questions |
| `DEV-REQUEST.md` | Unsent draft of layout questions for the `wpp-base` theme developers |
| `sections/PASTE-ORDER.md` | Paste order, sections to remove, verification |
| `sections/01-timeline.html` | Stylesheet + timeline |
| `sections/02-map.html` | Map band with text description |
| `sections/03-closing.html` | Lockup, copy, newsletter iframe + resize listener |
| `preview.html` | Browser preview — loads the three fragments under simulated theme chrome |

## Uses widget

<!-- None. The timeline and "Media that moves us forward" lockup are built page-local for now;
     promote them to vpm-widgets if a second page wants them (see BRIEF.md). -->
