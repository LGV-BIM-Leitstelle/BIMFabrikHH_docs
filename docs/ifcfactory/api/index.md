# API reference

These pages document the **public** ifcfactory surface: the package root re-exports and the main modules **`element`**,
**`primitives`**, and **`operations`**. Internal paths under `_internal` are not listed here so refactors there are less
likely to break the docs.

Build locally with `poetry install --with ifcfactory` then `poetry run zensical build` (see repository `README.md`).

## Sections

- [Package (`ifcfactory`)](package.md) — top-level exports and module docstring
- [`ifcfactory.element`](element.md) — `BIMFactoryElement`
- [`ifcfactory.primitives`](primitives.md) — profiles and solid primitives
- [`ifcfactory.operations`](operations.md) — `Transform`, `Boolean`, etc.
