# Nonlocal thermal-response limits and dose compensability in parallel laser writing on Sb₂S₃ phase-change films

Simulation and analysis code for the manuscript:

> Z. Wang, W. Xia and X. Ma, *Nonlocal thermal-response limits and dose compensability in
> parallel laser writing on Sb₂S₃ phase-change films*.

Parallel direct laser writing couples optical parallelism to array-scale heat accumulation.
This repository contains the axisymmetric transient thermal solver, the array-level
superposition kernel, the non-negative dose-inversion analysis and the numerical
validation scripts used in the paper. Figure-generation scripts are not included here.

## Key results

- A nonlocal crosstalk factor **G** quantifies centre-pixel overheating; for a 100 nm
  Sb₂S₃ film (20 µs dwell, 11 × 11 array, 1 µm pitch) G = 3.49 on silica, 1.36 on
  sapphire and 1.07 on silicon.
- Non-negative dose inversion (**Kq = 1**) equalizes array temperature and reduces the
  normalized absorbed power by 64%, but the centre self-share falls from 0.287 to 0.248.
- Under fixed uniform illumination, single-pixel contrast is bounded exactly by **1/G**;
  temperature errors are dose-compensable, whereas contrast losses require pitch, delay
  or withheld-block margins.

## Repository layout

```
code/     thermal model, dose-inversion and validation scripts
data/     raw numerical records (convergence, validation, scans) in JSON
```

Main entry points in `code/`:

| Script | Purpose |
|---|---|
| `parallel_thermal_scan.py` | axisymmetric transient finite-volume single-spot solver |
| `seq_model.py` | sequential/raster writing model (time-shifted responses, G_sequential) |
| `analytic_model.py` | analytic/auxiliary model helpers |
| `independent_3d_validation.py` | independent fully implicit 3D multi-source validation |
| `timestep_convergence.py`, `raster_time_convergence.py`, `convergence.py` | mesh / time-step convergence |
| `conductivity_robustness.py`, `sensitivity.py`, `nonlinear_boundary.py` | parameter robustness scans |
| `pattern_limit.py`, `dose_inverse.py`, `inverse_kernel.py`, `order_scan.py`, `bisection_speed.py`, `scale_inf.py`, `same_instant_validation.py` | pattern contrast bounds, dose inversion, kernel and scaling analyses |

## Quickstart

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Every script is standalone, e.g.:

```bash
python code/timestep_convergence.py          # time-step convergence study
python code/independent_3d_validation.py     # independent 3D validation
python code/sensitivity.py                   # ±30% parameter sensitivity
```

## Requirements

Python 3.10+ with `numpy` and `scipy` (see `requirements.txt`).

## Citation

If you use this code, please cite the manuscript above. The numerical records in `data/`
correspond to the values reported in the paper and its supplementary information.

## License

MIT License — see [LICENSE](LICENSE).