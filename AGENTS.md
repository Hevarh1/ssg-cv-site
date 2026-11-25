# AGENTS.md

Hugo personal CV site for Hevar Hemin (university SSG project). Hugo v0.170.0.

## Build
`hugo --minify --panicOnWarning` from this folder checks the build (drafts are skipped). Publishing: every push to `main` runs `.github/workflows/pages.yml`, which builds with Hugo 0.170.0 (`hugo --minify --panicOnWarning -D`) and deploys to https://hevarh1.github.io/ssg-cv-site/, the `baseURL` in `hugo.toml`. -D includes the draft pages; the draft flags stay in the files.

## File map
- `hugo.toml`: title, language, params, main menu.
- `content/`: one Markdown file per page. `content/projects/` holds one page per project; `tags` lists its technologies (plain labels, no tag pages) and optional `link` is the live site.
- `assets/data/`: `experience.json`, `education.json`, `certifications.json`, `skills.json` (JSON arrays of records, as in the course book Ch. 12). The `*-list.html` partials read them with `resources.Get` and `transform.Unmarshal`; a missing file fails the build via `errorf`. JSON has no comments, so each file's sources and TODOs are in the front matter of its content page (`experience.md`, `education.md`, `skills.md`).
- `layouts/`: `baseof.html` (page shell with `block "main"`), `home.html`, `single.html` (About, Contact); `experience.html`, `education.html`, `skills.html` (chosen by `layout:` in the content file); `projects/list.html`, `projects/single.html`; `robots.txt`.
- `layouts/_partials/`: `head.html` (title, description, canonical, Open Graph, favicon, CSS), `header.html`, `nav.html`, `project-link.html`, `footer.html`, `tags.html`, `experience-list.html`, `education-list.html`, `skills-list.html`.
- `assets/css/main.css`: plain CSS, light theme with one accent colour; colours are variables in `:root` at the top. Minified and fingerprinted by Hugo Pipes in `head.html`.
- `static/favicon.svg`: favicon. There is no CV PDF yet (it would expose the phone number; see OPEN-QUESTIONS.md #4).
- `OPEN-QUESTIONS.md`: conflicts and gaps in the sources (local only, ignored by git).
- Never edit `public/`, `resources/` or `.hugo_build.lock` (ignored by git).

## Content rules
0. Links between pages in Markdown are relative (`about/`), never starting with `/`, because the site lives in a subfolder (course book §2.5).
1. Use only facts from the CV files in `~/Downloads` (`Resume_Hevar.pdf` and the other "Hevar Hemin" versions). Never invent or improve employers, dates, numbers, skills or links. `Backend Developer CV-1.pdf` belongs to someone else: never use it.
2. Missing or conflicting facts go in `OPEN-QUESTIONS.md`, with a `TODO` comment in the page's front matter, not in rendered text.
3. Every new content page starts with `draft: true`. Only the owner un-drafts pages.
4. Never publish the phone number, home address, date of birth or ID numbers. Email, GitHub, LinkedIn and hevar.net are approved.
5. No secrets or API keys anywhere.
6. No git commits, pushes or hosting changes unless the owner asks.
7. Data records keep their fields and types. Every record in a file has every field:
   - `experience.json`: `role`, `org`, `place`, `start`, `end` (strings), `points` (array of strings), `stack` (array of strings, `[]` if none).
   - `education.json`: `degree`, `school`, `place`, `start`, `end` (strings).
   - `certifications.json`: `name`, `detail`, `date` (strings).
   - `skills.json`: `group` (string), `items` (array of strings).
