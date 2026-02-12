# Deep Learning-based Channel Estimation for OFDM Wireless Communication

[cite_start]This repository contains the implementation of a software-based OFDM channel estimation framework that leverages a cascaded **Initial Denoising Network (IDN)** and a **Transformer-based model** to reconstruct high-fidelity Channel State Information (CSI)[cite: 17, 18].



## 📌 Project Overview
[cite_start]Traditional estimation methods like Least Squares (LS) and LMMSE often struggle in low-SNR environments or require prior channel statistics that are unavailable in practice[cite: 13, 14, 15]. [cite_start]Our approach utilizes self-attention mechanisms to capture global time-frequency correlations across the OFDM grid, significantly outperforming conventional baselines[cite: 83, 84, 341].

---

## 🛠️ System Architecture
[cite_start]The framework consists of a three-stage deep learning pipeline[cite: 95, 107]:

1.  **Stage 1: Initial Denoising Network (IDN)**
    * [cite_start]A 4-layer dense network with LeakyReLU activation and Batch Normalization[cite: 144, 147, 149].
    * [cite_start]Suppresses AWGN from pilot-based CSI matrices to improve input quality[cite: 48, 97].
2.  **Stage 2: Tokenization**
    * [cite_start]Flattens the 2D grid into 1D sequential tokens[cite: 169, 170].
    * [cite_start]Appends positional encoding (Subcarrier and Symbol indices) to preserve spatial context[cite: 174, 176, 177].
3.  **Stage 3: Transformer Model**
    * [cite_start]Utilizes a Multi-Head Self-Attention mechanism to learn global dependencies across the resource grid[cite: 90, 99].

---

## 📊 Performance Benchmarking
[cite_start]Results obtained at **10 dB SNR** show the superiority of the proposed cascaded architecture[cite: 102, 341].

| Estimation Method | Model Category | NMSE (dB) | Core Strength |
| :--- | :--- | :--- | :--- |
| **Least Squares (LS)** | Mathematical Baseline | -1.20 | [cite_start]Simple; highly sensitive to noise[cite: 331, 332]. |
| **LMMSE** | Traditional Optimal | -1.37 | [cite_start]Traditional optimal but complex[cite: 335, 336]. |
| **IDN-Transformer** | **Proposed Model** | **-1.57** | [cite_start]Superior noise suppression & global correlation[cite: 339, 340]. |

---

## ⚙️ Model Specifications & Efficiency
[cite_start]The model is optimized for real-time performance on edge devices[cite: 269].

### Computational Metrics
| Metric | Phase 1 (50 Epochs) | Phase 2 (300 Epochs) |
| :--- | :--- | :--- |
| **Training Time** | [cite_start]8 Minutes [cite: 263] | [cite_start]40 Minutes [cite: 264] |
| **Latency** | [cite_start]~5ms [cite: 266] | [cite_start]~5ms [cite: 267] |
| **Inference GFLOPs** | [cite_start]0.039 [cite: 254] | [cite_start]0.039 [cite: 256] |
| **NMSE (dB)** | [cite_start]-0.70 [cite: 237] | [cite_start]**-1.57** [cite: 321] |

### Parameter Breakdown
| Module | Component | Parameter Count |
| :--- | :--- | :--- |
| **IDN** | 4x Linear + BatchNorm Layers | [cite_start]~4.1 Million [cite: 196] |
| **Transformer** | Embeddings + 4x Encoder Layers | [cite_start]~15.36 Million [cite: 215] |
| **Total** | **Full DL Model** | [cite_start]**~19.46 Million** [cite: 229] |

---

## 📋 Dataset Parameters
[cite_start]The simulation environment is modeled after realistic 5G/LTE resource blocks[cite: 117].

| Parameter | Value | Rationale |
| :--- | :--- | :--- |
| **Channel Model** | Rayleigh Fading | [cite_start]Non-line-of-sight (NLOS) multipath[cite: 117]. |
| **Subcarriers ($N_{SC}$)** | 96 | [cite_start]Standard 5G New Radio block size[cite: 117]. |
| **OFDM Symbols ($N_{SY M}$)**| 14 | [cite_start]Single resource block in time domain[cite: 117]. |
| **Pilot Density** | 1/4 (25%) | [cite_start]Maximizes spectrum efficiency[cite: 117]. |
| **Modulation** | 4-QAM / 16-QAM | [cite_start]Standard modulation schemes[cite: 117]. |

---

## 🚀 Tech Stack
* [cite_start]**Language:** Python [cite: 109]
* [cite_start]**Frameworks:** PyTorch / TensorFlow [cite: 111]
* [cite_start]**Libraries:** NumPy, SciPy (Signal Processing), Matplotlib (Visualization) [cite: 112, 113]
* [cite_start]**Platform:** Google Colab with GPU support [cite: 110]

