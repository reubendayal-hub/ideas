# ideas — Reuben's shared pages

A plain static site of standalone HTML pages that Reuben shares for review: cricket club (FCC) proposals, side projects, one-off comparisons. There's no build step, no framework and no package.json.

## Layout

```
index.html                 # neutral landing page, deliberately does NOT list pages
<slug>/index.html          # one self-contained page per folder, served at /<slug>
vercel.json                # cleanUrls + noindex / no-referrer headers on every path
CLAUDE.md                  # this file (not served in any linked way)
```

- **One page per folder.** Each page is a single self-contained `index.html`: inline `<style>`, images embedded as `data:` URIs, no local assets and no JS unless the page really needs it.
- **Slugs** are kebab-case and prefixed by context where that helps (for example `fcc-shed-options`). The URL is `/<slug>`.
- **Link-only visibility:** pages are unlisted, not password-protected. Anyone with the URL can open it. So:
  - Never link pages from the root `index.html`, and never link one page from another.
  - Every page's `<head>` has `<meta name="robots" content="noindex, nofollow">`. `vercel.json` also sends `X-Robots-Tag: noindex` for all paths. Don't add a robots.txt `Disallow`, because it would stop crawlers from seeing the noindex.
  - For anything sensitive, give the slug an unguessable suffix (for example `fcc-budget-7k2q9x`).
- **Page register** (the only list of pages; keep it updated here, not on the site):
  - `fcc-shed-options`: FCC shed kits vs the kommune-approved design, Karlebo Cricket Ground.

## Style conventions (match the existing pages)

- Colour tokens on `:root`: `--navy #1e2f4a`, `--gold #b89a6a`, `--golddk #9a7d4f`, `--cream`, `--bg`, `--card`, `--border`, `--text`, `--muted`.
- Dark mode: redefine the tokens under `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) … }` and again under `:root[data-theme="dark"]`.
- System font stack. Mobile-first: `viewport-fit=cover`, safe-area insets, no horizontal scroll at phone width.

## Adding a page

1. Create `<slug>/index.html` (the zips Reuben supplies usually already have this shape; unzip them at the repo root).
2. Add the robots meta tag and add the page to the register above. Don't link it from the site.
3. Commit and push to `main`.
4. Deploy with `vercel --prod` from the repo root.

## Deploy

- Hosted on Vercel as a static project called `ideas`, linked through `.vercel/` (gitignored). Vercel serves `/<slug>` from `<slug>/index.html`.
- Share links as `https://reubendayal.vercel.app/<slug>`. That domain is attached to the `ideas` project, so every `vercel --prod` updates it. Reuben chose it over a nordicanchor.dk subdomain to keep these pages separate from the business brand. Don't share `ideas-*.vercel.app` URLs: per-deployment URLs sit behind Vercel login protection.
- `vercel --prod` deploys production. The project may also be connected to GitHub for auto-deploys on push to `main`; check the Vercel dashboard before assuming it is.
- These pages are public once deployed. Don't add anything private (member personal data, contact details, finances) unless Reuben confirms it's OK to publish.

## Relationship to FCC

This repo is cloned inside `~/Documents/GitHub/FCC/ideas` but is a **separate git repo and separate Vercel project**. Don't commit it into the FCC repo, and don't touch FCC's deploy from here.
