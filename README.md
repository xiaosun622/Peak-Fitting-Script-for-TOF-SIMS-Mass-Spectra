# Interactive Peak Fitting Tool for FIB TOF-SIMS and Mass Spectra

## Overview

This Jupyter Notebook-based tool provides an interactive workflow for peak fitting of **FIB TOF-SIMS** and other mass spectrometry spectra. It supports **Gaussian**, **Lorentzian**, and **PseudoVoigt** models, with optional **baseline correction** and **Savitzky–Golay smoothing**, and includes default settings for **uranium isotope ratio** analysis.

- **Current version:** 1.6.4 (234U included, particle region only)  
- **Author:** Xiao Sun (https://github.com/xiaosun622)

---

## Workflow

### 1. Load spectrum file
Reads a tab-delimited `.txt` file.

**Expected columns**
- `mass/charge (m/Q)` (x-axis)
- `Total (cts/TOF-Extraction)` (intensity)

### 2. Apply smoothing (optional)
Uses a Savitzky–Golay smoothing filter to reduce noise while preserving peak shape.

**Adjustable parameters**
- **Smooth Win:** window size (number of points)
- **Polyorder:** polynomial order used in smoothing

### 3. Define peak regions
For each ion, set a peak centre and range width (±).

Peak region is defined as:

- `centre ± range_width`

### 4. Baseline correction (optional)
If enabled, an estimated background is subtracted before fitting.

**Baseline options**
- **average:** flat baseline using predicted intensity at `centre ± offset`
- **linear:** line fit to surrounding baseline regions
- **polynomial:** 2nd-order polynomial fit

### 5. Select fit model
Choose a symmetric or asymmetric peak shape:

- Gaussian
- Lorentzian
- PseudoVoigt (or Voigt for asymmetric cases)

### 6. Fit the peak
The model is fitted to the baseline-corrected signal. Initial parameters are estimated (centre, amplitude, sigma), and then optimised to minimise the squared error.

### 7. Extract results
For each fitted peak, the tool reports:

- **Best-fit curve** (model prediction)
- **Fitting deviation** (data minus prediction)
- **R²** (goodness of fit)
- **Area** (peak amplitude from the model fit)

### 8. Plot outputs
Each subplot includes:

- Smoothed signal
- Corrected signal (if baseline correction is enabled)
- Model fit
- Fitting deviation (formerly “Residuals”)

### 9. Calculate isotope ratios
For uranium isotopes (e.g. 234U, 235U, 238U), the ratio is calculated as:

For uranium isotopes (234U, 235U, 238U), the ratio is:

Ratio = Area235 / (Area234 + Area235 + Area238)

## Terminology

| Term              | Meaning                                                         |
| ----------------- | --------------------------------------------------------------- |
| Fitting deviation | Difference between corrected data and model fit                 |
| Baseline          | Estimated background under the peak (subtracted before fitting) |
| Best fit          | Model prediction using optimised parameters                     |
| R²                | Coefficient of determination, closer to 1 indicates better fit  |

## Requirements

- Python 3.7+
- pandas
- numpy
- matplotlib
- scipy
- lmfit
- ipywidgets




### Install dependencies

```bash
pip install pandas numpy matplotlib scipy lmfit ipywidgets
