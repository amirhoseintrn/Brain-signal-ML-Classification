# Brain-signal-ML-Classification
# EEG Mental Task Classification: Thinking vs. Rest

This MATLAB project implements a complete pipeline to classify brain signals (EEG) into two mental states: **active thinking** (mental arithmetic) and **rest**. The pipeline starts from raw `.edf` files, extracts a rich set of features, performs statistical analysis, applies multiple feature selection methods, reduces dimensionality, and finally evaluates 9 classifiers using stratified 10‑fold cross‑validation.

## 🧠 Key Features

- **Feature Extraction (per channel, per 2‑second window)**  
  20 features: Mean, Std, Median, Skewness, Kurtosis, RMS, Zero‑Crossing Rate, Hjorth parameters, Shannon & Spectral Entropy, ApEn/SampEn/PermEn (placeholders), and band powers (δ, θ, α, β, γ).

- **Statistical Analysis**  
  T‑test & Mann‑Whitney U test to identify discriminative features (p‑value ranking).

- **Feature Selection**  
  - **Filter methods:** FDR, Mutual Information, mRMR  
  - **Wrapper method:** ReliefF  
  - **Embedded methods:** LASSO (L1‑regularized logistic regression), Random Forest importance  
  - **Ensemble voting:** Majority voting over the top‑20 features from all methods → final 20 golden features.

- **Dimensionality Reduction** (visualization & analysis)  
  PCA, LDA (supervised), ICA, t‑SNE, Kernel PCA (RBF).

- **Classification** (10‑fold stratified CV)  
  Models: Naïve Bayes, k‑NN, SVM (RBF), LDA, Decision Tree, Random Forest, Gradient Boosting, Logistic Regression, Ensemble Subspace k‑NN.  
  Metrics: Accuracy, Sensitivity, Specificity, Precision, F1‑Score, AUC‑ROC, Cohen’s Kappa, Matthews Correlation Coefficient (MCC).

## 📂 Dataset Format

- Input: `.edf` files (e.g., from *EEG during Mental Arithmetic Tasks* database).  
- Files containing `_1.edf` → **Rest** (label=1), others → **Task** (label=2).  
- Sampling rate: 500 Hz.  
- Each file is segmented into non‑overlapping 2‑second windows.

## 🚀 How to Run

1. Update `dataPath` in **Cell 1** to point to your folder of `.edf` files.
2. Run **Cell 1** → extracts features and saves `eeg_features_final.mat`.
3. Run **Cell 2** → normalisation, statistical tests, boxplots of top features.
4. Run **Cells 10–13** → feature selection, dimensionality reduction, and final classification with 10‑fold CV.

## 📊 Output

- Feature selection ranking tables & bar plots.
- Dimensionality reduction scatter plots (PCA, t‑SNE, ICA, etc.).
- Final performance table (mean ± std across 10 folds) for all 9 classifiers.

## 🛠 Requirements

- MATLAB (tested on R2022b+)
- Toolboxes: Statistics and Machine Learning, Signal Processing, Parallel Computing (optional for `parfor`), Deep Learning (for `rica`), Econometrics (for `pca`), and Bioinformatics (if using `pdist2`).

## 📌 Notes

- The entropy placeholders (ApEn, SampEn, PermEn) are set to 0 – replace with actual implementations if needed.
- The code normalises using training‑set statistics only (Z‑score) to avoid data leakage.
- Parallel loop (`parfor`) speeds up feature extraction for many files.

## 👤 Author

[Your Name] – Final Year Project / EEG Classification Study

## 📄 License

MIT
