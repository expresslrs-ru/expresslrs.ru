# Repository Guidelines

## Project Structure & Module Organization

This repository hosts the Russian ExpressLRS documentation site. Main content lives in `docs/` as Markdown pages grouped by topic: `docs/hardware/`, `docs/software/`, `docs/Manuals/`, `docs/Info/`, `docs/HdZero/`, and `docs/index/`. Site navigation, theme settings, plugins, and external scripts are configured in `mkdocs.yml`. Static assets belong under `docs/assets/` when used by MkDocs; root-level files such as `CNAME`, `favicon.ico`, `_config.yml`, `_layouts/`, and `img/` are legacy or hosting-related support files. GitHub Actions deployment is defined in `.github/workflows/ci.yml`.

## Build, Test, and Development Commands

- `pip install mkdocs-material pillow cairosvg` installs the same core dependencies used by CI.
- `mkdocs serve` runs a local preview site with live reload.
- `mkdocs build` validates the documentation build and catches many broken configuration or navigation issues.
- `mkdocs gh-deploy --force` publishes to GitHub Pages; use this only when intentionally deploying.

Run commands from the repository root. If using the included `venv/`, activate it first.

## Coding Style & Naming Conventions

Write documentation in Markdown with short sections, clear Russian headings, and practical examples. Keep filenames lowercase where possible and avoid spaces in new paths; existing paths with spaces should not be renamed casually because `mkdocs.yml` may reference them. Use relative links for internal pages and keep every new page registered in the `nav:` section when it should appear in the site menu.

For YAML, use two-space indentation and preserve the existing MkDocs style. Avoid unrelated formatting churn in `mkdocs.yml`.

## Testing Guidelines

There is no unit test suite. Treat `mkdocs build` as the required validation before opening a pull request. For visual or navigation changes, also run `mkdocs serve` and click through the affected pages. Confirm referenced images, scripts, and internal links resolve correctly.

## Commit & Pull Request Guidelines

Recent commits use short, direct messages such as `fix info md`, `Update mkdocs.yml`, and `add lua_expl.md, fix info md`. Follow that style: concise, imperative, and focused on the changed content.

Pull requests should include a brief summary, list affected pages or sections, and mention whether `mkdocs build` passed. Add screenshots only for layout, theme, image, or navigation changes. Link related issues or discussions when applicable.

## Security & Configuration Tips

Do not commit generated site output, credentials, or machine-specific files. Keep `.DS_Store` and virtual environment changes out of future commits. Be careful with `mkdocs gh-deploy --force`, since it overwrites the published Pages branch.
