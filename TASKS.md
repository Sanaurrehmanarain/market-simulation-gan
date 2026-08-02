# Project Tasks & Problem Solving Log

## ❓ Core Problems Solved

### 1. The Non-Stationarity Problem
* **Issue:** Financial prices trend upwards (non-stationary), causing Neural Networks to fail.
* **Solution:** Transformed raw closing prices into **Log Returns** to stabilize the mean and variance.
* **Result:** The GAN could learn the *distribution* of changes rather than absolute prices.

### 2. The "Mode Collapse" Problem
* **Issue:** In early experiments, the Generator produced flat lines at -1.0 and +1.0 (Saturation).
* **Diagnosis:** The `tanh` activation function was saturating due to vanishing gradients.
* **Solution:** Implemented **Batch Normalization** after every LSTM layer and added **Dropout (0.3)** to the Discriminator.
* **Result:** The model broke out of the local minimum and began generating volatile sequences.

### 3. The "Warm-Up" Artifact
* **Issue:** The LSTM Generator produced a flat line for the first 10 days of every sequence due to empty initial hidden states.
* **Solution:** Implemented a **Post-Processing Pipeline** that generates 60 days of data but trims the first 10 "warm-up" days.
* **Result:** Final synthetic data (50-day sequences) is 100% free of initialization artifacts.

## ✅ Task Checklist
- [x] **Data Pipeline:** Fetch S&P 500 data via `yfinance` API.
- [x] **Preprocessing:** Normalize data (-1, 1) and create rolling window sequences.
- [x] **Architecture:** Design LSTM Generator and Discriminator.
- [x] **Training:** Implement Minimax adversarial training loop.
- [x] **Debugging:** Fix Mode Collapse using Batch Norm.
- [x] **Evaluation:** Validate using PCA (Principal Component Analysis) and Distribution Plots.
- [x] **Visualization:** Generate high-quality comparison plots for the Thesis.