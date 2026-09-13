# BIMFabrikHH documentation

Source for the combined documentation site (Zensical) covering BIMFabrikHH Core, BIMFabrikHH API, and ifcfactory.

**Python:** 3.11 or 3.12 (aligned with ifcfactory; 3.13 is excluded until those packages support it).

## Local preview

Install core doc tooling **plus** editable [ifcfactory](https://github.com/LGV-BIM-Leitstelle/ifcfactory) from the
sibling folder `../ifcfactory` (same parent as this repo):

```bash
poetry install --with ifcfactory
poetry run zensical serve
```

The **ifcfactory → Overview** page pulls in the upstream [
`ifcfactory/README.md`](https://github.com/LGV-BIM-Leitstelle/ifcfactory)
via [pymdown Snippets](https://facelessuser.github.io/pymdown-extensions/extensions/snippets/) (`base_path = [".."]`,
snippet `ifcfactory/README.md`). That requires a **sibling** `ifcfactory` checkout next to this repo (same as the API
build).

If you only clone `BIMFabrikHH_docs`, add ifcfactory as
a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) or checkout next to this repo, then adjust
`paths` in `zensical.toml`, the snippet `base_path`, and the path in `[tool.poetry.group.ifcfactory.dependencies]` if
you use a different layout (e.g. `vendor/ifcfactory`).

Then open [http://localhost:8000](http://localhost:8000) (
see [Create your site](https://zensical.org/docs/create-your-site/)).

## Build

```bash
poetry run zensical build
```

Static output goes to `site/` (ignored by git). Adjust `site_url` in `zensical.toml` when publishing.

## CI

GitHub Actions (`.github/workflows/docs.yml`) runs only when you start it by hand
(**Actions → Docs → Run workflow**). It checks out this repo
and [ifcfactory](https://github.com/LGV-BIM-Leitstelle/ifcfactory) as **siblings**, then runs
`poetry install --with ifcfactory` and `zensical build` and publishes `site/` to
[GitHub Pages](https://lgv-bim-leitstelle.github.io/BIMFabrikHH_docs/). In the repository settings, set **Pages →
Source** to **GitHub Actions**.
