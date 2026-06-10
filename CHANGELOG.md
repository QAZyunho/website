# Changelog

All notable changes to this template are documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com).

## [1.0.0] — Initial template release

The portfolio, generalized into a reusable Hugo template.

### Added
- **Multilingual support** — Hugo `[languages]` (English default + Korean demo),
  UI strings in `i18n/*.toml`, per-language content (`.<lang>.md`) and data
  (`data/<lang>/`), and a header language dropdown.
- **Owner configuration** in `config/_default/params.yaml` — identity, social links,
  color palette, and per-section enable toggles (gating nav tabs and home sections).
- **Color palettes + light/dark mode** — named palettes (forest/slate/crimson/plum)
  and a visitor light/dark toggle, both via CSS custom properties; the owner palette
  is set from config, the theme choice persists per browser with no flash on load.
- **Site Settings dashboard** — the `/admin/` content editor gained a Settings panel
  (edits `params.yaml`) and a content-language selector for per-language editing.
- **MIT license** and template documentation.

### Notes
- Theming uses CSS relative-color syntax (2023+ browsers).
- Ships with neutral placeholder content (a demo persona) so it builds complete.
