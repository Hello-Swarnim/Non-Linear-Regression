# Non-Linear Regression — Model Fitting & Statistical Diagnostics

Fits and statistically compares three candidate models — an **exponential sum**, a **rational function**, and a **degree-4 polynomial** — to a supplied 60-point dataset `(tᵢ, yᵢ)`, for **MTH686**, IIT Kanpur.

For each model, parameters are estimated via nonlinear/linear least squares, residuals are checked for normality, and 95% confidence intervals are derived from the Fisher Information Matrix (FIM) — then the three models are compared to pick the best fit.

## What's here

- **[`report.pdf`](report.pdf)** — full write-up: model derivations, parameter estimates, FIM/CI tables, residual diagnostics, and the final model comparison.
- **[`Appendix.pdf`](Appendix.pdf)** — supplementary material.
- **[`MTH686_Project.ipynb`](MTH686_Project.ipynb)** — all code: data loading, model fitting, diagnostic plots, and FIM/CI computation.
- **[`set-49.dat`](set-49.dat)** — the dataset (`t`, `y`) pairs, `1 ≤ t ≤ 60`.

## Models fit

| Model | Form | Method |
|---|---|---|
| **1. Exponential sum** | `y(t) = α₀ + α₁e^(β₁t) + α₂e^(β₂t)` | Osborne's method |
| **2. Rational function** | `y(t) = α₀ + α₁t / (1 + β₁t)` | Levenberg–Marquardt (damped Gauss–Newton) |
| **3. Polynomial (degree 4)** | `y(t) = β₀ + β₁t + β₂t² + β₃t³ + β₄t⁴` | Ordinary least squares |

For each model, the notebook:
1. Fits the parameters and plots the fitted curve against the data.
2. Checks residual normality via **histograms** and **QQ plots**, and formally via **Shapiro–Wilk** and **Jarque–Bera** tests.
3. Plots residuals vs. `t` to check for structure/heteroscedasticity.
4. Computes the **Fisher Information Matrix** and derives 95% confidence intervals for each parameter, using `β̂ⱼ ± t_(α/2, n−p) · SE(β̂ⱼ)`.

## Results

| Model | σ̂² | R² | Shapiro–Wilk p | Jarque–Bera p |
|---|---|---|---|---|
| **Exponential** | **0.0232** | **0.836** | 0.204 | 0.392 |
| Rational | 0.0265 | 0.797 | 0.152 | 0.401 |
| Polynomial (deg 4) | 0.0335 | 0.753 | 0.720 | 0.976 |

**The exponential model gives the best overall fit** — lowest residual variance and highest R², with residuals that are still reasonably close to normal. The polynomial model has the highest normality p-values but overfits local fluctuations, at the cost of worse R² and residual variance; the rational model falls in between.

## Running it

```bash
pip install numpy scipy pandas matplotlib
jupyter notebook MTH686_Project.ipynb
```

The notebook reads `set-49.dat` directly (data is also hardcoded inline in an early cell) — run cells sequentially, model by model, to reproduce each fit, diagnostic plot, and confidence interval table.

## Author

Swarnim Verma — Department of Mathematics and Scientific Computing, IIT Kanpur (MTH686 course project).
