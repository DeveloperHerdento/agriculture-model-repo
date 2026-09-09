# agriculture-python-model

Python data/model pipelines for agriculture commodity monitoring in
Indonesia. Two independent variants live side by side in this repo:

- **`palm-oil/`** — palm oil (kelapa sawit) model
- **`paddy/`** — paddy/rice (padi) model: field extraction, growth-phase
  classification, vegetation-health/drought analysis, and productivity
  estimation (LUE + WOFOST)

> **Project status:** `paddy/` currently has four exploratory notebooks
> covering the full pipeline (Modules 1-4, see below); `palm-oil/` is
> scaffolded but has no scripts/notebooks yet. Nothing here is packaged
> as a reusable library or service — each variant is a handful of
> standalone scripts/notebooks. See `CLAUDE.md` for the full set of repo
> conventions.

## Data flow (`paddy/`)

```
Module 1: PaddyFieldExtraction
  Satellite imagery ──▶ classification ──▶ accuracy assessment
                                │
                                ▼
                  Klasifikasi_Sawah.tif / .geojson
                  (shared paddy-field mask, read by Modules 2-4)
                                │
        ┌───────────────────────┼───────────────────────┐
        ▼                       ▼                       ▼
Module 2: GrowthPhase   Module 3: Health         Module 4: Productivity
  GEE time-series          Vegetation indices       LUE constant-productivity
  growth-phase              VHI + drought              WOFOST potential
  classification            analysis                   productivity
        │                       │                       │
        ▼                       ▼                       ▼
   results/tables/         results/tables/         results/tables/
   figures/module_2/       figures/module_3/       figures/module_4/
```

Module 1's output (`Klasifikasi_Sawah.tif` / `.geojson`) is a shared
dependency read by Modules 2-4, so it stays flat in `data/processed/`
while everything else is organized per module.

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

### Paddy (`paddy/scripts/notebook/`)

Run the notebooks in order — each later module depends on Module 1's
output:

1. `Module_1_PaddyFieldExtraction.ipynb` — extracts the paddy-field mask
   and runs accuracy assessment
2. `Module_2_PaddyGrowthPhase.ipynb` — classifies growth phase from GEE
   time series
3. `Module_3_Health.ipynb` — vegetation indices, VHI, and drought
   analysis
4. `Module_4_Productivity.ipynb` — LUE constant and WOFOST potential
   productivity estimates

### Palm oil (`palm-oil/scripts/`)

Not built out yet — add a usage section here as scripts land (e.g.
`python palm-oil/scripts/<step>.py`).

## Conventions

See `CLAUDE.md` for the full set of repo rules (data-path handling,
naming, when to update `CHANGELOG.md`, etc).
