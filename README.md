# Projected Gradient and Frank-Wolfe Variants for Portfolio Optimization

> **GitHub repository description:** A benchmark of projected-gradient and Frank-Wolfe variants for constrained mean-variance portfolio optimization on five real equity universes.

This project studies first-order optimization methods for the long-only Markowitz mean-variance portfolio problem. It compares projection-based and projection-free methods on real equity datasets, evaluating convergence, computational cost, and the sparsity of the resulting portfolio allocations.

Developed for the *Optimization for Data Science* course in the MSc in Data Science at the University of Padova.

## Problem formulation

Given expected asset returns \(\bar r\), a covariance matrix \(\Sigma\), and risk-aversion parameter \(\eta\), the portfolio weights \(x\) are found by solving:

\[
\min_x \quad \eta x^\top \Sigma x - \bar r^\top x
\]

subject to a fully invested, long-only portfolio:

\[
\sum_i x_i = 1, \qquad x_i \geq 0.
\]

## Methods compared

- Projected Gradient Descent (PGD)
- Frank-Wolfe / Conditional Gradient (FW)
- Away-step Frank-Wolfe (AFW)
- Pairwise Frank-Wolfe (PFW)

The methods were evaluated using exact line search and, where applicable, diminishing or fixed step-size rules. Simplex projection methods were also compared as part of the PGD implementation.

## Data

The empirical analysis uses daily adjusted equity prices from 6 October 2006 to 24 February 2023 for five market universes:

- FTSE 100
- EURO STOXX 50
- Dow Jones Industrial Average
- S&P 500
- NASDAQ 100

Simple returns were used to estimate expected returns and sample covariance matrices. The S&P 500 universe, with 420 assets in the dataset, provided the most ill-conditioned and computationally challenging setting.

## Evaluation

The algorithms were benchmarked on:

- Objective-value convergence and optimality certificates
- Number of iterations to convergence
- CPU time
- Sensitivity to the conditioning and dimension of the market universe
- Sparsity of final portfolio allocations

## Key findings

- **PFW and AFW with exact line search** consistently achieved the best overall performance, combining fast convergence, low computational cost, and sparse portfolios.
- Classical **Frank-Wolfe with exact line search** performed well on smaller, better-conditioned datasets but was slower on harder problems.
- **Diminishing step-size** Frank-Wolfe variants showed sublinear convergence and visible zig-zagging behaviour.
- **PGD** was less competitive, particularly for larger or ill-conditioned datasets, because repeated projections increased runtime and it did not reach the pre-specified tolerance in the experiments.
- For simplex projection, **Condat's algorithm** was faster than the Duchi-based alternative while producing the same feasible projection.

## Repository contents

```text
ODS_PROJECT_REPORT_GROUP11_PORTFOLIO.pdf   Full methodology, experiments, figures, and references
README.md                                  Project overview (this file)
```

## Code and data availability

The implementation notebook and source datasets are intentionally **not included** in this public repository. This repository is intended as a portfolio record of the methodology and results; the full report provides the mathematical formulation, experimental design, and findings. The code is available upon request.

## Authors

- Giorgia Bonin
- Emanuele Cavaliero
- Francesco Ceron

## Academic context

University of Padova, Department of Mathematics "Tullio Levi-Civita"  
MSc in Data Science, Academic Year 2024/2025  
Course: Optimization for Data Science

## License

No license has been specified. Add a license file before allowing reuse of the report or other project materials.
