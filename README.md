# Structural Credit Modeling  
**Black–Scholes Applied to Corporate Liabilities**


1. Implemented a baseline structural credit model (Merton, 1974) in which a firm's equity is modeled as a call option on its assets.
2. Calibrated unobservable firm asset value and asset volatility using observable equity prices, equity volatility, debt, and risk-free rates.
3. Applied the model to real firms and identifed systematic weaknesses in its behavior.
4. Implement **time-series smoothing step applied to the model-implied default probabilities (PDs)**.
5. Demonstrated the improved model performs better than the baseline under a clearly defined evaluation criterion.
6. Documented assumptions, methodology, results, and limitations in a concise technical report provided in `report/`


### Improvement Implemented

The chosen, minimal improvement is a time-series smoothing step applied to the model-implied default probabilities (PDs). Concretely:

- Location: `improved/__main__.py` (the improved pipeline) computes raw PDs using the baseline calibration and then applies exponential smoothing to produce `PD_smoothed`.
- Parameter: the smoothing intensity is controlled by the variable `SMOOTHING_ALPHA` in `improved/__main__.py` (default shown in the script and used for report is `0.1`). You can change this value in the file to test different smoothing strengths.
- Output: the improved pipeline writes `outputs/improved_model_results.csv` with both the raw PD (`PD_raw`) and the smoothed PD (`PD_smoothed`) columns.

## Quick run (minimal)

Follow these steps to run the baseline and improved pipelines quickly. These commands assume you are in the repository root and have `conda` or `python` available.

1. Create and activate a Python environment and install dependencies:

```bash
conda create -n quant_takehome python=3.9 -y
conda activate quant_takehome
pip install -r requirements.txt
```

2. Run the baseline starter pipeline:

```bash
python -m naive_model
```

3. Run the improved pipeline (writes `outputs/improved_model_results.csv`):

```bash
python -m improved
```

4. Compare results (example):

```bash
python evaluation/compare_models.py outputs/naive_model_results.csv outputs/improved_model_results.csv
```

If you want to tweak the smoothing parameter used by the improved pipeline, edit `SMOOTHING_ALPHA` in `improved/__main__.py`.

