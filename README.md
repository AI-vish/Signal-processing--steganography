# 🖼️ Image Steganography using DWT and SVD  

### _A Hybrid Frequency-Domain Approach for Secure Image Embedding_  
**Authors:** Ranjith Balu, Vishal Thangakumar, Thenmozhi Dharshini, S. Padmavathi, R. Sujee  
**Affiliation:** Amrita Vishwa Vidyapeetham, Coimbatore, India  
**Published in:** Springer – Lecture Notes in Networks and Systems (2025)  

---

## 📘 Project Overview

This repository contains the **implementation code and experiment scripts** for the paper  
**“Image Steganography using Discrete Wavelet Transform (DWT) and Singular Value Decomposition (SVD)”**,  
which presents a robust and high-fidelity technique for **secure data embedding within images**.

The method leverages the **multi-resolution analysis** capability of DWT and the **matrix precision** of SVD to achieve:
- High imperceptibility of embedded data  
- Strong robustness against attacks and compression  
- Preservation of image quality (high PSNR, SSIM)  
- Secure and reversible extraction of hidden information  

Our approach improves upon traditional methods like **Least Significant Bit (LSB)** embedding by moving the process to the **frequency domain**, achieving **better resistance to steganalysis** and **compression artifacts**.

---

## 🎯 Objectives

- Enable **secure communication** by embedding sensitive information (medical scans, defense data, legal records, etc.) inside digital images.
- Maintain the **visual integrity** of the cover image while increasing embedding capacity.
- Develop a **robust, scalable**, and **quantitatively verifiable** image steganography technique.

---

## ⚙️ Methodology

### 🔹 Core Idea
The system combines **Discrete Wavelet Transform (DWT)** and **Singular Value Decomposition (SVD)**:
- **DWT** decomposes the image into low- and high-frequency subbands (LL, LH, HL, HH).  
- **SVD** is then applied to the DWT coefficients to obtain singular matrices (**U, S, Vᵗ**).  
- The **S-matrix** is modified using the secret image's singular values, controlled by a scaling factor `α`.  
- Inverse transforms (IDWT and inverse SVD) reconstruct the final **stego image**.

This dual-domain hybridization enhances robustness and invisibility simultaneously.

---

## 🧩 Implementation Workflow

### 🧠 Encoding Phase
1. **Input:** Cover image (carrier) and secret image (to embed).  
2. **Split:** Separate RGB channels.  
3. **DWT:** Apply Daubechies-20 (`db20`) wavelet transform on each channel.  
4. **SVD:** Perform SVD on DWT coefficients for both cover and secret images.  
5. **Embedding:** Modify singular values using  
   \[
   S_{new} = S_{cover} + \alpha \times S_{secret}
   \]
   where `α` is the scaling factor (controls embedding strength).
6. **Reconstruct:** Combine using inverse SVD and IDWT to obtain the **stego image**.

### 🔍 Decoding Phase
1. **Input:** Stego image and original cover image.  
2. **DWT & SVD:** Apply DWT and SVD on both to extract singular values.  
3. **Extraction:** Reverse embedding using  
   \[
   S_{secret} = \frac{S_{stego} - S_{cover}}{\alpha}
   \]
4. **Reconstruction:** Apply inverse transforms to recover the **hidden secret image**.

---

## 🧪 Experimental Setup

| Parameter | Details |
|------------|----------|
| OS | Windows 11 |
| Processor | Intel Core i5 |
| RAM | 16 GB |
| Wavelet Used | Daubechies 20 (`db20`) |
| Scaling Factor (α) | Optimal ≈ 0.01 |
| Libraries | OpenCV, NumPy, PyWavelets, Matplotlib |

Performance was evaluated across multiple combinations of image sizes (small-to-large and vice versa) to test adaptability and fidelity.

---

## 📊 Evaluation Metrics

| Metric | Description | Desired Outcome |
|---------|--------------|----------------|
| **SQNR** | Signal-to-Quantization-Noise Ratio | High (>45 dB) |
| **PSNR** | Peak Signal-to-Noise Ratio | High (>47 dB) |
| **SSIM** | Structural Similarity Index | ≈ 0.999 |
| **CC** | Correlation Coefficient | ≈ 1 |

### 🧾 Results Summary

| Sample | SQNR (dB) | PSNR (dB) | SSIM | CC |
|:-------:|:----------:|:----------:|:------:|:----:|
| 1 | 45.36 | 49.95 | 0.9976 | 0.9999 |
| 4 | 49.51 | 55.07 | 0.9997 | 1.0000 |
| 8 | 47.94 | 50.76 | 0.9998 | 0.9999 |
| **Avg.** | **>45** | **>50** | **≈0.999** | **≈1.0** |

✅ **Inference:** The proposed DWT–SVD model maintains exceptional image fidelity and resistance to detection, even under transformations and compression.

---

## 🧮 Key Equations

**Signal-to-Quantization-Noise Ratio (SQNR):**
\[
SQNR = 10 \log_{10} \frac{\sum I(i)^2}{\sum (I(i) - I'(i))^2}
\]

**Peak Signal-to-Noise Ratio (PSNR):**
\[
PSNR = 10 \log_{10} \frac{MAX_I^2}{MSE}
\]

**Structural Similarity Index (SSIM):**
\[
SSIM(x,y) = [L(x,y) \cdot C(x,y) \cdot S(x,y)]
\]

**Correlation Coefficient (CC):**
\[
CC = \frac{\sum (X_i - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum (X_i - \bar{X})^2 \sum (Y_i - \bar{Y})^2}}
\]

---

## 🧰 Tech Stack

- **Python 3.10+**  
- **OpenCV** – Image processing & matrix manipulation  
- **NumPy** – Numerical operations  
- **PyWavelets (pywt)** – Discrete Wavelet Transform  
- **Matplotlib / Seaborn** – Visualization  
- **scikit-image** – Evaluation metrics (PSNR, SSIM)

---


---

## 🧭 How to Run

```bash
# Clone the repository
git clone https://github.com/<your-username>/Image-Steganography-DWT-SVD.git
cd Image-Steganography-DWT-SVD

# Install dependencies
pip install -r requirements.txt
