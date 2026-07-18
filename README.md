# Code and Data for Predicting Longitudinal Profiles of Persistent Supraglacial Streams

This repository contains a Python-based analysis workflow and data used  for the manuscript "Predicting longitudinal profiles of persistent supraglacial streams" across five glaciers: Siachen and Rongbuk (High Mountain Asia), Fountain (Canadian Arctic), and Vonbreen and Veteranbreen (Svalbard, Norway).  The workflow is organized into three sequential interactive python notebooks covering data importing, analysis, and plotting. All results, fitted parameters, goodness-of-fit statistics, and figures are generated automatically by running the notebooks in order.

## Description of notebooks

### `01_DataPrep.ipynb` — Data Loading & Preprocessing
 It assignes the α values that determine the slope trend and creates the stream metadata registry containing group names, labels, colors, markers, and trend types for all 16 supraglacial streams across 5 glaciers (Siachen, Rongbuk, Fountain, Vonbreen, and Veteranbreen). All CSV files are loaded from the `Stream_csv/` folder. The loaded and processed data is saved to `data.pkl` for use in subsequent notebooks.

### `02_Analysis.ipynb` — Stream data Analysis

This notebook performs all quantitative analysis on the loaded glacier stream data. It sequentially computes:

* Sinuosity — arc length and chord length per segment, cumulative sinuous and normal lengths
* Segment means — mean velocity, elevation, length and maximum elevation per segment using all the points.
* Slope — `slope_l` (along stream path, computed as elevation difference between neighbouring segments divided by their length difference) and `slope_d` (along flowline path) Refere supplementary Text S1 for more details.
* Negative Divergence of stream length — Calculated as $\partial_{x'} Q_i^s = \frac{-v_i\,\Delta x_i + v_{i-1}\,\Delta x_{i-1}}{\Delta x'}$ per segment.
* beta' (slope profile parameter) — fitted from the slope profile equation $s={\beta'}x^{\frac{\alpha-1}{2}}$ (Eq.3 in the main text), with corresponding standard error.
* beta' (elevation profile parameter) — fitted from the elevation integral equation, $z(x)=z(x_0)-\beta'\left(x^{\frac{\alpha+1}{2}}-x_0^{\frac{\alpha+1}{2}}\right)$ (Eq.4 in the main text), with corresponding standard error.
* Goodness of fit metrics — R² and RMSE for both the slope profile fit and the elevation profile fit.
Results are saved to `analysis.pkl` for use in the plotting notebook.
* Sinuosity was predicted using the relation $\mathcal{S}(x)\doteq\frac{s'}{\beta' x^{\frac{\alpha-1}{2}}}$ (Eq.6 in the main text)
* Uncertainty analysis - Estimation of propagated error in calculation of streams slope, modelled stream slope, and modelled elevation

### `03_Plotting.ipynb` — Figures & Export csv

This notebook generates all manuscript figures and exports the fitted parameter values. It produces:

* Fig. 2 ab — Normalized slope and elevation profiles for α=0 streams (sia_2, sia_4, sia_5, and vet_1)
* Fig. 3 ab — Normalized slope and elevation profiles for α=2 streams (fou_1 - fou_4 and von_1 - von_4)
* Fig. 3 cd — Normalized slope and elevation profiles for α=1 streams (sia_1, sia_3, sia_6, and ron_1)
* Fig. 4 — observed vs predicted sinuosity scatter plot for all streams
* Fig. S5 — Elevation profiles along flowline for each glacier group
* Fig. S6 — Negative divergence of stream length along flowline for each glacier group
* Fig. S7 — Sinuosity variation and slope KDE distributions for each α values in separate panels
* A CSV file (`beta'_values.csv`) containing the fitted `β' ± SE` (Slope and elevation profile) values for all 16 streams formatted to 3 significant figures.

## Description of Folders
### `Stream_csv/` — Input Data
Contains the raw CSV files for all 16 streams across the 5 glacier systems. Each file contains point-level (5m-Interval measurements of position (`x`, `y`), along-stream distance (`distance`), surface elevation (`elev`), surface velocity (`velocity`), and `relief`. Files are named by stream codes (`sia_1.csv` through `vet_1.csv`).
### `Output/` 
Stores all the plots and csv files.
### `Stream_kml`
Containes all the kml files of the 16 delineated stream centerlines. Files are named by stream codes.
