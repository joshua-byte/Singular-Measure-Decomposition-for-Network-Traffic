# Measure-Based Anomaly Detection

A resolution-dependent anomaly detection framework inspired by measure
decomposition and the Dirac delta distribution.

This project models network traffic as the sum of:

-   An absolutely continuous background field
-   A singular atomic event measure
-   A resolution-controlled extraction process

Instead of treating anomalies as arbitrary outliers, this approach
interprets them as singular contributions relative to observational
scale.

------------------------------------------------------------------------

## Mathematical Interpretation

We treat traffic x(t) as a finite measure:

x(t) = f(t) dt + sum_i a_i δ(t - t_i)

Where:

-   f(t) → continuous background (robust rolling median)
-   δ(t - t_i) → singular event support
-   a_i → event mass (normalized deviation)

An event is defined relative to:

-   Background window (coarse-graining scale)
-   Threshold parameter K
-   Event separation window

------------------------------------------------------------------------

## Pipeline

### 1. Robust Background (Absolutely Continuous Component)

-   Rolling median
-   Rolling MAD (Median Absolute Deviation)
-   Gaussian-consistent scaling (1.4826 factor)

Ensures robustness under heavy-tailed bursts and contamination.

------------------------------------------------------------------------

### 2. Deviation Field

z(t) = (x(t) - μ(t)) / σ(t)

Singular support condition:

\|z(t)\| \> K

------------------------------------------------------------------------

### 3. Singular Measure Extraction

For each contiguous support region:

-   Compute event mass via local integration
-   Collapse region to a single impulse at maximal deviation
-   Enforce minimum separation between impulses

Result: a sparse atomic measure representing structural anomalies.

## License

MIT License
