# Voice Error Analysis: Regression & Classification

## Project Overview
This folder contains an end-to-end systematic error analysis on the "Acoustic Features of Voice" dataset. Rather than exclusively optimizing for high accuracy, this project investigates model behavior to determine whether predictive failures arise from data quality, model limitations, or the overall problem formulation[cite: 1]. 

*   **Regression Phase:** Predicting Mean Fundamental Frequency (`meanfun`) to evaluate baseline linear assumptions versus non-linear tree ensembles[cite: 1].
*   **Classification Phase:** Predicting Speaker Gender (`label`) to investigate threshold sensitivity, probability confidence, and false-positive/false-negative trade-offs[cite: 1].

## Tech Stack
*   **Language:** Python
*   **Libraries:** Pandas, NumPy, Scikit-Learn, SciPy, Matplotlib, Seaborn
*   **Environment:** Jupyter Notebook

## Key Pipeline Interventions & Methodologies
*   **Rigorous Cross-Validation:** All model evaluations and statistical error properties are calculated using 5-fold cross-validation to balance the bias-variance trade-off while isolating test-fold outliers[cite: 1].
*   **Residual Diagnostics:** Visual and statistical mapping of errors (Skewness, Kurtosis, MAE) to identify heteroscedasticity, systematic biases, and heavy-tailed model instability[cite: 1].
*   **Threshold Sensitivity Mapping:** Iterating classification thresholds from 0.1 to 0.9 to track the divergence of Precision, Recall, F1, and MCC, ultimately identifying stable operating regions[cite: 1].

## Core Insights & Algorithmic Discoveries
*   **The Biological Ceiling:** Feature distribution mapping revealed that classification errors are not random; they cluster heavily in intersecting biological regions (e.g., low-pitch females and high-pitch males)[cite: 1]. This proves that relying purely on acoustic features has a hard predictive limit.
*   **Linear Limitations vs. Tree Adaptability:** The baseline Linear Regression failed heavily on extreme fundamental frequencies due to its rigid assumptions of linearity and homoskedasticity[cite: 1]. The Random Forest successfully recursively partitioned the feature space to adapt to distinct male/female subpopulations without enforcing a global formula[cite: 1].
*   **The Illusion of Confidence:** Probability analysis isolated "high-confidence errors" (predictions >80% certain but entirely wrong)[cite: 1]. This exposed a critical failure mode where models can be mathematically certain while practically incorrect, highlighting the need for "Uncertain" confidence thresholds in biological data applications[cite: 1].
