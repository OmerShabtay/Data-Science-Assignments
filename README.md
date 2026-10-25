# Data Science Assignments 📊

This repository contains my data science projects and assignments, focusing on data engineering, statistical diagnostics, supervised error analysis, and unsupervised manifold & anomaly learning.

## Repository Contents

### 📂 [HW1: History of Rock EDA](./History%20of%20Rock%20EDA/)
An end-to-end Exploratory Data Analysis of Spotify's "History of Rock (1950-2020)" dataset.
* **Focus:** Feature engineering, handling algorithmic biases (e.g., API failure placeholders, time-dependency of remastered tracks), and advanced categorical analysis.
* **Key Discovery:** Identified an algorithmic breakdown in Spotify's audio analysis model regarding complex/asymmetric time signatures (e.g., Pink Floyd's "Money").
* **Tech Stack:** Python, Pandas, NumPy, SciPy, Seaborn, Matplotlib.

### 📂 [HW2: Regression & Classification Error Analysis](./Voice%20Error%20Analysis/)
A systematic investigation of model failure patterns using the "Acoustic Features of Voice" dataset.
* **Focus:** Moving beyond basic accuracy to diagnose heteroscedasticity, isolate extreme errors, evaluate threshold sensitivity, and compare linear assumptions against tree-based ensembles.
* **Key Discovery:** Models systematically fail at hard biological boundaries (overlapping pitch ranges between genders) where acoustic traits naturally blur, proving that non-linear tree ensembles are required to map hidden subpopulations.
* **Tech Stack:** Python, Pandas, NumPy, Scikit-Learn, SciPy, Seaborn, Matplotlib.

### 📂 [HW3: Unsupervised Learning, Dimensionality Reduction & Anomaly Detection](./RIR%20Acoustic%20Anomaly%20Detection/)
An unsupervised geometric and anomaly investigation of the "Room Impulse Response (`rirmega`)" physical acoustics corpus (1,000 enclosures × 10 engineered physical and geometric descriptors).
* **Focus:** 3D spatial feature engineering, Principal Component Analysis (PCA), dual-space clustering on samples and transposed features ($X$ vs. $X^T$ via K-Means, Ward Hierarchical, and DBSCAN), and multi-dimensional anomaly detection (Z-Score, Isolation Forest, and Local Outlier Factor).
* **Key Discovery:** Demonstrated that physical room acoustics form a continuous Sabine manifold rather than discrete spherical clusters, and uncovered a stark spatial divergence between global boundary outliers (cavernous warehouses and $-134\text{ dB}$ corridor divergence artifacts) and local neighborhood density anomalies (LOF).
* **Tech Stack:** Python, Pandas, NumPy, Scikit-Learn, SciPy, Seaborn, Matplotlib.
