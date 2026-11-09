# Experimental reproducibility

**Study:** A hybrid deep learning framework for global irradiance prediction using fuzzy C-Means, CNN-WNN, and Informer models  
**DOI:** https://doi.org/10.1016/j.clet.2025.101061

## Scope of implementation

The code combines fuzzy memberships, convolutional and wavelet-oriented processing, and a sparse attention layer for irradiance forecasting.

The current attention module is a sampled-key sparse prototype, rather than a verified full ProbSparse Informer implementation. Verify the precise architecture, data partitions and selected climatological features before comparing results.

## Data handling and evaluation

Measured data are supplied as an external time-ordered CSV rather than packaged with the source code. Normalization statistics and fuzzy-regime parameters, where used, must be fitted on training observations only. Input windows must not include future target values.

The default training workflow uses chronological partitions for model development, residual calibration (when applicable), validation and final evaluation. Multiple cities, sites, meteorological regimes or horizons need separately documented holdout protocols; a successful single-series run is not evidence of generalization.

## Reporting requirements

A repeatable experiment records the source dataset and its license, feature definitions, sampling period, target units, forecast horizon, random seeds, optimizer budget, train/test boundaries and all metric definitions. The software check `python train.py --smoke` uses simulated signals and serves only to validate execution.

Paper-level numerical agreement has not been independently established. The results of new runs should be reported as new experiments, with explicit comparison settings rather than attributed to the published results.
