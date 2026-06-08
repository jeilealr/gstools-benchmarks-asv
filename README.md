# gstools-benchmarks-asv

Cumulative OpenMP benchmark history for [GSTools](https://github.com/jeilealr/GSTools),
generated automatically by CI on every accepted commit to `main`.

## Live reports

| Report | Description |
|--------|-------------|
| [Case/backend comparison](https://jeilealr.github.io/gstools-benchmarks-asv/) | Interactive chart — latest 50 commits, Cython vs Rust side by side |
| [Native ASV history](https://jeilealr.github.io/gstools-benchmarks-asv/asv/) | Full commit-over-commit trend plots from Airspeed Velocity |

## What is measured

Three representative two-point statistics workflows are benchmarked, each with
both GSTools backends and with 1, 2, 4, and 8 OpenMP threads:

| Family | Cases |
|--------|-------|
| Variogram estimation | full 900 pts · sampled 5 000→1 500 · sampled 15 000→4 500 |
| Global kriging | 30×500 · 120×2 000 · 360×6 000 (cond pts × target pts) |
| Random field generation | unstructured RandMeth · structured RandMeth · Fourier · CondSRF |

Both runtime (`time_`) and peak memory (`peakmem_`) are recorded.

## Backends

| Label | Description |
|-------|-------------|
| `cython_fallback` | Default Cython backend from [gstools-cython](https://github.com/GeoStat-Framework/GSTools-Cython) |
| `rust_core` | Rust backend from [gstools-core](https://github.com/GeoStat-Framework/GSTools-Core) |

Speedup is defined as:

```
speedup = cython_fallback_time / rust_core_time
```

A value greater than `1.0` means the Rust backend was faster on the same
machine, commit, case, and thread count.

## Repository layout

```
/               Interactive case/backend comparison (latest 50 commits)
/asv/           Native ASV benchmark website (full history)
/results/       Raw ASV result JSON files (one file per benchmarked commit)
```

The raw JSON files follow the [ASV result format](https://asv.readthedocs.io/en/stable/index.html)
and can be loaded locally with any ASV installation.

## Runner hardware

Results are produced on `ubuntu-latest` GitHub-hosted runners. The machine
summary card in the interactive report shows the exact CPU, core count, and RAM
recorded for each run. GitHub may update the underlying hardware over time; use
the machine metadata when comparing absolute numbers across distant commits.

## Benchmark source

The benchmark suite, ASV configuration, and tooling live in the
[`benchmarks/`](https://github.com/jeilealr/GSTools/tree/main/benchmarks)
directory of the GSTools repository.
