# Spotify Rock Music: Exploratory Data Analysis (EDA) 

## Project Overview
This folder contains an end-to-end Exploratory Data Analysis (EDA) of the "History of Rock (1950-2020)" dataset, originally extracted via the Spotify Web API. The project aims to uncover the historical trends, acoustic signatures, and algorithmic biases embedded within the rock music genre over seven decades.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Seaborn, Matplotlib, SciPy
* **Environment:** Jupyter Notebook

## Key Pipeline Interventions & Feature Engineering
Rather than just running standard statistics, this project focuses heavily on **Data Quality and Engineering**:
1. **Resolving Temporal Contamination:** The Spotify API inherently stamps "Remastered" or "Live" editions with their reissue year, severely biasing chronological analysis. I engineered a programmatic boolean mask to filter out these artifacts upstream, ensuring the true historical evolution of the dataset was preserved.
2. **Handling Algorithmic Placeholders:** Excision of API failure placeholders (e.g., exactly `0` for tempo or popularity) before calculating statistical moments.
3. **Categorical Type Casting:** Converting computationally misleading hidden categoricals (like musical `key` or `time_signature`) into strings to prevent continuous metric traps (e.g., calculating a "mean" musical scale).
4. **Decade Extraction:** Engineered a categorical `decade` feature using floor division for precise time-series aggregation.

## Core Insights & Algorithmic Discoveries
* **Algorithmic Breakdown on Complex Time Signatures:** Discovered a machine learning flaw in Spotify's audio analysis regarding the `time_signature` feature. Progressive rock tracks with asymmetric or shifting meters (e.g., Pink Floyd's "Money" in 7/8) break the algorithm's cyclical bar detection, forcing the API to default to a non-existent `1` time signature.
* **The Physical Constraints of Data:** The dataset overwhelmingly favors tracks composed in the keys of A, D, G, C, and E. This mathematically visualizes the physical limitations of the genre's primary instrument: the standard open chords on a standard-tuned guitar.
* **The "Loudness & Energy" Signature:** Rock music, by its algorithmic definition in this dataset, is heavily reliant on mastering intensity, showing a strict inverse correlation between `acousticness` and `popularity`/`energy`.
* **The Stability of Classic Rock:** Temporal analysis revealed that "Early" and "Mid" era rock maintain a higher, more stable median popularity on Spotify today compared to the "Modern" era, which displays a long tail of low-popularity tracks.
