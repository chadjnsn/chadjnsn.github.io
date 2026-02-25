## Optional Eleventy migration plan

This document outlines a future path to rebuild the site using [Eleventy (11ty)](https://www.11ty.dev/) while preserving URLs and GitHub Pages hosting.

### Goals

- Keep or improve current URLs (`/`, `/posts/`, `/404.html`).
- Maintain or improve SEO (titles, descriptions, canonical URLs, social previews).
- Keep the stack simple and easy to maintain.

### Proposed stack

- **Generator**: Eleventy (11ty)
- **Language/content**: Markdown for pages and posts
- **Templating**: Nunjucks or Liquid (your preference)
- **Styling**: Modern CSS (optionally reusing concepts from the current `_sass/_variables.scss`)
- **Build output**: `dist/` directory published to GitHub Pages

### Suggested folder structure

- `package.json` – Eleventy and dev dependencies
- `.eleventy.cjs` – Eleventy configuration
- `src/`
  - `pages/`
    - `index.md` – home page
    - `posts.md` – posts index
    - `404.md` – 404 page
  - `posts/` – individual blog posts (optional to start)
  - `includes/` – partials (header, footer, SEO tags, etc.)
  - `layouts/` – base layouts (`base.njk`, `page.njk`, `post.njk`, etc.)
  - `assets/` – CSS, JS, images, icons (including PWA icons and profile photo)

### URL and content mapping

- Map current Jekyll pages to Eleventy:
  - `index.md` → `src/pages/index.md`
  - `posts.md` → `src/pages/posts.md` (listing posts from `src/posts/`)
  - `404.md` → `src/pages/404.md` with `permalink: "/404.html"`
- If you add posts later:
  - Jekyll `_posts/YYYY-MM-DD-title.md` → Eleventy `src/posts/title.md` with `date` frontmatter.

### SEO and head management

- Create a base layout (e.g. `src/layouts/base.njk`) that:
  - Sets `<title>` from frontmatter with a site-level default.
  - Adds `<meta name="description">` from frontmatter or site default.
  - Includes canonical URL logic based on `site.url` and `page.url`.
  - Adds OpenGraph and Twitter card tags using site-wide defaults and optional per-page overrides.

### GitHub Pages deployment (Eleventy)

1. Add a GitHub Actions workflow (e.g. `.github/workflows/eleventy.yml`) that:
   - Runs `npm ci`
   - Runs `npm run build` (Eleventy outputs to `dist/`)
   - Uploads `dist/` as the Pages artifact
2. Ensure `CNAME` is copied into `dist/` during build (e.g. via a simple copy step or Eleventy passthrough).

### Migration steps (high level)

1. Create a new branch for the Eleventy migration.
2. Add `package.json`, Eleventy config, and the `src/` structure above.
3. Recreate the existing pages (`index`, `posts`, `404`) in Eleventy with equivalent content and URLs.
4. Port over any design elements you care about (e.g. color palette, typography, or particles hero) in a simplified, maintainable way.
5. Run the Eleventy build locally and test all key URLs.
6. Switch the GitHub Actions workflow to build and deploy the Eleventy site instead of Jekyll once you are satisfied.

