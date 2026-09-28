---
description: Turn an idea into a half-page BRIEF.md before building a page. Usage: /brief [one-line idea] — interviews you briefly, then writes the brief into the page folder so the build starts from agreed requirements instead of discovering them mid-build.
effort: medium
---

Write a page brief BEFORE any code gets written. Play the PM role: pin down the requirements that would otherwise surface as mid-build direction changes.

**Arguments:** $ARGUMENTS

---

## Step 1 — Understand the idea

If `$ARGUMENTS` describes the idea, start from it. Otherwise ask: "What's the idea, in a sentence or two?"

If it will appear on more than one URL, it's a widget, not a page. Stop: it belongs in the `vpm-widgets` repo, which has its own `/brief`.

**If an existing `BRIEF.md` is already in the page folder, read it first, then ask:**
> "Before we update this brief — what have you reconsidered since we last worked on this? What assumptions no longer hold?"
Fold any answers into the brief before proceeding. Skip if this is a fresh page.

## Step 2 — Interview (one message)

Ask only what isn't already clear from the idea. If the answer is vague, reflect back a concrete interpretation and ask for confirmation rather than re-asking open-ended.

1. **User moment** — who lands on this page, why are they there, and what does the page need to do for them in that specific moment? One concrete scenario ("a voter who searched for their polling place and…").
2. **Done** — what does success look like? Be concrete: "live at vpm.org/elections by the 10th," not "looks good."
3. **Out of scope** — what are we explicitly NOT doing in v1? (The scope-creep question — push for at least two real exclusions.)
4. **Live URL** — where on vpm.org will it live?
5. **Paste shape** — how does the page get pasted in: one Code Block, separate ACF fields, or several blocks? This determines the folder shape `/new-page` scaffolds, so it won't ask again.

Audience and content source are usually "VPM site visitors" and "static content, maintained by whoever's driving this" for a page — infer them from the idea and only ask if it genuinely leaves them open.

## Step 3 — Write BRIEF.md

Write `BRIEF.md` into `pages/[slug]/`. If the folder doesn't exist yet, hold the brief and let `/new-page` create the folder and file it. Keep it to half a page:

```markdown
# [Page Name] — Brief
*Written: [date]*

## Problem / Why
[1–2 sentences]

## User moment
[One concrete scenario: who lands on the page, why they're there, what the page does for them in that moment]

## What done looks like
[concrete, observable success criteria — bullet list]

## Out of scope (v1)
- [exclusion]
- [exclusion]

## Deploy target & constraints
[Live URL + paste shape, e.g. "vpm.org/elections — one Code Block, self-contained, no external deps". `/new-page` reads this to pick its shape.]

## Open questions
[anything unresolved — fine to leave items here]
```

**This repo is public, and the brief gets committed with the page.** Keep it to requirements. No
criticism of colleagues or vendors, no embargoed content or publication dates for unpublished
work, no named individuals' contact details. See the public-repo rules in `CLAUDE.md`. If the real
reason for a requirement is sensitive, write the requirement and leave the reason out.

## Step 4 — Confirm and hand off

Show the brief, ask for one round of corrections, then finish with:
> Brief saved to `[path]`. Scaffold the build with `/new-page [name]`.
