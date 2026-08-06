# The Basics Virginia™ — Page Composite

Full page build for The Basics Virginia™, compiled into a single Brightspot HtmlModule drop-in.

**Shape:** single-file. Paste `index.html` whole into one HtmlModule.

## Sections (top to bottom)

1. Hero
2. 5 Principles Grid
3. The Basics in Action
4. The Movement (includes Toolkits video)
5. Nature Trail CTA

## Notes

- Built as web components (`<basics-hero-section>`, etc.), so the custom element definitions must
  come along with the markup — don't split them out.
- **All `font-size` and spacing values use `px`, not `rem`, on purpose.** `rem` resolves against the
  host document root, and Brightspot and WordPress each set that differently, so `rem` values render
  at the wrong size inside the CMS. This holds even inside Shadow DOM. Keep new values in `px`.
