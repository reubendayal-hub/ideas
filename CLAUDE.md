# ideas — Reuben's shared pages

A plain static site of standalone HTML pages that Reuben shares for review: cricket club (FCC) proposals, side projects, one-off comparisons. There's no build step, no framework and no package.json.

## Layout

```
index.html                 # landing page: a list of links to every page
<slug>/index.html          # one self-contained page per folder, served at /<slug>
CLAUDE.md                  # this file (not linked from the site)
```

- **One page per folder.** Each page is a single self-contained `index.html`: inline `<style>`, images embedded as `data:` URIs, no local assets and no JS unless the page really needs it.
- **Slugs** are kebab-case and prefixed by context where that helps (for example `fcc-shed-options`). The URL is `/<slug>`.
- **Landing page:** every new page gets an `<a class="item" href="/<slug>">` entry in the root `index.html` list, with a `.title` and a one-line `.desc`. Newest goes first.

## Style conventions (match the existing pages)

- Colour tokens on `:root`: `--navy #1e2f4a`, `--gold #b89a6a`, `--golddk #9a7d4f`, `--cream`, `--bg`, `--card`, `--border`, `--text`, `--muted`.
- Dark mode: redefine the tokens under `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) … }` and again under `:root[data-theme="dark"]`.
- System font stack. Mobile-first: `viewport-fit=cover`, safe-area insets, no horizontal scroll at phone width.

## Adding a page

1. Create `<slug>/index.html` (the zips Reuben supplies usually already have this shape; unzip them at the repo root).
2. Add the link card to the root `index.html`.
3. Commit and push to `main`.
4. Deploy with `vercel --prod` from the repo root.

## Deploy

- Hosted on Vercel as a static project linked through `.vercel/` (gitignored). Vercel serves `/<slug>` from `<slug>/index.html` without any config.
- `vercel --prod` deploys production. The project may also be connected to GitHub for auto-deploys on push to `main`; check the Vercel dashboard before assuming it is.
- These pages are public once deployed. Don't add anything private (member personal data, contact details, finances) unless Reuben confirms it's OK to publish.

## Relationship to FCC

This repo is cloned inside `~/Documents/GitHub/FCC/ideas` but is a **separate git repo and separate Vercel project**. Don't commit it into the FCC repo, and don't touch FCC's deploy from here.
