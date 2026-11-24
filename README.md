# Hevar Hemin: CV site

Personal CV and portfolio of Hevar Hemin, built with [Hugo](https://gohugo.io/) as a university static site generator (SSG) project.

**Live site:** https://hevarh1.github.io/ssg-cv-site/

## Run locally

Requires Hugo 0.170.0 or newer.

```sh
hugo server -D        # preview at http://localhost:1313/ (includes draft pages)
hugo --minify -D      # build into public/
```

## Deploy

Every push to `main` builds the site and publishes it to GitHub Pages through `.github/workflows/pages.yml`.

## Structure

- `content/`: one Markdown file per page; `content/projects/` holds the project pages
- `assets/data/`: experience, education, certifications and skills (JSON)
- `layouts/`: Hugo templates and partials
- `assets/css/main.css`: styles (light/dark, print)
- `static/`: favicon
