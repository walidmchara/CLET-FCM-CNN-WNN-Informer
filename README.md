# FCM–CNN–WNN–Informer for Solar Irradiance

**Publication:** A hybrid deep learning framework for global irradiance prediction using fuzzy C-Means, CNN-WNN, and Informer models  
**Journal:** Cleaner Engineering and Technology (2025)  
**DOI:** https://doi.org/10.1016/j.clet.2025.101061

## Method

Fuzzy C-means estimates soft atmospheric-regime memberships. Convolutional filters summarize local meteorological patterns, wavelet-oriented features represent variability across scales, and an Informer-style attention block captures temporal dependencies.

The project includes chronological data preparation, model fitting, optional hyperparameter selection, evaluation metrics and graphical diagnostics. The architecture family and training parameters are configured in [config.json](config.json).

## Input data

The training script accepts a time-ordered multivariate CSV with a numeric `target` column. The target in this study is **global horizontal irradiance**. Dataset columns and evaluation assumptions are discussed in [data/README.md](data/README.md). Source data must be obtained from the study's experimental dataset and should be kept distinct from the synthetic software check.

## Installation and execution

```bash
python -m venv .venv
pip install -r requirements.txt
pytest -q
python train.py --smoke --epochs 2 --out outputs/smoke
```

With measured time-series data:

```bash
python train.py --csv path/to/measurements.csv --target target --time-col time --epochs 40 --out outputs/experiment
```

The program saves training history, test predictions, error metrics, and a fitted checkpoint under the chosen output directory. Optional parameter search is supported through `--search paper --trials N`, subject to the method-specific qualifications below.

## Evaluation notes

The current attention block uses a sampled-key sparse approximation. A full ProbSparse Informer encoder–decoder and the published experimental settings must be validated independently before direct benchmarking.

The test interval is chronological. Normalization statistics must be estimated on training data, and all reported comparisons should specify the time span, forecast horizon, seed, target units and metric definitions. [REPRODUCIBILITY.md](REPRODUCIBILITY.md) records the implementation boundaries and outstanding experimental checks.
