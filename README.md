# Deep Learning-based Channel Estimation for OFDM Wireless Communication

\This repository contains the implementation of a software-based OFDM channel estimation framework that leverages a cascaded **Initial Denoising Network (IDN)** and a **Transformer-based model** to reconstruct high-fidelity Channel State Information (CSI).



## 📌 Project Overview
Traditional estimation methods like Least Squares (LS) and LMMSE often struggle in low-SNR environments or require prior channel statistics that are unavailable in practice. Our approach utilizes self-attention mechanisms to capture global time-frequency correlations across the OFDM grid, significantly outperforming conventional baselines.

---

## 🛠️ System Architecture
The framework consists of a three-stage deep learning pipeline:

1.  **Stage 1: Initial Denoising Network (IDN)**
    * A 4-layer dense network with LeakyReLU activation and Batch Normalization.
    * Suppresses AWGN from pilot-based CSI matrices to improve input quality.
2.  **Stage 2: Tokenization**
    * Flattens the 2D grid into 1D sequential tokens.
    * Appends positional encoding (Subcarrier and Symbol indices) to preserve spatial context.
3.  **Stage 3: Transformer Model**
    * Utilizes a Multi-Head Self-Attention mechanism to learn global dependencies across the resource grid.

---

## 📊 Performance Benchmarking
Results obtained at **10 dB SNR** show the superiority of the proposed cascaded architecture.

| Estimation Method | Model Category | NMSE (dB) | Core Strength |
| :--- | :--- | :--- | :--- |
| **Least Squares (LS)** | Mathematical Baseline | -1.20 | Simple; highly sensitive to noise. |
| **LMMSE** | Traditional Optimal | -1.37 | Traditional optimal but complex. |
| **IDN-Transformer** | **Proposed Model** | **-1.57** | Superior noise suppression & global correlation. |

---

## ⚙️ Model Specifications & Efficiency
The model is optimized for real-time performance on edge devices.

### Computational Metrics
| Metric | Phase 1 (50 Epochs) | Phase 2 (300 Epochs) |
| :--- | :--- | :--- |
| **Training Time** | 8 Minutes | 40 Minutes  |
| **Latency** | ~5ms  | ~5ms  |
| **Inference GFLOPs** | 0.039  | 0.039  |
| **NMSE (dB)** | -0.70  | **-1.57**  |

### Parameter Breakdown
| Module | Component | Parameter Count |
| :--- | :--- | :--- |
| **IDN** | 4x Linear + BatchNorm Layers | ~4.1 Million  |
| **Transformer** | Embeddings + 4x Encoder Layers | ~15.36 Million  |
| **Total** | **Full DL Model** | **~19.46 Million**  |

---

## 📋 Dataset Parameters
The simulation environment is modeled after realistic 5G/LTE resource blocks.

| Parameter | Value | Rationale |
| :--- | :--- | :--- |
| **Channel Model** | Rayleigh Fading | Non-line-of-sight (NLOS) multipath. |
| **Subcarriers ($N_{SC}$)** | 96 | Standard 5G New Radio block size. |
| **OFDM Symbols ($N_{SY M}$)**| 14 | Single resource block in time domain. |
| **Pilot Density** | 1/4 (25%) | Maximizes spectrum efficiency. |
| **Modulation** | 4-QAM / 16-QAM | Standard modulation schemes. |

---

## 🚀 Tech Stack
* **Language:** Python 
* **Frameworks:** PyTorch / TensorFlow
* **Libraries:** NumPy, SciPy (Signal Processing), Matplotlib (Visualization) 
* **Platform:** Google Colab with GPU support 

