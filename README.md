# Interactive Peak Fitting Tool for FIB TOF-SIMS / Mass Spectra

## Overview

This Jupyter Notebook-based tool is designed for interactive peak fitting of FIB TOF-SIMS and other mass spectrometry data. It supports Gaussian, Lorentzian, and PseudoVoigt models with optional baseline correction, smoothing, and default settings on uranium isotope ratio analysis.

**Current Version:** 1.4.6

**Author:** Xiao Sun [https://github.com/xiaosun622]

---

## Workflow: Step-by-Step Procedure

### 1. Load Spectrum File

* Reads a tab-delimited `.txt` file.
* Expected columns:

  * `mass/charge (m/Q)` (x-axis)
  * `Total (cts/TOF-Extraction)` (intensity)

### 2. Apply Smoothing (Optional)

* Savitzky–Golay smoothing filter reduces noise while preserving peak shape.
* Adjustable parameters:

  * `Smooth Win`: Window size
  * `Polyorder`: Polynomial order used in smoothing

### 3. Define Peak Regions

* User inputs peak center and range width (±) for each ion.
* Regions are defined as: `center ± range_width`

### 4. Baseline Correction (if enabled)

* Options:

  * `average`: Flat baseline using predicted intensity ± offset
  * `linear`: Line fit to surrounding regions
  * `polynomial`: 2nd-order polynomial fit
* This background is subtracted from the signal to isolate the peak.

### 5. Select Fit Model

* Choose between symmetric or asymmetric peak shapes:

  * Gaussian
  * Lorentzian
  * PseudoVoigt (or Voigt for asymmetric cases)

### 6. Fit the Peak

* The fitting is applied to the **baseline-corrected signal**.
* Initial parameters are estimated (center, amplitude, sigma).
* The model is optimized to minimize the squared difference between corrected data and prediction.

### 7. Extract Results

* From the fit result:

  * Best-fit curve (`model_prediction`)
  * Fitting Deviation (`data - prediction`)
  * R² (goodness of fit)
  * Area (peak amplitude)

### 8. Plot Outputs

Each subplot includes:

* Smoothed signal
* Corrected signal
* Model fit
* **Fitting Deviation** (formerly “Residuals”)

### 9. Calculate Isotope Ratios

For isotope pairs (e.g. 235U vs 238U), the ratio is:

```math
\text{Ratio} = \frac{\text{Area}_{235}}{\text{Area}_{235} + \text{Area}_{238}}
```

### 10. Save Outputs (Manual Trigger)

* Press "Save Results" after fitting to export:

  * A PNG image of all plots
  * A CSV summary table with areas, R², and isotope ratios

---

## Terminology

| Term                  | Meaning                                                         |
| --------------------- | --------------------------------------------------------------- |
| **Fitting Deviation** | Difference between corrected data and model fit                 |
| **Baseline**          | Estimated background under the peak (subtracted before fitting) |
| **Best Fit**          | Model prediction using optimized parameters                     |
| **R²**                | Coefficient of determination; closer to 1 means better fit      |

---

## Requirements

* Python 3.7+
* `pandas`, `numpy`, `matplotlib`, `scipy`, `lmfit`, `ipywidgets`

Install via pip:

```bash
pip install pandas numpy matplotlib scipy lmfit ipywidgets
```

---
