# Neural Data Repository Learning Guide

This repository contains teaching material for a neural data science module. It is organized around two practical data-analysis workflows:

1. Local field potential (LFP) analysis
2. Calcium imaging analysis

The main goal is to learn how raw neural recordings are loaded, inspected, preprocessed, transformed, and evaluated before downstream scientific analysis.

## Repository Map

```text
.
|-- README.md
|-- requirements.txt
|-- instructor-notes.md
|-- 01-local_field_potential/
|   |-- local-field-potential.ipynb
|   |-- exercises.ipynb
|   |-- code/
|   |   |-- lfp_functions.py
|   |   |-- OpenEphys.py
|   |   `-- utils.py
|   `-- imgs/
|-- 02-calcium_imaging/
|   |-- calcium_imaging.ipynb
|   |-- calcium_imaging_colab.ipynb
|   |-- exercises.ipynb
|   |-- code/
|   |   |-- auxiliary_functions.py
|   |   |-- normalization_functions.py
|   |   `-- utils.py
|   `-- imgs/
`-- styles/
```

## How To Use The Repository

Start with the root `README.md` for setup instructions. The notebooks are the primary learning material, and the Python files in each `code/` folder provide helper functions used by the notebooks.

Recommended order:

1. Open `01-local_field_potential/local-field-potential.ipynb`.
2. Work through `01-local_field_potential/exercises.ipynb`.
3. Open `02-calcium_imaging/calcium_imaging.ipynb`.
4. Work through `02-calcium_imaging/exercises.ipynb`.
5. Use `02-calcium_imaging/calcium_imaging_colab.ipynb` if running the calcium imaging lesson in Google Colab.

## Module 1: Local Field Potential

The LFP lesson introduces continuous extracellular neural signals and the signal-processing tools used to study them.

Main notebook:

- `01-local_field_potential/local-field-potential.ipynb`

Supporting code:

- `01-local_field_potential/code/lfp_functions.py`: band-pass filtering, Morlet wavelet transform, and power estimation.
- `01-local_field_potential/code/OpenEphys.py`: loader for Open Ephys continuous, event, and spike files.
- `01-local_field_potential/code/utils.py`: data download helper.

What to learn:

- What an LFP signal represents biologically.
- How sampling rate affects what frequencies can be measured.
- Why Nyquist frequency matters.
- How Fourier analysis summarizes frequency content.
- How detrending and de-averaging prepare continuous signals.
- How filtering isolates activity in a target frequency band.
- How wavelet transforms reveal time-varying frequency content.
- How oscillatory events such as theta rhythms or ripples can be detected.

Key technical topics:

- Continuous neural signals
- Sampling frequency
- Nyquist theorem
- Fourier transform
- Power spectrum
- Butterworth filters
- Filter order and frequency bands
- Time-frequency analysis
- Wavelets and Morlet transforms
- Instantaneous power
- Oscillation detection

### LFP Exercises

Exercise notebook:

- `01-local_field_potential/exercises.ipynb`

Exercises:

1. Explore filter parameters
   - Filter short LFP segments in different frequency bands.
   - Compare how the filtered signal changes across bands.
   - Change filter order while keeping the frequency band fixed.
   - Measure how filter order affects computation time.

2. Wavelet transform with real wavelets
   - Compare wavelet-based time-frequency representations.
   - Inspect how wavelet choice changes temporal and frequency resolution.
   - Connect wavelet parameters to the uncertainty tradeoff.

3. REM sleep detection
   - Use theta and delta power to distinguish REM from non-REM periods.
   - Compute a theta/delta ratio or difference.
   - Plot examples of REM and non-REM LFP segments.
   - Think about how a biological state can be inferred from signal features.

Questions to answer after the exercises:

- What changes when the filter order increases?
- What information is lost when looking only at the power spectrum?
- Why does wavelet analysis help with transient oscillatory events?
- Why is theta/delta power useful for sleep-state classification?

## Module 2: Calcium Imaging

The calcium imaging lesson introduces video-based neural recordings and the CaImAn processing pipeline.

Main notebooks:

- `02-calcium_imaging/calcium_imaging.ipynb`
- `02-calcium_imaging/calcium_imaging_colab.ipynb`

Supporting code:

- `02-calcium_imaging/code/auxiliary_functions.py`: plotting, field-of-view inspection, temporal pixel traces, spatial filtering, and summary images.
- `02-calcium_imaging/code/normalization_functions.py`: detrending, AR noise estimation, and trace normalization.
- `02-calcium_imaging/code/utils.py`: data download helper.

What to learn:

- What calcium imaging measures and how it differs from electrophysiology.
- How to load and inspect calcium imaging movies.
- How to use summary images to evaluate a recording.
- Why motion correction is needed before extracting neural activity.
- The difference between rigid and piecewise-rigid motion correction.
- How CaImAn performs source extraction with CNMF.
- How spatial footprints and temporal traces represent extracted components.
- How parameter choices affect source extraction quality.
- How denoising, deconvolution, and normalization support downstream analysis.

Key technical topics:

- Fluorescence movies
- Field of view and region of interest
- Pixel intensity traces
- Motion artifacts
- Rigid motion correction
- Piecewise-rigid motion correction
- Spatial filtering
- Correlation images
- Peak-to-noise ratio images
- Image crispness
- CNMF source extraction
- Spatial footprints
- Temporal calcium traces
- Autoregressive calcium dynamics
- Trace normalization
- Source evaluation

### Calcium Imaging Exercises

Exercise notebook:

- `02-calcium_imaging/exercises.ipynb`

Exercises:

1. Image characteristics
   - Inspect the field of view and region of interest.
   - Plot temporal traces from randomly selected pixels.
   - Compare active and inactive pixels.
   - Explain why source extraction is needed instead of analyzing individual pixels directly.

2. Motion correction parameters
   - Apply different spatial filters to frames.
   - Compare the visual effects of different `gSig_filt` values.
   - Run motion correction with different settings.
   - Measure quality using crispness and summary images.
   - Compare rigid and piecewise-rigid correction.

3. Source extraction parameters
   - Explore how CNMF parameters change detected components.
   - Inspect spatial footprints and calcium traces.
   - Relate parameter choices to false positives, missed cells, and trace quality.

Questions to answer after the exercises:

- Why can raw pixel traces be misleading?
- What image features make motion correction easier or harder?
- When is piecewise-rigid correction preferable to rigid correction?
- How do `min_corr`, `min_pnr`, `gSig`, and `gSiz` affect source extraction?
- What makes an extracted component biologically plausible?

## Cross-Cutting Concepts

These concepts appear across both modules and are worth studying explicitly:

- Data loading and file formats
- Sampling rate and temporal resolution
- Noise, artifacts, and preprocessing
- Signal-to-noise ratio
- Visualization as a quality-control tool
- Parameter sensitivity
- Reproducible notebook workflows
- Separating raw data, processed data, and analysis outputs
- Interpreting algorithms in terms of biological assumptions

## Suggested Learning Path

Beginner path:

1. Run each notebook from top to bottom.
2. Reproduce every figure.
3. Change one parameter at a time and describe what changes.
4. Complete the exercise notebooks with short written answers.

Intermediate path:

1. Read the helper functions used by each notebook.
2. Reimplement one plotting or analysis step in a new notebook cell.
3. Add timing comparisons for expensive operations.
4. Compare multiple preprocessing parameter settings with the same metric.

Advanced path:

1. Write reusable functions for repeated analysis steps.
2. Add tests for small numerical helper functions where practical.
3. Create a short report comparing parameter settings.
4. Extend the lessons with a downstream analysis, such as state classification for LFP or event-rate comparison for calcium traces.

## Skills To Practice

Python and notebooks:

- Navigating JupyterLab
- Running cells in order
- Reading stack traces
- Using NumPy arrays
- Plotting with Matplotlib and Seaborn
- Timing code with `%timeit`

Signal processing:

- Thinking in time and frequency domains
- Choosing filter bands
- Understanding frequency resolution
- Understanding time-frequency tradeoffs
- Interpreting power traces

Neural data analysis:

- Identifying artifacts
- Comparing raw and processed data
- Connecting analysis parameters to biological interpretation
- Evaluating whether a detected event or component is plausible

Scientific workflow:

- Keeping notes on parameter choices
- Recording assumptions
- Comparing outputs systematically
- Explaining what each preprocessing step changes

## Practical Study Checklist

Use this checklist while working through the repository:

- [ ] I can explain the difference between LFP and calcium imaging data.
- [ ] I can describe what preprocessing each module performs.
- [ ] I can load and visualize the example data.
- [ ] I can explain why sampling rate matters.
- [ ] I can compute and interpret a power spectrum.
- [ ] I can apply a band-pass filter and explain the result.
- [ ] I can describe the purpose of wavelet analysis.
- [ ] I can explain why motion correction is needed in calcium imaging.
- [ ] I can compare rigid and piecewise-rigid motion correction.
- [ ] I can interpret correlation and PNR images.
- [ ] I can describe what CNMF source extraction produces.
- [ ] I can explain how parameter choices affect the output.
- [ ] I can write a short interpretation of each exercise result.

## Possible Extensions

Ideas for extending the repository:

- Add a completed example solution notebook for each exercise set.
- Add a `data/README.md` describing expected downloaded data folders.
- Add a short glossary of neural data terms.
- Add automated checks for helper functions that do not require large datasets.
- Add a project notebook that compares multiple LFP states or calcium imaging sessions.
- Add a spike-data lesson when the planned spike module is available.
