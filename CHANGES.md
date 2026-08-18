# C2VSimFG — change register

Base: **C2VSimFG 1.5** (DWR Version 1.5), tag `C2VSimFG_1.5`. Each row below is one commit / one tag / one
suggested change. Status: *proposed* until reviewed; reviewers mark *accepted* / *rejected*.

| tag | Log.txt version | change (one line) | files touched | depends on | status |
|---|---|---|---|---|---|
| `C2VSimFG_1.5` | C2VSimFG 1.5 | DWR Version 1.5 (unmodified base) | — | — | base |
| `C2VSimFG_1.5+cb1` | C2VSimFG 1.5+cb1 | Race condition: delivery adjustment - KOPTDV 11 to 10 (adjust GW pumping only; SW diversions are observed data) | Simulation/C2VSimFG.in (KOPTDV) | — | proposed |
| `C2VSimFG_1.5+cb2` | C2VSimFG 1.5+cb2 | Race condition: multiple stream nodes sharing a GW node - CSTRM=0 at 83 confluence reach-end nodes (only the receiving node exchanges with the aquifer) | Simulation/Streams/C2VSimFG_Streams.dat (Stream Bed Parameters, CSTRM) | — | proposed |

## How to review one change

```sh
git tag -n                              # list all changes with their one-line messages
git diff C2VSimFG_1.5+cb2 C2VSimFG_1.5+cb3 --stat   # files touched by change 3
git diff C2VSimFG_1.5+cb2 C2VSimFG_1.5+cb3          # the exact edit
git show C2VSimFG_1.5+cb3                     # commit message (issue / resolution / result) + diff
```

## How to accept only some changes

Start from the base and cherry-pick the accepted tags in order:

```sh
git checkout -b accepted C2VSimFG_1.5
git cherry-pick C2VSimFG_1.5+cb1 C2VSimFG_1.5+cb3 C2VSimFG_1.5+cb4
```

Model files are kept independent between changes (each change edits its own files/sections), so
picks apply cleanly. `Log.txt` and `CHANGES.md` are appended by every change and will report a
trivial conflict when a change is skipped — keep both sides' rows and `git cherry-pick --continue`.
Where a change genuinely builds on another, the *depends on* column says so; pick the dependency first.
