# Garmin Wearable Telemetry & Training Load Optimization Pipeline

A data science and sports science pipeline built in Python to parse raw, compressed Garmin binary fitness data (`.fit`), engineer time-series physiological features, and model athletic workload optimization.

## Objective
As a collegiate Division 1 distance runner and data science major, my goal was to engineer an end-to-end data pipeline capable of converting raw wearable telemetry into useful training stress metrics. This project models human fatigue accumulation and training using my historical cardiovascular exertion datasets.

## Architecture & Data Pipeline
The current iteration operates as a local proof-of-concept utilizing standard and enhanced telemetry layers:

1. **Binary Ingestion:** Utilizes the `fitparse` library to extract raw data from compressed Garmin Flexible and Interoperable Data (FIT) structures.
2. **Data Cleansing & Normalization:** Resolves structural anomalies including hardware-specific tracking fields (`enhanced_speed`), coordinates coordinate/speed drops, and handles irregular training schdules by reindexing data frames to a continuous daily timeline.
3. **Physiological Feature Engineering:** Computes daily Training Impulse (TRIMP) scores utilizing Banister’s exponential heart rate scaling model to properly weight cardiovascular strain over chronological duration.
4. **Time-Series Workload Modeling:** Implements multi-day rolling mathematical windows to isolate:
   * **Acute Training Load:** A 7-day rolling average tracking short-term physiological fatigue.
   * **Chronic Training Load:** A 28-day rolling average tracking long-term fitness adaptation.
   * **Acute-to-Chronic Workload Ratio (ACWR):** An optimization index predicting whether an athlete is under-training (<0.8), optimized (0.8–1.3), or in an elevated overtraining/injury risk zone (>1.5).

## Tech Stack & Dependencies
* **Language:** Python
* **Environment Manager:** Anaconda / Jupyter Notebooks
* **Core Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-Learn, Fitparse

## Project Roadmap
* [x] Parse binary `.fit` records and establish data frames.
* [x] Standardize metric transformations (single-leg cadence conversion to SPM, pace processing).
* [x] Engineer daily TRIMP, Acute, Chronic, and ACWR features.
* [x] Construct a dual-axis visual analytics dashboard mapping load vs. optimization zones.
* [x] Scale the data lake by ingesting a multi-year historical Garmin account archive export.
* [ ] Train a supervised machine learning model (e.g., Random Forest Regressor) to predict next-day recovery states (Resting Heart Rate / Heart Rate Registry) based on cumulative load features.
