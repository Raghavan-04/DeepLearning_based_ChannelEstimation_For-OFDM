
## **Current Parameters Extracted **

From your `96 × 14 × 10000` dataset, are currently extracting:

### **Per-Sample Parameters** (for each of 10000 samples)
| Category | Number of Parameters |
|----------|---------------------|
| **Channel Impulse Response** | 96 (delay taps) |
| **Complex Gains** | 96 (per path) |
| **Multipath Delays** | 31 paths + 3 metrics |
| **Doppler Parameters** | 5 metrics |
| **Angle of Arrival** | 23 angles + 2 metrics |
| **Coherence Parameters** | 12 metrics |
| **Statistics** | 8 metrics |
| **TOTAL per sample** | **~270 parameters** |

### **Aggregate Across Samples**
- **Total stored parameters**: ~2.7 million (270 × 10,000)
- **Visualization outputs**: 12 plots per sample

## **Maximum Extractable Parameters (Theoretical)**

With data structure: **10,000 samples × 96 subcarriers × 14 symbols**, we could extract:

### **1. Time-Domain Parameters** (per sample)
```
- Impulse response taps: 96
- Complex gains: 96 (magnitude + phase = 192 parameters)
- Power delay profile: 96
- RMS delay spread: 1
- Mean excess delay: 1
- Maximum excess delay: 1
- Delay window: 1
- Number of significant taps: 1
- Tap locations: up to 96
```
**Subtotal: ~400 parameters/sample**

### **2. Frequency-Domain Parameters** (per sample)
```
- Frequency response: 96 (magnitude + phase = 192)
- Coherence bandwidth (multiple thresholds): 5
- Frequency correlation matrix: 96×96 = 9,216
- Subcarrier correlation coefficients: 96
- Group delay: 96
- Phase linearity: 1
```
**Subtotal: ~9,600 parameters/sample**

### **3. Time-Variation Parameters** (per sample)
```
- Doppler spectrum: 14 points
- Maximum Doppler shift: 1
- Doppler spread: 1
- Coherence time: 1
- Channel aging rate: 1
- Time correlation matrix: 14×14 = 196
- Symbol-to-symbol correlation: 14
- Channel variation rate: 1
- Doppler frequency components: up to 14
```
**Subtotal: ~230 parameters/sample**

### **4. Statistical Parameters** (across samples)
```
- Distribution parameters (Rayleigh/Rician): 3
- K-factor: 1
- Nakagami-m parameter: 1
- Fading severity: 1
- Level crossing rate: 1
- Average fade duration: 1
- Higher-order statistics: 5
- Channel capacity: 1
- Outage probability: 1
```
**Subtotal: ~15 parameters (global)**

### **5. Spatial Parameters** (using virtual array)
```
- AoA spectrum: 181 angles
- AoA peaks: up to 96
- Angular spread: 1
- Spatial correlation: 96×96 = 9,216
- Virtual array manifold: 96×181 = 17,376
- MUSIC pseudospectrum: 181
- Beamforming weights: 96×181 = 17,376
```
**Subtotal: ~44,000 parameters/sample**

### **6. Channel Capacity & Information Theory**
```
- Instantaneous capacity: 1
- Ergodic capacity: 1
- Outage capacity: 1
- Mutual information: 1
- Channel entropy: 1
- Diversity order: 1
- Multiplexing gain: 1
```
**Subtotal: ~7 parameters/sample**

### **7. Advanced Features** (machine learning ready)
```
- Time-frequency images: 96×14 = 1,344 pixels
- STFT representations: 96×14×2 = 2,688
- Wavelet coefficients: up to 96×14×4 = 5,376
- PCA components: up to 96
- Autoencoder features: configurable
- Channel state information (CSI) matrices: 96×14×2 = 2,688
```
**Subtotal: ~12,000 parameters/sample**

## **Complete Parameter Budget**

| Level | Parameters per Sample | Total for 10k Samples |
|-------|----------------------|----------------------|
| **Basic (current)** | 270 | 2.7M |
| **Comprehensive** | ~66,000 | 660M |
| **Maximum (with all features)** | ~150,000 | 1.5B |

## **Summary**

| Metric | Value |
|--------|-------|
| **Currently extracted** | ~270 parameters/sample |
| **Should extract** | ~1,400 parameters/sample |
| **Maximum possible** | ~66,000 parameters/sample |
| **Your data capacity** | 96×14×10000 = 13.44M complex values |
| **Theoretical information** | 26.88M real values |


