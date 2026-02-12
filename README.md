This project focuses on a **Deep Learning (DL)-based framework** for high-fidelity Channel State Information (CSI) recovery in **OFDM wireless systems**. By cascading a denoising network with a Transformer model, the system suppresses pilot noise and exploits global correlations across the OFDM grid without requiring prior channel statistics.

# Deep Learning-based Channel Estimation for OFDM Wireless Communication

## 📌 Problem Statement

Traditional estimation methods like **Least Squares (LS)** and **Linear Minimum Mean Squared Error (LMMSE)** face several hurdles in real-world environments:
 
**Sensitivity to Noise:** Performance degrades significantly in low Signal-to-Noise Ratio (SNR) environments.
 
**Statistical Dependency:** LMMSE requires prior knowledge of channel statistics, which are often unavailable.
 
**Local Limitations:** Existing CNN models often fail to capture long-range time-frequency correlations.



## 🚀 Proposed Methodology

The architecture is a software-based framework developed using **Python** and **PyTorch**. It utilizes a three-stage pipeline:

1. **Stage 1: Initial Denoising Network (IDN):** A 4-layer fully connected network suppresses AWGN noise from the received pilot CSI.


2. **Stage 2: Tokenization:** The 2D CSI grid is flattened and converted into 1D sequences. Real and imaginary components are separated, and positional encoding is added to preserve time-frequency coordinates.


3. **Stage 3: Transformer Model:** A Multi-Head Self-Attention mechanism is used to reconstruct the complete CSI by capturing global dependencies across subcarriers and symbols.



---

## 📊 Performance & Results

The model was benchmarked against traditional methods at **10 dB SNR** and evaluated using **Normalized Mean Squared Error (NMSE)**.

Estimation Method,Model Category,NMSE (dB)
Least Squares (LS),Mathematical Baseline,-1.20 dB 
LMMSE,Traditional Optimal,-1.37 dB 
IDN-Transformer,Proposed Project Model,-1.57 dB +1

### Key Metrics: 
**Latency:** ~5ms per inference, making it suitable for time-sensitive processing.

**Complexity:** Approximately 19.46 Million parameters.
  
**Efficiency:** 0.039 GFLOPs per inference, optimized for edge device deployment.



## 🛠️ Tools Used
 
**Language:** Python 
 
**Frameworks:** PyTorch / TensorFlow 
 
**Environment:** Google Colab (GPU Support) 

**Libraries:** NumPy, SciPy, Matplotlib 



---
