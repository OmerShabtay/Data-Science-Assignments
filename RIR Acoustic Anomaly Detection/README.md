# Room Impulse Response (RIR) Acoustics: Unsupervised Learning, PCA & Anomaly Detection

## Project Overview
This folder contains an end-to-end unsupervised learning, dimensionality reduction, and multi-dimensional anomaly detection study on the **Room Impulse Response (`rirmega`) Acoustic Metadata Corpus** (1,000 measured and physics-simulated 3D enclosures). Operating without ground-truth labels, this project investigates the latent geometry, multicollinearity, clustering behavior, and anomalous regimes of sound propagation in enclosed spaces.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Scikit-Learn, SciPy, Matplotlib, Seaborn
* **Environment:** Jupyter Notebook (with in-memory SSL stream ingestion for 100% OS-independent reproducibility)

## Physical Feature Engineering (10 Continuous Descriptors)
Rather than relying on raw stringified metadata, we unpack and engineer **10 continuous physical and 3D geometric features** from nested JSON structures and spatial coordinate vectors:
* **Acoustic Decay & Clarity:** Reverberation Time (`rt60`, in s), Direct-to-Reverberant Ratio (`drr_db`, in dB), Speech Clarity Index (`c50_db`, 50 ms window), and Music Clarity Index (`c80_db`, 80 ms window).
* **3D Enclosure Geometry:** Enclosure Volume ($V = L \times W \times H$, in $\text{m}^3$), Reflective Boundary Surface Area ($S = 2(LW + LH + WH)$, in $\text{m}^2$), and Geometric Elongation Aspect Ratio ($\max(L,W,H)/\min(L,W,H)$).
* **Spatial Placement & Materials:** Euclidean 3D Source-to-Microphone Distance ($\|\mathbf{r}_{\text{src}} - \mathbf{r}_{\text{mic}}\|_2$, in m), Mean Broadband Absorption Coefficient (`absorption`), and Low-Frequency 125 Hz Octave Band Absorption (`abs_125hz`).

## Key Pipeline Methodologies
* **Exploratory Data Analysis (EDA):** Distribution diagnostics (Skewness, Kurtosis) and $10 \times 10$ correlation mapping validating Sabine's reverberation scaling and inverse-square distance decay.
* **Dimensionality Reduction (PCA):** Standardized eigenvalue decomposition compressing 10D acoustics into orthogonal physical axes (`PC1`: 47.99% Global Scale & Clarity, `PC2`: 16.90% Material Absorption, `PC3`: 12.06% Corridor Elongation; 4 PCs retain 86.14% variance).
* **Dual-Space Clustering ($X$ and $X^T$):**
  * *Sample Space ($1000 \times 10$):* Contrasting centroid-based partitioning (**K-Means**, **Ward's Hierarchical Clustering**) against density connectivity (**DBSCAN**) using weighted intra-cluster variance and Silhouette scores.
  * *Feature Space ($10 \times 1000$):* Hierarchical Ward clustering and correlation dendrograms on the transposed matrix $X^T$ to isolate collinear feature families and orthogonal singletons (`aspect_ratio`, `abs_125hz`).
* **Multi-Dimensional Anomaly Detection:** Benchmarking parametric univariate thresholding (**Z-Score**, $|Z|>3$), random tree partitioning (**Isolation Forest**, `contamination=0.05`), and local reachability density (**Local Outlier Factor / LOF**, $k=20$) across overlap matrices, execution runtimes, and physical record inspections.
* **Executive Diagnostic Dashboard:** A 4-panel visual synthesis and 5-feature pairplot categorizing enclosures into *Normal ($n=887$)*, *Single-Method Flag ($n=55$)*, *Two-Method Agreement ($n=47$)*, and *Consensus Anomalies ($n=11$)*.

## Core Insights & Physical Discoveries
* **Continuous Sabine Manifolds vs. Artificial Clusters:** Because physical room dimensions scale continuously under Sabine's equation, the corpus forms a single connected density gradient rather than disjoint spherical blobs. Centroid algorithms (K-Means) impose arbitrary Voronoi boundaries across this continuum, whereas DBSCAN absorbs 90.2% of rooms into one macro-cluster (`n=902`) and flags the sparse tail of cavernous warehouses as noise (`n=98`).
* **Global Hull vs. Local Neighborhood Outliers:** Out of 113 rooms flagged by at least one detector, 48 of 50 Isolation Forest detections overlapped with Z-Score (leaving 0 unique to Isolation Forest), whereas **58% of LOF detections (29/50) were completely unique**, uncovering subtle multivariate anomalies hidden inside the dense core cloud.
* **Three Physical Archetypes of Consensus Anomalies:** Forensic inspection of the 11 universal consensus anomalies revealed:
  1. *Corridor Mathematical Divergence Artifacts (`#008`, `#045`, `#689`):* Elongated corridors (`aspect_ratio` $> 6.9$, `src_mic_dist` $> 16\text{ m}$) where negligible early energy arrives within 50 ms, causing `c50_db` to diverge below $-129\text{ dB}$.
  2. *Cavernous Industrial Warehouses (`#597`, `#820`, `#862`):* Legitimate extreme enclosures ($V > 2,770\text{ m}^3$, $RT_{60} > 1.17\text{ s}$) residing in the sparse upper tail.
  3. *Ultra-Dry Near-Field Micro-Offices (`#302`, `#562`):* Tiny damped enclosures ($V = 24.7\text{ m}^3$) or sub-meter transducer placements (`src_mic_dist` $= 0.985\text{ m}$) yielding extreme positive clarity ($C_{80} = 57.9\text{ dB}$).
