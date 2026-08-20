# C2VSimFG — tracked modifications

Git repository tracking proposed corrections and refinements to DWR's **C2VSimFG** IWFM model
(**C2VSimFG 1.5**, WY1974-2021, IWFM 2024.2.1594; DWR Version 1.5).

The base commit (tag `C2VSimFG_1.5`) is the unmodified DWR release. Every later commit is **exactly one
suggested change**, tagged `C2VSimFG_1.5+cbN`, so a reviewer can inspect each as a single diff and
accept or reject items individually. See **CHANGES.md** for the tag → change map and the review recipe.

## Layout

| path | contents |
|---|---|
| `C2VSimFG/` | the model (Preprocessor, Simulation, Budget, ZBudget, gis) — as released by DWR plus committed changes |
| `Log.txt` | DWR-style version log; one row per commit (`Version,Time,Date,IWFM_version,comment`) |
| `CHANGES.md` | tag → one-line description → files touched → depends-on → status |

Not tracked (see `.gitignore`): `C2VSimFG/bin/` (IWFM executables — obtain the version named in
Log.txt from DWR), `C2VSimFG/Excel/` (post-processing workbooks), `C2VSimFG/Results/`,
`*.out`, `*.hdf`, `*.bud` (model outputs). Copy the required IWFM executables into
`C2VSimFG/bin/` to run the model: the base release and changes cb1-cb4 run with IWFM 2024.2.1594
(from the DWR release); change cb5 onward runs with IWFM-2025.0.1747 (DWR IWFM download) in
`C2VSimFG/bin/IWFM-2025.0.1747/` - the Log.txt IWFM_version column records which engine each
version uses.

Files over 100 MB (crop/native/urban area time series, precipitation, DelivArea/RchgArea .dbf) are stored
with **Git LFS** — run `git lfs install` before cloning so they check out as real files, not pointers.

## Running

From `C2VSimFG/`: `Simulation\RUN_SIMULATION_PLL.bat` (simulation; preprocessor output `C2VSimFG_PreprocessorOut.bin` is included), then `Budget\Run_Budget.bat`, `Zbudget\ZBudget.bat`. A full run takes about 2.5 hours with the parallel executable. Outputs go to `Results/`.

## Conventions

- Version string: DWR version + `+cbN` (N = change number); the same string names the git tag
  (spaces replaced by `_`).
- Each change commit touches only the model files needed for that change plus `Log.txt` and
  `CHANGES.md`; commit body follows Issue / Resolution / Files & parameters / Result / Re-calibration.
- Every committed change was run to completion cumulatively on top of the previous commits.
- Line endings are never converted (`.gitattributes: * -text`) — IWFM inputs stay byte-exact.

Charles Brush, Hydrolytics LLC.
