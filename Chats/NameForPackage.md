# Name For Package

## Bruce's Ask

So now that fifteenth supports github pages, and be-persistent support it, at least testing and documentation wise, I thought I'd move on to looking at gist-in.  The name of gist-in seems too specialized when considering support for git pages.  

I thought maybe the package should be called git-in.  A quick google search seemed to indicate that git-in wasn't already taken, but of course it is.

Can you suggest a good name that seems unlikely to already be taken up (or too close to pass through npm's mysterious dedup algorithm)?

I was thinking maybe pipe-in should include this, but the differences are significant enough that I think it makes sense to have a separate package, but name wise, pipe-in has the nice feature of not being "boxed in" the way gist-in is.

Please add your suggestions below.

## Claude's Suggestions

Agreed on keeping it a separate package rather than folding into `pipe-in` —
`gist-in`'s README already frames itself as "a very thin wrapper around
pipe-in" for one specific source; a second thin wrapper for
`githubpages://` is the same shape of thing, not a reason to merge pipe-in's
general fetch/stream/sanitize machinery with source-specific USL handling.

`git-in` and `gitin` are both taken (confirmed via the registry, not just
Google — `registry.npmjs.org/git-in` and `/gitin` both `200`). Checked a
shortlist of alternatives that keep the `<noun>-in` family shape `gist-in` /
`pipe-in` already established — all confirmed **unclaimed** (`404` from the
registry):

| Name | Read | Available |
|---|---|---|
| **`blob-in`** | *pull in a git blob* | ✅ |
| `raw-in` | *pull in a raw URL* | ✅ |
| `repo-in` | *pull in from a repo* | ✅ |
| `hub-in` | *pull in from (git)Hub* | ✅ |
| `ref-in` | *pull in a git ref* | ✅ |

**Recommendation: `blob-in`.** A gist file and a GitHub Pages repo file are
both, literally, git blobs — that's the one word that actually generalizes
across `gist://` and `githubpages://` without implying either source
specifically, which is exactly the "boxed in" problem you flagged with
`gist-in`. It also reads the same way in an attribute as the two existing
packages do:

```html
<template blob-in="githubpages://bahrus/repo:be-persistent/README.md" blob-in-for="options"></template>
```

On the "too close to pass npm's dedup" worry: the `<word>-in` suffix pattern
itself is already proven safe — `gist-in` (from `gist`) and `pipe-in` (from
`pipe`) both published fine, so a short common word plus `-in` isn't what
trips npm's typosquat-similarity check. None of the five above are near-misses
of `git-in`, of each other, or of any well-known package I could find, so I
wouldn't expect a dedup rejection on any of them.

If you'd rather stay closer to the literal vocabulary already in the code
(`readVia: 'raw'`, `raw.githubusercontent.com`, gist's own "raw form"),
**`raw-in`** is the strongest runner-up — it's the exact word this whole
session has already been using for "the fast, tokenless read path" on both
protocols. `repo-in` reads a little oddly for the gist case (a gist isn't
user-facing "a repo"), so I'd rank it third.
