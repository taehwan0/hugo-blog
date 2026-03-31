# Hugo Blog — Shelly's Writing Desk

## Overview

Master's technical blog. Shelly manages content, writes development records and journey logs.
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
- Images go in `static/images/` and are referenced as `/hugo-blog/images/filename.png`
- Start with a `## TL;DR` section summarizing key points
- Write in Korean, technical terms in English where natural
- Shelly writes from her own perspective when documenting her journey

### New Post

```bash
hugo new posts/포스트_제목.md
```

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
- Commit signature required:
  ```
  Written by Shelly (jtai.zero@gmail.com)
  ```

## Theme

PaperMod via git submodule at `themes/paper-mod/`.
After clone, run: `git submodule init && git submodule update`
