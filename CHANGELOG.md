# Changelog

## Unreleased

- Initial repo structure: `palm-oil/` and `paddy/` variants, each with
  `data/{raw,processed}`, `scripts/` (+ `scripts/notebook/`), and
  `results/{figures,tables}`. Added `README.md`, `CLAUDE.md`,
  `requirements.txt`, `.gitignore`.
- `paddy`: organized module outputs into per-module subfolders
  (`data/processed/module_{1,2,3,4}/`, `results/figures/module_{1,2,3,4}/`,
  `results/tables/module_{1,2,3,4}/`) and updated the four notebooks
  accordingly. Shared inputs produced by Module 1 (`Klasifikasi_Sawah.tif`
  / `.geojson`) stay flat in `data/processed/` since Modules 2-4 read them
  as a common dependency. Also fixed Module 2's
  `Grafik_TimeSeries_MultiMusim_CHIRPS.png` save path, which was writing
  to the notebook's working directory instead of `results/figures/`.
