---
description: Give a direct share link for a page build. Usage: /share [slug] [note]. The link opens a page that explains what it is and shows the preview at desktop/tablet/mobile width.
---

The share viewer lives in `vpm-widgets` (`share/index.html`) and serves both repos, so there's one
copy to maintain. Follow `.claude/commands/share.md` in the `vpm-widgets` checkout
(`~/Projects/vpm/vpm-widgets`, or the sibling of this repo), with `$ARGUMENTS` passed through.
Page builds use `?p=<slug>`, and the "on `origin/main`?" check runs against this repo
(`pages/<slug>`).

If that file isn't there, run `git pull` in the `vpm-widgets` checkout. If it's still missing,
stop and say so.

Quick reference:

```
https://mhdesigns98.github.io/vpm-widgets/share/?p=<slug>&note=<url-encoded note>&view=mobile
```
