# Quarto project conventions

This is a Quarto website. All pages are authored as `.qmd` files and rendered to static HTML.

## Building & previewing

- **Render locally**: `quarto render` — regenerates all HTML in `docs/`.
- **Live-reload preview**: `quarto preview` — starts a dev server on http://localhost:3000; auto-rebuilds on file changes.

## Project structure

- `_quarto.yml` — site configuration (output directory, theme, partials).
- `styles.css` — all CSS; defines design tokens as custom properties (`--bg`, `--text`, `--accent`, etc.).
- `partials/` — HTML snippets injected into every page:
  - `head-theme-init.html` — pre-paint theme script (reads `localStorage.theme`).
  - `header.html` — site header with nav and theme toggle.
  - `footer.html` — site footer + `js/theme.js` script.
- `js/theme.js` — theme toggle logic; persists choice to `localStorage`.
- `images/` — avatar, favicons, etc.
- `index.qmd` — home page (hero layout).
- `about/index.qmd`, `cv/index.qmd`, `contact/index.qmd` — pretty-URL pages.
- `blog/index.qmd` — blog listing page (Quarto `listing:` directive).
- `blog/posts/*/index.qmd` — individual blog posts.
- `404.qmd` — 404 page (renders to `docs/404.html`).
- `docs/` — generated output (never hand-edited); deployed via GitHub Pages.

## URL convention

Use **folder + `index.qmd`** for every page so output paths stay pretty:
- `about/index.qmd` → `docs/about/index.html` → `/about/`
- `cv/index.qmd` → `docs/cv/index.html` → `/cv/`
- `contact/index.qmd` → `docs/contact/index.html` → `/contact/`
- `blog/index.qmd` → `docs/blog/index.html` → `/blog/`

## Design system

All design lives in `styles.css`:
- **Custom properties** (lines 6–48): `--bg`, `--text`, `--accent`, theme pairs for light/dark.
- **Layout**: `.wrap` max-width container; semantic spacing.
- **Components**: `.hero` (avatar + title), `.links-row` (social links), `.cv-entry` (work/education), `.skill-row` (skill ratings), `.contact-list` (contact rows).
- **Typography**: monospace titles, system fonts only.

Dark/light toggle reads/writes `data-theme` on `<html>` via `localStorage`; CSS respects both explicit `[data-theme]` attrs and `prefers-color-scheme`.

## Header/footer via partials

The site **intentionally skips Quarto's default navbar** (`website.navbar`, `theme: cosmo`, etc.). Instead:
- Config sets `format.html.theme: none` (no Bootstrap).
- `include-in-header: partials/head-theme-init.html` injects the pre-paint theme script.
- `include-before-body: partials/header.html` injects the custom header/nav.
- `include-after-body: partials/footer.html` injects the custom footer + theme script.

This keeps the hand-built design unchanged and avoids Bootstrap leakage. The nav is static (all pages identical); there's no active-page indicator beyond CSS `:hover` effects.

## Blog authoring

To add a blog post:
1. Copy `blog/posts/welcome-to-quarto/` to `blog/posts/my-new-post/`.
2. Edit `index.qmd`: update frontmatter (title, date, categories, description) and body.
3. Use `` ```{r} `` code blocks for R (renders output automatically).
4. Run `quarto render` to regenerate.

The blog listing page (`blog/index.qmd`) auto-discovers posts in `blog/posts/` via the `listing:` directive.

## Deployment

No CI—render locally, commit `docs/`, and push:
```
quarto render
git add -A
git commit -m "..."
git push origin master
```

GitHub Pages serves from the `/docs` folder of the `master` branch (configure in Repo Settings → Pages).

## Common edits

- **Tweak colors**: edit `--bg`, `--text`, `--accent` etc. in `styles.css`.
- **Change header nav**: edit `partials/header.html`.
- **Update bio/CV text**: edit `about/index.qmd`, `cv/index.qmd` directly (Quarto renders the `.qmd` → HTML on every `quarto render`).
- **Add a new top-level page**: create `my-page/index.qmd` with YAML frontmatter + content (will auto-render to `docs/my-page/index.html`).
