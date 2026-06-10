# Academic Portfolio — Hugo Template

A quiet, paper-like academic portfolio and research blog, built with **Hugo**
(Extended). Bio, research interests, publications, news, CV, and a bilingual-ready
blog - with a warm off-white palette and the bilingual **Chiron GoRound TC**
typeface so Latin and Hangul render with equal care.

It is intentionally dependency-light: no Node.js, no JS framework, no build step
beyond the Hugo binary. A small zero-dependency Python dashboard (`cms-server.py`)
lets you edit content and settings from the browser when you want to.

## Features

- **Multilingual** out of the box (English + Korean demo) with a header language
  dropdown. Add or remove languages from config.
- **Owner-configurable** from `config/_default/params.yaml` (or the admin dashboard):
  identity and social links, a named **color palette**, and which **sections** appear.
- **Light/dark mode** - a visitor toggle in the header, remembered per browser, with
  no flash on load and respect for the OS preference.
- **Content dashboard** at `/admin/` — schema-driven editors for publications, news,
  CV, and research interests, a split Markdown editor for blog posts with
  paste-to-upload images, and a **Site Settings** panel.
- **Static + free to host** — GitHub Pages via GitHub Actions on push to `main`.

## Stack

- **Hugo (Extended)** — static site generator with native Sass compilation
- **Go templates** + **SCSS** (one partial per page/component) + **YAML** data files
- **Vanilla JS only** — filter tabs, mobile nav, image lightbox, theme toggle
- **GitHub Pages** via GitHub Actions (`hugo --minify`)

## Quick start

```bash
hugo server          # live-reload preview at http://localhost:1313/
hugo --minify        # production build into public/
```

Requires **Hugo Extended ≥ 0.146** (content adapters + native Sass). The theme uses
CSS relative-color syntax, so visitors need a 2023+ browser (Chrome 119, Safari 16.4,
Firefox 128).

## Make it yours

0. **Quick setup** — run `python init.py` once after cloning. It prompts for your
   name, affiliation, social links, palette, and Pages URL, then rewrites
   `hugo.toml` and `params.yaml` for you (no dependencies; comments and the
   language list are preserved). Prefer to edit by hand? Skip it and do step 1.
1. **Identity & structure** — `config/_default/hugo.toml`: set `baseURL`, `title`
   (your name), and the language list. `config/_default/params.yaml`: set
   `description`, `tagline`, social links, `palette`, and the `sections` toggles.
2. **Content** — replace the placeholder data in `data/<lang>/*.yml`
   (publications, news, cv, research_interests), the bio in `content/_index.md`,
   and the demo post in `content/blog/`. Swap `static/images/profile.svg` and
   `static/cv.pdf` for your own.
3. **Preview** with `hugo server`, then push to `main` to deploy.

### Configuration reference (`config/_default/params.yaml`)

| Key | Purpose |
|---|---|
| `description` | Affiliation line shown under your name |
| `tagline` | One-line summary on the home page |
| `faviconEmoji` | Emoji used as the favicon (default 🌲) |
| `profileImage` | Path under `static/` to your profile image |
| `email`, `googleScholar`, `github`, `linkedin` | Social links |
| `cvPdf` | Path under `static/` to your CV PDF |
| `palette` | `forest` · `slate` · `crimson` · `plum` (see `assets/scss/_theme.scss`) |
| `sections` | Per-section booleans: `research`, `publications`, `blog`, `news`, `cv` |

Per-language overrides for `description`/`tagline` go in
`config/_default/hugo.toml` under `[languages.<lang>.params]`.

### Adding a language

1. Add a `[languages.<lang>]` block in `config/_default/hugo.toml`.
2. Copy `i18n/en.toml` to `i18n/<lang>.toml` and translate the values.
3. Add `data/<lang>/*.yml` (copy from `data/en/`; keep `title` keys identical so
   slugs and cross-links stay stable, translate the prose).
4. Add `<name>.<lang>.md` content siblings (e.g. `_index.<lang>.md`) and a
   `_content.<lang>.gotmpl` for the publications and research-interests sections.
5. Update `LANGS` in `static/admin/admin.js` so the dashboard can edit the new
   language's content.

### Colors & theme

Palettes are defined in `assets/scss/_theme.scss` as sets of CSS custom properties.
The owner-selected `palette` sets `data-palette` on `<html>`; the visitor's light/dark
choice sets `data-theme`. Add a palette by adding a `[data-palette="name"]` block and
listing the name in `PALETTES` in `static/admin/admin.js`.

## The content dashboard (`/admin/`)

Two ways to edit content:

1. **Directly** — edit the Markdown/YAML and commit.
2. **Dashboard** — a zero-dependency Python backend that serves the editor and
   commits each save to your **local** git repo (push in bulk when ready):

   ```bash
   python cms-server.py     # then open http://localhost:8787/
   ```

   Use the **content-language selector** (top right) to edit each language's data and
   posts. The **Settings** tab edits `config/_default/params.yaml` (palette, sections,
   social links). The local server only accepts loopback requests.

   Each content editor has an **⤳ Auto-translate** button that fills the other
   languages from what you're editing, using the free, keyless [MyMemory](https://mymemory.translated.net)
   service (client-side; works locally and on Pages). It translates only prose —
   titles, authors, venues, URLs, and slugs stay fixed — and protects markdown.
   It only fills *missing* translations, so your hand-edits are never overwritten.
   Treat the output as a draft to review (conventional MT, not an LLM).

   When the dashboard is served from GitHub Pages instead, it falls back to committing
   through the GitHub API using a **fine-grained token** scoped to the repo
   (Contents: read/write). Click **Authorize with GitHub** on the login screen to open
   GitHub's token page pre-filled, then paste the token back. Owner/repo are detected
   from the Pages URL (override `OWNER`/`REPO` in `static/admin/admin.js` for custom
   domains). Use a short token expiration — the dashboard also self-expires the stored
   token after 2 days. The dashboard's palette, light/dark mode, and UI language are
   adjustable from its header.

## Project layout

```
config/_default/  hugo.toml (structural) + params.yaml (owner-editable)
content/          Markdown pages + posts; data-driven sections via _content.<lang>.gotmpl
data/<lang>/      Per-language structured content (publications, news, cv, interests)
i18n/             UI string bundles (en.toml, ko.toml, …)
layouts/          Go templates — shell, per-section views, partials, render hooks
assets/scss/      main.scss entry, _variables.scss, _theme.scss tokens, per-component partials
assets/js/        main.js (fingerprinted at build for cache-busting)
static/           Images, cv.pdf, and the /admin dashboard
```

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds with Hugo
Extended and publishes `public/` to GitHub Pages. Set `baseURL` in
`config/_default/hugo.toml` to your Pages URL first.

## Documentation

- [CHANGELOG.md](CHANGELOG.md) — notable changes
- [ROADMAP.md](ROADMAP.md) — direction and ideas

## License

[MIT](LICENSE). If you build something with it, an attribution link back to the
template is appreciated but not required.
