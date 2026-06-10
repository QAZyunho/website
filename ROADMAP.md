# Roadmap

High-level direction for the template. Notable changes live in
[CHANGELOG.md](CHANGELOG.md).

## Next up (next session)
Onboarding polish — make the template inviting at first glance:
- [ ] **Quickstart guide with friendly snapshots** — a short, visual "get running in
      5 minutes" walkthrough with screenshots of the site (light/dark, palettes) and
      the admin dashboard.
- [ ] **Beautiful introductory README** — a polished landing README with a hero
      screenshot/demo, a feature gallery, and a live-demo link; current README is
      functional but plain.

## Open threads
- Initial package not yet pushed. Local repo is on `main` with `origin` set to
  `https://github.com/2ood/hugo-academic-portfolio.git`; create the empty public repo
  on GitHub, then `git push -u origin main`. Deploy values kept as placeholders by
  choice (set `baseURL` + admin `OWNER`/`REPO` when going live).

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
