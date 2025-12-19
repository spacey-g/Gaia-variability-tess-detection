Gaia–TESS Variability Detection Pipeline
Project Overview

This project investigates stellar photometric variability by combining data from Gaia DR3 and TESS.
The aim is to quantify low-amplitude stellar variability and assess its impact on exoplanet detection and confirmation, with special attention to separating intrinsic stellar signals from instrumental systematics.

An end-to-end, reproducible pipeline is implemented that:

selects stars from Gaia DR3,

retrieves corresponding TESS light curves,

performs time-series variability analysis,

and visualizes variability across the Hertzsprung–Russell (HR) diagram.

Scientific Motivation

Stellar variability introduces noise that can obscure or mimic exoplanet transit signals.
By cross-matching Gaia’s precise stellar characterization with TESS’s high-cadence photometry, we can:

identify low-level stellar variability,

distinguish astrophysical signals from instrumental effects,

and better understand stellar noise sources affecting exoplanet surveys.

Pipeline Overview
1️ Gaia DR3 Star Selection

Minimal synchronous ADQL queries (robust to Gaia Archive instabilities)

Selection of bright stars with reliable photometry

Extracted parameters:

source_id

RA / Dec

G-band magnitude

BP–RP color

2️ TESS Light Curve Retrieval

TESS light curves are searched and downloaded using RA/Dec

Implemented via lightkurve

Handles missing TESS coverage gracefully

3️ Light Curve Processing

Each light curve is:

cleaned of NaNs,

flattened to remove long-term trends,

normalized to focus on short-timescale variability.

4️ Variability Quantification

We compute:

RMS variability (photometric scatter)

Lomb–Scargle periodograms to detect dominant periodicities

Dominant periods shorter than ≈ 0.05 days are flagged as likely instrumental systematics.

Output Figures & Results
🔹 TESS Light Curve Example

This figure shows a cleaned and normalized TESS light curve for a Gaia-selected star.

Interpretation:

Low-amplitude variability

Presence of short-timescale fluctuations

Useful for identifying transit-like or systematic features

🔹 Lomb–Scargle Periodogram

Periodogram used to identify dominant variability timescales.

Interpretation:

Strong power at very short periods (~minutes)

Indicative of instrumental systematics rather than stellar rotation or pulsation

🔹 Gaia HR Diagram Colored by TESS RMS Variability

This is the main science figure of the project.

Interpretation:

Demonstrates how photometric variability is distributed across stellar populations

Links stellar properties (color, luminosity) to variability amplitude

Directly relevant for understanding exoplanet detection sensitivity

 Output Data Products

gaia_tess_variability_final_catalog.csv
Final merged Gaia–TESS catalog containing:

Gaia identifiers and photometry

TESS RMS variability

Dominant period

Instrumental vs astrophysical flag

Variability class (quiet / mild / strong)

Example Scientific Result

For a representative Gaia DR3 source, the retrieved TESS light curve exhibits low-amplitude variability (RMS ≈ 0.002). Lomb–Scargle analysis reveals a dominant period at ≈ 0.01 days, consistent with instrumental systematics rather than intrinsic stellar variability.

This highlights the importance of systematics-aware variability analysis when interpreting photometric data for exoplanet studies.

 Technologies Used

Python

astroquery – Gaia Archive access

lightkurve – TESS data handling

astropy – time-series analysis

numpy, pandas, matplotlib

 Future Work

Potential extensions include:

Scaling to larger Gaia samples (50–100+ stars)

Cross-matching with Gaia DR3 variability tables

Machine-learning–based variability classification

Explainable AI (XAI) analysis of stellar light curves

Direct application to exoplanet false-positive mitigation

Author & Research Context

This project was developed as part of an astronomy research portfolio focused on:

time-domain astrophysics,

stellar variability,

and exoplanet detection methodologies.

It is intended for research development.
