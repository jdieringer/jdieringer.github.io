# jdieringer.github.io

Personal project portfolio — a single, self-contained static site (no build step).

**Live:** https://jdieringer.github.io

## Files

| File | Purpose |
|---|---|
| `index.html` | Landing page — hero, about, and the project cards. |
| `projects/*.html` | One design-notes page per project. |
| `flash.html` | In-browser firmware flasher (ESP Web Tools / Web Serial). |
| `firmware/` | One folder per flashable build — see `firmware/README.md`. |
| `assets/site.css` | Shared stylesheet for every page (edit the theme here). |
| `assets/site.js` | Shared reveal-on-scroll script. |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (skips Jekyll processing). |
| `README.md` | This file. |

Each project card on the landing page links to its design-notes page in `projects/`.
The whole site is static — no build step.

## Deploy (one-time setup)

This is a **GitHub user site**, so it must live in a repo named exactly `jdieringer.github.io`.

```bash
cd /Users/jdieringer/Projects/jdieringer
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/jdieringer/jdieringer.github.io.git
git push -u origin main
```

Then on GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `root`.**
The site goes live at https://jdieringer.github.io within a minute or two.

## Updating

Edit `index.html`, then:

```bash
git add index.html && git commit -m "Update" && git push
```

Pages redeploys automatically on push.

## To do / customize

- **Add repo links.** Each design-notes page (`projects/*.html`) has a `Repo` button in its footer marked `aria-disabled="true"`. When a repo is public, set its `href` and remove the `aria-disabled` attribute.
- **Update firmware** after a rebuild — see `firmware/README.md`.
- **Edit the theme** — colors, fonts, spacing — in one place: `assets/site.css` (the `:root` block at the top holds the Ohio State scarlet/gray palette).
- **Tweak the hero copy** in the `.hero` section of `index.html`.
- **Add a project** by copying an existing `<article class="card reveal">…</article>` block in `index.html` (point its `.stretch` link at the new page) and duplicating a file in `projects/` as a starting template.
