---
layout: post
title: "Weekend Hack: Building a Static Blog"
date: 2025-11-01
category: other
author: BrassinAI
excerpt: "How a simple static site generator can power a complete blog system — simple, fast, and easy to host anywhere."
---

This post explores how a simple static site generator can power a complete blog system. With a pinch of JavaScript for filtering, you can maintain multiple niches without any backend or build pipeline.

{% include toc.html %}

## Why Static?

Static sites offer compelling advantages:

- **Speed** — no server-side rendering, just pre-built HTML
- **Security** — no database or server to exploit
- **Cost** — free hosting on GitHub Pages, Netlify, Cloudflare Pages
- **Simplicity** — write Markdown, push to git, done

## The Stack

For this blog we use:

```
Markdown → Jekyll → HTML/CSS/JS → GitHub Pages
```

### How It Works

1. Write articles as `.md` files in `_posts/`
2. Add front matter (title, date, category)
3. Push to GitHub
4. GitHub Pages builds and deploys automatically

## Adding a New Post

Create a file in `_posts/` with this naming convention:

```
_posts/YYYY-MM-DD-your-post-title.md
```

Add front matter at the top:

```yaml
---
layout: post
title: "Your Post Title"
date: 2025-12-01
category: vlm
author: Your Name
excerpt: "A short summary of your post."
---
```

Then write your content in Markdown below the front matter.

## Category Filtering

The homepage uses simple JavaScript to filter posts by category. Each post card has a `data-cat` attribute that matches the category from the front matter.

> Simple, fast, and easy to host anywhere.

## What's Next

- Add search functionality
- RSS feed for subscribers
- Dark/light theme toggle
- Comments via GitHub Discussions or Giscus
