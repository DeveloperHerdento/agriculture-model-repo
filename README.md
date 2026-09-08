# agriculture-python-model

Python data/model pipelines for agriculture commodity monitoring. Two
independent variants live side by side in this repo:

- **`palm-oil/`** — palm oil (kelapa sawit) model
- **`paddy/`** — paddy/rice (padi) model

Each variant is self-contained (own data, scripts, results) and can be
worked on independently — they don't share code or datasets.

## Folder layout

```
<variant>/
  data/
    raw/          Original source data, never modified in place
    processed/    Derived/cleaned data produced by scripts
  scripts/        Python ETL / model scripts (*.py)
  scripts/notebook/  Exploratory Jupyter notebooks (*.ipynb)
  results/
    figures/       Plots, maps, charts
    tables/        Output tables (csv/xlsx/etc), model metrics
docs/             Cross-variant docs (setup notes, data dictionaries, etc)
```

`data/raw`, `data/processed`, and `results/` are git-ignored (data and
generated output aren't versioned — only `.gitkeep` placeholders are
tracked so the folders exist). Scripts should resolve paths relative to
their own file location (`os.path.dirname(__file__)`), not the current
working directory, so they run correctly regardless of where they're
invoked from.

## Setup

```bash
pip install -r requirements.txt
```

Requires Python 3.10+.

## Usage

Each variant's `scripts/` folder holds its own ETL/model pipeline —
add a short usage section per variant here as scripts are built out
(e.g. `python palm-oil/scripts/<step>.py`).

## Conventions

See `CLAUDE.md` for the full set of repo rules (data-path handling,
naming, when to update `CHANGELOG.md`, etc).
