# AGENTS.md

Hugo personal CV site for Hevar Hemin (university SSG project). Hugo v0.170.0.

## Build
`hugo --minify --panicOnWarning` from this folder checks the build (drafts are skipped). Publishing: every push to `main` runs `.github/workflows/pages.yml`, which builds with Hugo 0.170.0 (`hugo --minify --panicOnWarning -D`, baseURL taken from the Pages settings) and deploys to https://hevarh1.github.io/ssg-cv-site/. -D includes the draft pages; the draft flags stay in the files. `baseURL` in `hugo.toml` stays `https://hevar.net/ssg/` for the copy built into HevarNet's `public/ssg`.

## File map
- `hugo.toml`: title, language, params, main menu.
- `content/`: one Markdown file per page. `content/projects/` holds one page per project (tagged by technology).
- `data/`: `experience.yaml`, `education.yaml`, `skills.yaml`. Looped by the `*-list.html` partials (read with `hugo.Data`, not the deprecated `site.Data`).
- `layouts/`: `baseof.html` (page shell with `block "main"`), `home.html`, `single.html`, `list.html` (generic fallbacks); `experience.html`, `education.html`, `skills.html` (chosen by `layout:` in the content file); `projects/list.html`, `projects/single.html`; `taxonomy.html` and `term.html` for `/tags/`; `robots.txt`.
- `layouts/_partials/`: `head.html` (title, description, canonical, Open Graph, favicon, CSS), `header.html`, `nav.html`, `footer.html`, `tags.html`, `experience-list.html`, `education-list.html`, `skills-list.html`.
- `assets/css/main.css`: plain CSS (light/dark tokens, print styles), processed by Hugo Pipes.
- `static/favicon.svg`: favicon. There is no CV PDF yet (it would expose the phone number; see OPEN-QUESTIONS.md #4).
- `OPEN-QUESTIONS.md`: conflicts and gaps in the sources (local only, ignored by git).
- Never edit `public/`, `resources/` or `.hugo_build.lock` (ignored by git).

## Content rules
1. Use only facts from the CV files in `~/Downloads` (`Resume_Hevar.pdf` and the other "Hevar Hemin" versions). Never invent or improve employers, dates, numbers, skills or links. `Backend Developer CV-1.pdf` belongs to someone else: never use it.
2. Missing or conflicting facts go in `OPEN-QUESTIONS.md`, with a `TODO` comment in the page's front matter, not in rendered text.
3. Every new content page starts with `draft: true`. Only the owner un-drafts pages.
4. Never publish the phone number, home address, date of birth or ID numbers. Email, GitHub, LinkedIn and hevar.net are approved.
5. No secrets or API keys anywhere.
6. No git commits, pushes or hosting changes unless the owner asks.
