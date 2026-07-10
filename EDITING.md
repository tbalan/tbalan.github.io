# How to edit this site

This site is built with **Quarto**, a modern authoring tool for scientists and data professionals. You write markdown, Quarto renders it to static HTML, and GitHub Pages serves it.

## Editing workflow

### 1. Preview changes locally

Before committing, start a live-reload server:
```bash
quarto preview
```

Then open http://localhost:3000 in your browser. The site will auto-rebuild whenever you save a file.

### 2. Edit pages

Pages are stored in `.qmd` files (Quarto markdown):
- **Home**: `index.qmd` — your hero, avatar, tagline, social links.
- **About**: `about/index.qmd` — biography.
- **CV**: `cv/index.qmd` — work experience, education, skills.
- **Contact**: `contact/index.qmd` — email, GitHub, LinkedIn, etc.
- **Blog**: `blog/index.qmd` — auto-generated listing of your posts.

Just edit the text and save. If `quarto preview` is running, you'll see changes instantly.

### 3. Add a blog post

1. **Copy the template**:
   ```bash
   cp -r blog/posts/welcome-to-quarto blog/posts/my-new-post
   ```

2. **Edit** `blog/posts/my-new-post/index.qmd`:
   - Update the frontmatter (title, date, categories, description).
   - Write your post in markdown.
   - Include R code blocks: `` ```{r} `` ... `` ``` ``
   - Save.

3. The blog listing automatically picks up your new post.

### Example blog post structure

```markdown
---
title: "My First Post"
date: 2026-07-11
categories:
  - r
  - data-science
description: "A brief description of what you wrote."
---

Your post text goes here in markdown.

## Code example

```{r}
# This R code will run and output results
summary(mtcars)
plot(mtcars$wt, mtcars$mpg)
```
```

### 4. Update the design

Colors and fonts live in `styles.css`. Edit the custom properties at the top (lines 6–48) to tweak the color scheme or font stack. The CSS respects both light and dark themes automatically.

## Publishing

Once you're happy with your changes:

1. **Render** (generate all HTML):
   ```bash
   quarto render
   ```

2. **Commit**:
   ```bash
   git add -A
   git commit -m "update bio" # or whatever you changed
   ```

3. **Push**:
   ```bash
   git push origin master
   ```

That's it — GitHub Pages will serve the `docs/` folder within seconds.

## Tips

- Use `quarto preview` for iterative editing—much faster than commit-render-push cycles.
- The live-reload server catches most syntax errors and shows you them instantly.
- Blog post dates are sorted newest-first automatically.
- You can add new top-level pages by creating a new folder (e.g., `my-page/index.qmd`); Quarto will render it to `/my-page/`.
- The design system is CSS-based and theme-aware; the theme toggle in the header persists your choice to `localStorage`.

## Troubleshooting

- **Render fails with "file not found"**: check that image paths are absolute (e.g., `/images/avatar.jpg`, not `images/avatar.jpg`).
- **Blog post doesn't appear**: verify the post is in `blog/posts/your-post/index.qmd` and has YAML frontmatter with at least `title:` and `date:`.
- **Colors look wrong**: clear your browser cache (Ctrl+Shift+Delete) or open in an incognito tab.
- **Links break**: remember the site uses pretty URLs — link to `/about/` not `/about/index.html`.
