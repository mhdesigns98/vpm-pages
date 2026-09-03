# Pages Index

Lookup table for existing page builds — check here before picking a new slug or namespace prefix so
they don't collide. Kept out of `CLAUDE.md` so it isn't loaded into context on every session.

Reusable blocks live in the sibling repo: `~/Projects/vpm/vpm-widgets/INDEX.md`.

`/new-page` adds a row here when scaffolding.

| Folder | Shape | Description |
|---|---|---|
| `annual-report-2025/` | single-file | 2025 Annual Report interactive page |
| `basics-virginia/` | single-file | The Basics Virginia™ — five-section page composite (hero, 5 principles, in action, the movement, nature trail CTA) as one Brightspot HtmlModule drop-in; uses web components and px-not-rem sizing |
| `ecp-partners-team/` | single-file | Early Childhood Education partners & team (Brightspot embed) |
| `elections-2026-primary/` | split-file | 2026 Virginia Primary page — dates, video carousel, article links (WordPress ACF) |
| `how-federal-funding-works/` | single-file | Federal funding explainer section for the impact page |
| `impact-report-2025/` | split-file | 2025 Impact Report page as deployed — hero, sticky jump links, awards counters; consolidated page stylesheet + deferred behavior script (namespaces `vpm-impact25-`, `vpm-awards2025`). Two HTML fields, see its README for paste order |
| `mending-walls/` | split-file | Mending Walls documentary companion page (Mending Walls RVA public art project) — consolidated from 12 stacked WordPress sections into one Code Block (namespace `vpm-mw-`). Kinsta dev copy was missing a 5-image carousel present on the live `vpm.org` page; added from a live screenshot + supplied image URLs. Podcast kept as a simplified castbox iframe rather than the live page's native playlist widget; see README |
| `raised-razed/` | split-file | Raised/Razed documentary page (Vinegar Hill, Charlottesville) — consolidated from 32 stacked WordPress sections into one Code Block (namespace `vpm-rr-`). Built against the live `vpm.org` page after discovering the Kinsta staging port was missing content (a headshot, a 6th press card, all article links); see README |
| `rva-events-september-2026/` | single-file | Upcoming Events list block for a VPM subsite page — RVA First Fridays and Broad New Day (namespace `vpm-evts-`), no JS |
| `unwined-episode/` | split-file | Un-Wine'd page upper section — "Stream more" lockup, jump links, PBS viral player, episode write-up, sponsor row. **Uses widget:** `links-with-map` pasted directly below it |
| `voter-guide-2026/` | sections | 2026 Voter Guide — seven sections pasted separately into the WordPress editor; **read `sections/PASTE-ORDER.md` before pasting**. Reference implementation of the `sections/` shape. Carries `BRIEF.md`, `AUDIT.md`, and `DEV-REQUEST.md` |
