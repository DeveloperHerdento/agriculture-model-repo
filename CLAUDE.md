# CLAUDE.md

Code rules for this repo. Follow these over generic defaults.

## Project state (read this first)

Two independent commodity variants: `palm-oil/` and `paddy/`. They do not
share code or data — treat them as separate pipelines that happen to live
in one repo. Don't add cross-variant abstractions/shared utils unless
asked.

## Folder layout

```
<variant>/data/raw/         Original source data — never modify in place
<variant>/data/processed/   Derived/cleaned data produced by scripts
<variant>/scripts/          Python ETL / model scripts (*.py)
<variant>/scripts/notebook/ Exploratory Jupyter notebooks (*.ipynb)
<variant>/results/figures/  Plots, maps, charts
<variant>/results/tables/   Output tables, model metrics
docs/                       Cross-variant docs
```

- Scripts resolve data paths relative to their own file location
  (`os.path.dirname(__file__)`), not the current working directory.
- Never overwrite raw input files in place. Derived output goes to
  `data/processed/` (or gets a new suffix) instead of mutating input.
- `data/raw/`, `data/processed/`, and `results/` are git-ignored — only
  `.gitkeep` tracks the empty folders. Don't fight the `.gitignore` to
  force-add generated data/results unless the user explicitly asks.

## Conventions

- Keep each variant's scripts plain and dependency-light; don't introduce
  a framework or package structure for what is still a handful of
  standalone scripts.
- Match whatever comment/print-message language already exists in a
  variant's scripts when editing them, rather than switching mid-file.

## Docs

- Update `CHANGELOG.md` for any user-visible or structural change.
