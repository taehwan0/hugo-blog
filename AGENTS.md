# Hugo Blog

## Overview

Personal technical blog.
Built with Hugo + PaperMod theme, deployed to GitHub Pages via GitHub Actions.

- **URL:** https://taehwan0.github.io/hugo-blog/
- **Language:** Korean (ko-KR)
- **Comments:** Utterances (GitHub Issues)

## Content Structure

```
content/
├── posts/          # Blog posts (Korean, underscore-separated filenames)
├── search.md       # Search page
├── portfolio.md    # Portfolio page
└── archives.md     # Archives page
```

## Writing Posts

### Front Matter

```yaml
---
date: '2026-04-01T00:00:00+09:00'
draft: false
title: '포스트 제목'
showToc: true
TocOpen: true
---
```

### Conventions

- Filenames: Korean with underscores (e.g., `이벤트_왜_그리고_어떻게.md`)
- Images: see [Including Internal Content](#including-internal-content)
- Start with a `## TL;DR` section summarizing key points
- Write in Korean, technical terms in English where natural

### New Post

```bash
hugo new posts/포스트_제목.md
```

## Including Internal Content

### Images

All images live in `static/images/` and are referenced with a root-relative path that includes the `/hugo-blog/` base path.

```markdown
![대유쾌마운틴](/hugo-blog/images/daeyukwae-mountain.png)
```

| Item | Rule |
|------|------|
| Location | `static/images/<filename>` (flat, no subdirectories) |
| Reference | `/hugo-blog/images/<filename>` |
| Filename | Lowercase English, words joined by `-` or `_` (e.g. `event-sequence.png`, `k6_failed.png`) |
| Alt text | Short Korean description of the image |

Do not:

- Leave images in `content/posts/`. Hugo does not copy them into the post's output, so they never get served.
- Reference a local absolute path (e.g. `/Users/.../content/posts/foo.png`). Editors insert this when an image is dragged in; it works only on the author's machine.
- Use `../../images/<filename>`. It depends on the page's URL depth and breaks in the RSS feed, where Hugo rewrites `/hugo-blog/...` to an absolute URL but leaves `../` paths untouched.
- Use Korean or spaces in filenames. macOS stores them as NFD, while Markdown text is usually NFC, so the same-looking path can fail to match.

### Adding an Image

1. Copy or move the file into `static/images/` and rename it to follow the filename rule.
2. Insert `![<alt>](/hugo-blog/images/<filename>)` in the post.
3. Remove any copy left in `content/posts/`.
4. Verify the image appears in the build output:

   ```bash
   hugo build -D --destination /tmp/hugo-check
   ls /tmp/hugo-check/images/<filename>
   grep -o '<img[^>]*<filename>[^>]*>' -r /tmp/hugo-check/posts
   ```

If `baseURL` in `hugo.yaml` ever changes its path (`/hugo-blog/`), every image reference must be updated to the new path.

## Build & Preview

```bash
# Local preview
hugo server -D

# Build
hugo build --gc --minify
```

## Deployment

Automatic via GitHub Actions on push to `master` branch.
Hugo version: 0.147.6 (extended)

## Git

- Branch: `master` (single branch, auto-deploys)

## Theme

PaperMod via git submodule at `themes/paper-mod/`.
After clone, run: `git submodule init && git submodule update`
