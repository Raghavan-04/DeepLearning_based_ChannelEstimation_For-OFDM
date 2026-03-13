# Deep Learning-based Channel Estimation for OFDM Wireless Communication

This repository contains the implementation of a software-based OFDM channel estimation framework that leverages a cascaded **Initial Denoising Network (IDN)** and a **Transformer-based model** to reconstruct high-fidelity Channel State Information (CSI).

--

## Visualisation
I have created a simple visualisation for Neural Network and OFDM signal and what our project does 

**OFDM:** https://ofdm-analysis.streamlit.app

**Neural Network:** https://deeplearningbasedchannelestimationfor-ofdm-zecx7xgix7fdxcalt7d.streamlit.app

--

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
| **IDN-Transformer** | **Phase_1** | **-0.70** | Superior noise suppression & global correlation. |
| **IDN-Transformer** | **Phase_2** | **-1.57** | Optimised|
| **IDN-Transformer** | **Phase_3** | **-4.56** | Optimised|
| **IDN-Transformer** | **Phase_4** | **-6.70** | Optimising...|

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
## Present timeline
Testing with different parameters 

**Problem**: Rayleigh fading creates "peaks" and "valleys" across time and frequency.
Adjacent subcarriers and adjacent symbols are highly correlated. By flattening  96 x 14 grid into a single 1D vector and using nn.Linear are completely destroying that 2D geometric relationship. Furthermore, because your Transformer's sequence length is forced to 1, it cannot track how the channel changes over time.



### 💡 The Solution: Phase 3 Optimization & Loss Function Upgrade

To resolve the geometric tracking issues and improve estimation accuracy, we implemented a Phase 3 optimization strategy:

**1. Strategic Parameter Reduction**

* We systematically reduced the model parameters by approximately 50%, bringing the total down to roughly 9,759,168.


* This reduction preserved a 2:1 ratio between consecutive layers while maintaining enough capacity for accurate channel estimation.


* Dimensions were kept as multiples of 64 to ensure optimal GPU processing efficiency.


* We further built and tested a variety model that successfully reduced parameters down to ~3 million while maintaining performance.



**2. Loss Function Upgradation (Amplitude Regularization)**

* **The Limitation:** Standard MSE treats real and imaginary parts independently without a coupling constraint. A network can minimize MSE while producing an incorrect complex amplitude, which directly degrades receiver SNR since received signal power depends on amplitude.


* **The Fix:** We introduced an explicit amplitude regularization penalty: $L_{amp} = E[||\hat{H}|| - [cite_start]||H||]^2$.


* **Updated Total Loss:** $L_{total} = L_{MSE} + 0.1 \times L_{amp}$.


* **Impact:** By keeping the weight at 0.1, amplitude acts as a regularizer rather than the dominant objective. This preserves physically meaningful channel magnitude profiles—analogous to perceptual losses in image super-resolution—and explicitly penalizes incorrect signal power.



### 🏆 Phase 3 Results

With the model optimizations and the upgraded loss function, the IDN-Transformer achieved a drastically improved NMSE of **-4.76 dB**.

---

## 🚀 Works Remaining

Our roadmap for completing the project includes:

1. **Scaled Training:** Training the complete deep learning pipeline (IDN -> Tokenization -> Transformer) on a larger dataset of 10,000 samples.

2. **Optimization:** Further DL model optimization and justification.

3. **Final Benchmarking:** Conducting a final comparison between the Deep Learning model and the Linear Minimum Mean Squared Error baseline.



---
## 🚀 Tech Stack
* **Language:** Python 
* **Frameworks:** PyTorch / TensorFlow
* **Libraries:** NumPy, SciPy (Signal Processing), Matplotlib (Visualization) 
* **Platform:** Google Colab with GPU support 

## 📚 References

* G. Tian, X. Cai, T. Zhou, W. Wang, and F. Tufvesson, "Deep-Learning Based Channel Estimation for OFDM Wireless Communications," *IEEE International Workshop on Signal Processing Advances in Wireless Communications (SPAWC)*, 2022.

* J. Guo, et al., "Deep Learning-Based Channel Estimation with Transformer," *IEEE Access*, 2021.

* Y. Li, X. Bian, M. Li, "Denoising Generalization Performance of Channel Estimation in Multipath Time-Varying OFDM Systems," *Sensors (MDPI)*, 2023.

