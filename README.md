# VPM Pages

Full page builds for vpm.org — one folder per page, under `/pages/`.

Reusable blocks live in the sibling repo, [vpm-widgets](https://github.com/mhdesigns98/vpm-widgets).

## Which repo?

> **A widget is used on more than one page. A page build is used on exactly one.**

The test is reuse, not size. A small block that only ever appears on one URL belongs here.

## Structure

A page folder takes one of three shapes, matching how the page is actually pasted into the CMS:

```
/pages/[page-slug]/
    README.md      ← purpose, live URL, "Uses widget:" lines, paste order
    index.html     ← single-file: self-contained page, pasted whole into a Code Block
```

```
/pages/[page-slug]/
    preview.html   ← full browser preview
    html.html      ← ACF HTML field
    css.css        ← ACF CSS field
    js.js          ← ACF JS field
```

```
/pages/[page-slug]/
    PASTE-ORDER.md ← which section goes where, in order
    /sections/[section].html
```

All class names are namespaced to avoid conflicts with the host page.

## Pages

See [`INDEX.md`](INDEX.md).

## Design tokens

`tokens.css` in [`vpm-widgets`](https://github.com/mhdesigns98/vpm-widgets) is canonical **for both repos**. There is deliberately no
copy here. Read it and inline the properties a page needs into its own scoped `<style>` block; never
link it externally.

Narrative reference: `vpm-widgets/BRAND_GUIDE.md`, and the rendered
[brand guide](https://mhdesigns98.github.io/vpm-widgets/brand-guide.html).

## Claude Code setup

Clone this repo and [`vpm-widgets`](https://github.com/mhdesigns98/vpm-widgets) side by side, in the
same parent folder, then open a Claude Code session here. The slash commands below and a
`vpm-design` pointer skill are committed in `.claude/`, and they read tokens and brand rules from
`../vpm-widgets`. There's nothing else to install.

## Adding a new page

1. `/brief [idea]` first, for anything beyond a trivial tweak. It writes `pages/[slug]/BRIEF.md`
   (this repo is public, so the brief gets committed too; keep it to requirements)
2. `/new-page [slug]` — scaffolds the folder, inlines tokens, adds the `INDEX.md` row
3. Build it; namespace every class (e.g. `vpm-impact25-`)
4. Record any widgets it consumes in the page `README.md` as `Uses widget: [slug] (vpm-widgets)`
5. `/ship-page [slug]` before pasting into any CMS
6. Commit and push — preview at `https://mhdesigns98.github.io/vpm-pages/pages/[slug]/`
