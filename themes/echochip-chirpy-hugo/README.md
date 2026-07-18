# Echochip Chirpy Hugo Theme

## Requirements

- Hugo `0.158.0` or newer.
- Use `locale` in the site config for newer Hugo versions.

```toml
baseURL = "https://example.com/"
title = "Your Blog"
theme = "echochip-chirpy-hugo"
locale = "ko-KR"
enableRobotsTXT = true

[taxonomies]
category = "categories"
tag = "tags"

[params]
description = "Site description"
author = "Author Name"
tagline = "Short site tagline"       # supports inline HTML, e.g. a <br> line break — render with | safeHTML
favicon = "/favicon.ico"
avatar = "/images/avatar.png"        # sidebar profile photo, square image recommended (~400x400)
image = "/images/site-cover.jpg"     # fallback og:image when a page has no cover/image of its own

[params.social]
github = "https://github.com/yourname"
twitter = "https://x.com/yourname"
threads = "https://www.threads.com/@yourname"
email = "you@example.com"

# Goldmark's strikethrough extension treats a bare "~" as a delimiter too,
# not just "~~" — turn it off if your content uses "~" for numeric ranges
# (e.g. "15~16일"), otherwise arbitrary text gets wrapped in <del>.
[markup.goldmark.extensions]
strikethrough = false
```

## Post Front Matter Extras

- `cover.image` / `cover.alt` / `cover.caption` — renders as a captioned image at
  the top of the post body (use `cover.caption` for photo attribution, e.g.
  Unsplash credit) and is reused for `og:image`/`twitter:image`/JSON-LD `image`
  (falls back to a flat `image:` field, then `site.Params.image`, if `cover` is absent).
- `faq: [{q: "...", a: "..."}, ...]` — emits an additional `FAQPage` JSON-LD
  block alongside the `BlogPosting` schema. Render the Q&A in the post body
  yourself; this only adds the structured data.
- Prev/next-post navigation and the "관련된 글" (related posts) block only
  render on pages in the `posts` section — they're skipped on About/policy
  pages so a legal page doesn't show unrelated blog posts as "related".

## Required Content Pages

Create these files in the site using the theme if you want the sidebar
`archives` and `about` links to resolve.

`content/archives/_index.md`

```markdown
---
title: "Archives"
layout: "archives"
---
```

`content/about/_index.md`

```markdown
---
title: "About"
---

Write your profile or site information here.
```

## Footer Policy Links (AdSense checklist)

The footer renders a fixed row of links to five pages that Google/AdSense
reviewers typically expect a monetized blog to have. Create these at the
site root (paths are hardcoded in `partials/footer.html`):

```
content/about.md              -> /about/            "소개"
content/editorial-policy.md   -> /editorial-policy/  "편집 정책"
content/privacy.md            -> /privacy/           "개인정보처리방침"
content/disclaimer.md         -> /disclaimer/        "면책조항"
content/contact.md            -> /contact/           "문의"
```

If a page doesn't exist yet the link will 404 — either create a stub or
edit the href list in `partials/footer.html` to match your site.

## Notes

- Social icons are rendered only when their values are configured.
- Post pages emit Open Graph, Twitter Card, and BlogPosting JSON-LD metadata.
- The theme uses an inline theme bootstrap script to avoid a light flash before dark mode is applied.
