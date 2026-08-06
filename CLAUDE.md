# VPM Pages

## Purpose

Full page builds for vpm.org — one folder per page. This repo is the sibling of
[`vpm-widgets`](https://github.com/mhdesigns98/vpm-widgets) (`~/Projects/vpm/vpm-widgets/`),
which holds reusable blocks.

## ⚠️ This repo is PUBLIC

Everything committed here is world-readable and indexable. That's a deliberate choice — the page
markup ships to vpm.org anyway, so it isn't secret — but page folders accumulate *internal*
documentation in a way widget folders never did, and that's the thing to watch.

**Before committing, check what you're adding.** Reviewed and accepted as of 2026-08-06:

- `voter-guide-2026/DEV-REQUEST.md` — an unsent draft to the `wpp-base` theme vendor, including
  internal deadlines
- `voter-guide-2026/AUDIT.md` — QA findings, including one unfixed contrast failure
- The staging host `vpmnews.kinsta.cloud` and dev page id `466103`, in several files
- `voter-guide-2026/.vercel/project.json` — `orgId` / `projectId`

Those are known and judged acceptable. **Do not add worse.** Specifically, never commit:

- API keys, tokens, or credentials of any kind — including in a `reference/` example. Use
  `YOUR_KEY`-style placeholders, as `reference/wordpress-php-template/inc/voter-guide-data.php`
  already does for the AP elections API.
- Embargoed editorial content, unpublished results, or anything under a publication date
- Named individuals' contact details, or verbatim internal email threads
- Anything a `/brief` or `/ship-page` run produced that reads as criticism of a colleague or vendor

If a page genuinely needs sensitive material to be useful, keep that file outside the repo and
reference it by path from the page `README.md` — don't commit it and don't paraphrase it.

## Which repo does this belong in?

> **A widget is used on more than one page. A page build is used on exactly one.**
> If it only ever appears on one URL, it belongs in `vpm-pages` — even if it is block-shaped.

The test is **reuse, not size**. `elections-2026-primary` is a small ACF split-file block and lives
here anyway, because it only ever appears on the primary page. Its sibling
`elections-2026-primary-cta` stays in `vpm-widgets`, because it's a homepage CTA reused across
placements.

If you catch yourself about to build the same thing for a second page, stop — it's a widget. Move it
to `vpm-widgets` and let both pages consume a copy.

## Repo Structure

```
/pages
  /[page-slug]
    README.md      ← purpose, live URL, "Uses widget:" lines, paste order
    index.html     ← single-file: self-contained page, pasted whole into a Code Block
```

or, for pages built against WordPress ACF fields:

```
/pages
  /[page-slug]
    README.md
    preview.html   ← full browser preview
    html.html      ← ACF HTML field
    css.css        ← ACF CSS field
    js.js          ← ACF JS field (omit if the page has no JS)
```

or, for pages pasted in as several separate blocks:

```
/pages
  /[page-slug]
    README.md
    PASTE-ORDER.md ← which section goes where, in order
    /sections
      [section].html
```

**Pick the shape that matches how the page is actually pasted into the CMS**, not the one that looks
tidiest. A page that goes in as one Code Block is single-file. A page whose CSS and JS live in
separate ACF fields is split-file. A page assembled from several blocks in the editor uses
`sections/` — and then `PASTE-ORDER.md` is not optional, because the order is not recoverable from
the filenames. `voter-guide-2026` is the reference implementation of that pattern.

Do not convert an existing page from one shape to another as a side errand. If the CMS placement
didn't change, the shape shouldn't either.

## Design Tokens

**`~/Projects/vpm/vpm-widgets/tokens.css` is canonical for both repos.** There is deliberately no
copy in this repo — two token files would drift, and the drift would be invisible until two pages
disagreed about VPM blue.

Read that file and copy the custom properties the page actually needs into its own scoped `<style>`
block. Never link it externally: pages must survive as standalone paste-ins. No hard-coded hex
values.

Fuller narrative reference: `~/Projects/vpm/vpm-widgets/BRAND_GUIDE.md`.

## Consuming widgets

Pages hold their **own copy** of any widget markup they include. There is no build step, no package,
and no symlink between the repos — that constraint is what keeps both sides paste-safe for the CMS.

When a page includes a widget, record it in the page's `README.md`:

```
Uses widget: links-with-map (vpm-widgets)
```

That line is the only thing making the dependency findable later, so it isn't optional. When a
widget changes in `vpm-widgets`, grep this repo for its name to find the pages carrying a now-stale
copy.

Live example: `unwined-episode` sits directly above the `links-with-map` widget on the same URL, and
supplies the page-level anchor targets its jump links point at.

## Style Conventions

- All class names namespaced with a page-specific prefix (e.g. `vpm-impact25-`, `vpm-vg26-`)
- BEM naming within the namespace
- No external dependencies unless explicitly approved
- Prefer `px` over `rem` for font-size and spacing in CMS-pasted markup — `rem` resolves against the
  host document root, which WordPress and Brightspot each set differently (see the note at the top of
  `pages/basics-virginia/index.html`)

## Coding Conventions

- IIFE-wrapped JS, no `document.write()`
- WCAG 2.1 AA accessibility
- No external CSS frameworks — inline or scoped styles only
- Self-contained: the file set should work pasted into the CMS with nothing else added

## Workflow

1. Write a brief first (`/brief`) — done criteria, out-of-scope, deploy target
2. Scaffold with `/new-page`, then build
3. Add it under `/pages/[slug]/` following the structure above
4. Write a `README.md` covering purpose, live URL, paste order, and any `Uses widget:` lines
5. **Pre-ship check** (`/ship-page`) — required before pasting into any CMS, see checklist below
6. Commit and push to `main`
7. GitHub Pages preview: `https://mhdesigns98.github.io/vpm-pages/pages/[slug]/`

**If a `BRIEF.md` exists in the page folder, read it before building** and flag requests that
contradict or expand its scope.

VPM brand tokens and voice load automatically via the `vpm-design` skill.

## Pre-Ship Checklist

**This checklist is canonical for pages** — it's the list `/ship-page` enforces. The widget
equivalent lives in `~/Projects/vpm/vpm-widgets/CLAUDE.md` and is a different list on purpose: the
widget harness simulates *a block dropped into a hostile page*, which is not the situation a page
build faces. Don't merge them.

- [ ] Styles fully scoped — unaffected by hostile host CSS (`!important` links, global heading sizes)
- [ ] Every jump link resolves to an anchor that exists, including anchors supplied by a widget
      pasted below the page markup
- [ ] Paste order documented and verified against the live page
- [ ] Each consumed widget's copy matches current `vpm-widgets` source
- [ ] No focus loss or overlap with the sticky Stream Player
- [ ] Degrades gracefully in a 320px column
- [ ] Keyboard accessible, visible focus, WCAG 2.1 AA contrast, `prefers-reduced-motion` respected
- [ ] No console errors

Items deliberately **not** on this list, because they're artifacts of block-in-CMS embedding rather
than page building: duplicate-`id` collisions from placing a block twice, detach/re-inject
double-init, and click-interceptor overlay timing. If a page build ever genuinely faces one of
these, add it here with a note explaining why.

## Pages Index

See `INDEX.md` in the repo root.
