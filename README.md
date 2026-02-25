## Personal site - chadjohnson.io

This repository contains the source for my personal site, hosted on GitHub Pages at `https://chadjohnson.io/`.

The site is built with **Jekyll** using the [`cvless`](https://github.com/piazzai/cvless) theme and deployed via a GitHub Actions workflow in `.github/workflows/jekyll.yml`.

### Local development

1. Install Ruby (the project is currently pinned to version `3.1` in `.ruby-version`).
2. Install Bundler if you don't already have it:

   ```bash
   gem install bundler
   ```

3. Install dependencies and create `Gemfile.lock`:

   ```bash
   bundle install
   ```

4. Run the site locally:

   ```bash
   bundle exec jekyll serve
   ```

   Then open `http://localhost:4000` in your browser.

### Profile photo

The home page can display a profile photo if `site.photo` is set in `_config.yml`. To enable this:

- Add your profile image to the repository (for example at `assets/files/profile.jpg`).
- Update the `photo` setting in `_config.yml` to point to that file.

### PWA manifest and icons

The site includes a basic web app manifest at `assets/site.webmanifest`. To fully enable icons on various devices:

- Provide icon image files matching the paths referenced in `assets/site.webmanifest` (e.g. `android-chrome-192x192.png`, `android-chrome-512x512.png` in the site root or adjust the paths to wherever you store them).

