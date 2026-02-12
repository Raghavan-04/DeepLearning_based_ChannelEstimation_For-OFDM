# Deep Learning-based Channel Estimation for OFDM Wireless Communication

This project focuses on enhancing Channel State Information (CSI) recovery in OFDM-based wireless systems using a cascaded deep learning architecture. It specifically addresses the limitations of traditional estimation methods like Least Squares (LS) and Linear Minimum Mean Squared Error (LMMSE) in noisy environments.

---

 ## Project Overview

**Objective**: To develop a software-based framework that cascades an **Initial Denoising Network (IDN)** with a **Transformer-based model** to reconstruct high-fidelity CSI without requiring prior channel statistics.

---

 ## Problem Statement

Traditional estimation methods face several challenges:

**Noise Sensitivity**: Severe performance degradation in low SNR (Signal-to-Noise Ratio) environments.

**Statistical Dependency**: LMMSE requires prior knowledge of channel statistics, which are often unavailable in real-world scenarios.

**Architectural Limitations**: Existing CNN models often fail to capture long-range time-frequency correlations.



---

 ## Proposed Methodology

The framework utilizes a three-stage deep learning pipeline:

1. **Stage 1: Initial Denoising Network (IDN)**
* A 4-layer fully connected (Dense) network using LeakyReLU activation and Batch Normalization.


* 
**Function**: Predicts and subtracts pilot noise to enhance the quality of received CSI.




2. **Stage 2: Tokenization**
* Converts the 2D channel grid (Frequency × Time) into a 1D sequence.


* 
**Process**: Flattens the grid, separates real/imaginary components, and appends **Positional Encoding** (Subcarrier and Symbol indices) to preserve spatial coordinates.




3. **Stage 3: Transformer Model**
* Employs multi-head self-attention mechanisms.


* 
**Function**: Learns global correlations across subcarriers and symbols to reconstruct the complete CSI grid from limited pilot information.





---

## ## Simulation & Performance Results

### ### Dataset Parameters

| Parameter | Value |
| --- | --- |
| Channel Model | Rayleigh Fading 

 |
| No. of Subcarriers | 96 

 |
| No. of OFDM Symbols | 14 

 |
| Pilot Density | 25% of grid (Scattered/Sparse) 

 |

### ### Benchmark Results (SNR = 10 dB)

The proposed model was evaluated against traditional baselines using **Normalized Mean Square Error (NMSE)**:

| Method | NMSE (dB) |
| --- | --- |
| Least Squares (LS) | -1.20 dB 

 |
| LMMSE (Traditional Optimal) | -1.37 dB 

 |
| **IDN-Transformer (Proposed)** | <br>**-1.57 dB** 

 |

**Key Finding**: The IDN-Transformer consistently outperforms mathematical baselines by capturing global correlations across the 96 × 14 resource grid.

---

## ## Technical Stack

* 
**Language**: Python 


* 
**Libraries**: PyTorch/TensorFlow, NumPy, SciPy, Matplotlib 


* 
**Platform**: Google Colab with GPU support 



---

## ## Remaining Work

* Scaling the model to 10,000 samples.


* Optimization for **16-QAM** modulation.


* Final comparative analysis between the DL model and LMMSE.



Would you like me to draft a specific **Introduction** or **Conclusion** section for this README based on the project details?
