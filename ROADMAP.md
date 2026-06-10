# Roadmap

High-level direction for the template. Notable changes live in
[CHANGELOG.md](CHANGELOG.md).

## Recently shipped (2026-06-10)
- **`init.py`** — one-command post-clone personalization (rewrites `hugo.toml` +
  `params.yaml` surgically). First piece of the onboarding-polish goal.
- **Dashboard upgrades** — "Authorize with GitHub" deep-link, site favicon, palette
  + light/dark theme, EN/KO UI translation, and labeled Display/Content selectors.
- **Cache-busting** — `main.js` moved to `assets/js/` and fingerprinted at build.
- **Themed demo persona** — *Joomo Makguli* makgeolli-research demo content (EN/KO).

## Next up (next session)
Onboarding polish — continue making the template inviting at first glance:
- [ ] **Quickstart guide with friendly snapshots** — a short, visual "get running in
      5 minutes" walkthrough with screenshots of the site (light/dark, palettes) and
      the admin dashboard. (`init.py` now covers the config step.)
- [ ] **Beautiful introductory README** — a polished landing README with a hero
      screenshot/demo, a feature gallery, and a live-demo link; current README is
      functional but plain.

## Open threads
- Live demo is deployed from this repo (`baseURL` → `makguli.github.io/jumorepo/`,
  themed demo persona). When packaging the template for reuse, reset `baseURL`,
  `params.yaml` identity, and `data/`+`content/` back to neutral placeholders (or
  document that `init.py` + the dashboard are the intended reset path).

## Ideas / possible improvements
- [ ] More built-in palettes, and a small palette preview in the Settings dashboard.
- [ ] Optional live palette preview / per-visitor palette override.
- [ ] Dashboard support for editing `config/_default/hugo.toml` (title, baseURL,
      language list) without hand-editing TOML.
- [ ] RSS/sitemap polish and per-language feeds.
- [ ] A scaffolding script (or `hugo new`) for adding a language end-to-end.

## Non-goals
- No hosted/third-party CMS, no JS framework, no Node/Tailwind/PostCSS pipeline.
- No database, accounts, or comments. The build is the Hugo binary alone.
