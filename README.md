# dougaparry.com

Personal academic website, built with [Quarto](https://quarto.org) and deployed
to Netlify from GitHub.

## Structure

```
_quarto.yml          Site config: navbar, theme, fonts
styles.scss          The look & feel (clean minimal, teal accent)
index.qmd            Landing page (about, photo, links)
publications.qmd     Publications list
blog.qmd             Blog listing page
posts/               One folder per blog post
  _metadata.yml      Settings applied to all posts (incl. freeze)
  welcome/index.qmd  Example post with runnable R
images/              profile.jpg, favicon.png  (replace the placeholders)
files/               cv.pdf and files/papers/*.pdf
_freeze/             Cached R output (auto-created; commit it)
netlify.toml         Build config for Netlify
```

## First-time setup

1. Install Quarto: <https://quarto.org/docs/get-started/>
   (on macOS: `brew install --cask quarto`)
2. For the R blog posts, install R and the `rmarkdown` package:
   `install.packages("rmarkdown")`

## Everyday workflow

```bash
quarto preview      # live preview at localhost while you edit
quarto render       # build the whole site into _site/
```

Then commit and push. **Commit the `_freeze/` folder** — it holds the cached R
results so Netlify can build without needing R installed.

```bash
git add -A
git commit -m "Update site"
git push
```

Netlify rebuilds automatically on push.

## Replace the placeholders

- `images/profile.jpg` — your photo (square works best)
- `images/favicon.png` — small site icon
- `files/cv.pdf` — your real CV
- Social links and email in `_quarto.yml` and `index.qmd`
- Publications in `publications.qmd` (a template block is included)

## Add a blog post

```bash
mkdir posts/my-new-post
```

Create `posts/my-new-post/index.qmd` with front matter:

```yaml
---
title: "My post title"
description: "One-line summary shown on the blog list."
date: "2026-07-15"
categories: [R, methods]
---
```

Write prose and R chunks. Run `quarto render`, commit (with `_freeze/`), push.

## Deployment

Connect this GitHub repo to Netlify once. `netlify.toml` tells Netlify to
download the Quarto CLI and run `quarto render`; because R output is frozen,
no R is needed on the build server.
