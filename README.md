# P06 — Arrhenius or Super-Arrhenius Relaxation in a 3D Soft-Sphere Glass-Former

**A Bayesian Model Comparison**

This project was developed for the course **Advanced Statistics for Physics Analysis (ASPA)**, as part of a series of applied Bayesian statistics projects connecting statistical inference methods to open questions in physics.

## Overview

Supercooled liquids show a dramatic slowdown in structural relaxation as temperature decreases. Whether this slowdown follows a simple **Arrhenius law** (constant activation energy) or a **super-Arrhenius / Vogel–Fulcher–Tammann (VFT) law** (temperature-dependent, diverging activation energy) is a long-standing open question in the physics of glasses and disordered systems.

This project addresses that question as a **formal Bayesian model comparison** problem, rather than by visual curve inspection, using relaxation-time data from molecular simulations of a three-dimensional polydisperse soft-sphere glass-former, obtained under two different Monte Carlo dynamics (standard Metropolis and the accelerated, irreversible **kSwap** algorithm).

## What was done

- Fitted both the **Arrhenius** and **VFT** models to $\log\tau$ vs. $1/T$ under a Gaussian likelihood that propagates the reported measurement uncertainty (via the delta method) and infers an additional intrinsic scatter term $\sigma_{\text{int}}$.
- Sampled both models with **Hamiltonian Monte Carlo (NUTS)** using **Stan**, with full posterior diagnostics (trace plots, $\hat R$, effective sample size, divergence checks, parameter correlations).
- Compared models formally via **leave-one-out cross-validation (LOO-CV / PSIS)**, rather than relying on unpenalized in-sample fit.
- Validated both models with **posterior predictive checks** (density overlays, pointwise intervals, empirical coverage, Bayesian p-values) and **standardized residual analysis**.
- Derived and estimated physically interpretable quantities beyond the raw model comparison: the **effective activation energy** $E_{\text{eff}}(T)$ and the **fragility index** $m$, with full posterior uncertainty propagation (not plug-in point estimates).
- Extrapolated predictions of $\tau$ below the observed temperature range, with an explicit check of extrapolation stability near the VFT divergence temperature $T_0$.

## Key result

Across both Monte Carlo dynamics, the evidence — from intrinsic scatter, residual structure, LOO-CV, and predictive calibration — consistently favors the **VFT (super-Arrhenius)** model over the Arrhenius model, with the strength of evidence quantified explicitly rather than assumed.

## Tech stack

- **R** with **Stan** (via `rstan`) for Bayesian inference (NUTS sampler)
- `loo` for model comparison (PSIS-LOO)
- `bayesplot`, `ggplot2`, `patchwork` for diagnostics and visualization
- `moments` for posterior skewness quantification

## Repository contents

- `p06_aspa.pdf` — full write-up: theoretical background, model specification, mathematical derivations, results, and discussion
- `p06_statistics_final.ipynb` — complete R/Stan analysis notebook (data processing, model fitting, diagnostics, figures)
- Dataset: r3d_Relaxation_Time.csv data from Nishikawa, Ghimenti, Berthier & van Wijland, *"Irreversible swap algorithms for soft sphere glasses"*, Phys. Rev. E **111**, 045416 (2025)

## Authors

Melissa D. de Almeida Nespeque
