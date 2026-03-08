# SA-MedGAN: Self-Attention Progressive GAN for High-Fidelity Medical Image Synthesis 

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active_Research-success)

## 📌 Overview
[cite_start]In the rapidly advancing field of medical imaging, the scarcity of authentic and high-quality datasets often hinders the training of robust machine learning models[cite: 3, 14]. [cite_start]**SA-MedGAN** is a novel generative adversarial framework designed to synthesize highly realistic, high-resolution (up to 1024x1024) CT and MRI scans[cite: 57, 130]. 

By integrating a **Self-Attention (SA)** mechanism into a Progressive Growing GAN (ProGAN) architecture, this project ensures the network models long-range spatial dependencies. [cite_start]This approach preserves global anatomical symmetry and structural integrity—crucial for medical diagnostics—while progressively refining micro-textures during the synthesis process[cite: 4, 82].

## ✨ Key Features & Novel Contributions
* [cite_start]**Self-Attention Injection:** Overcomes the localized receptive field limitations of standard convolutions, ensuring macro-anatomical correctness[cite: 42].
* [cite_start]**Progressive Resolution (4x4 to 1024x1024):** Stabilizes training by starting at low resolution and incrementally adding details[cite: 58, 88].
* [cite_start]**WGAN-GP Optimization:** Utilizes Wasserstein GAN with Gradient Penalty (WGAN-GP) to prevent mode collapse and ensure stable adversarial training[cite: 5, 89].
* [cite_start]**Mixed Precision Training:** Implements `torch.amp` for computational efficiency and faster convergence on modern GPUs[cite: 5].
* [cite_start]**Rigorous Evaluation:** Automated benchmarking for calculating Fréchet Inception Distance (FID), Inception Score (IS), and Structural Similarity Index (SSIM)[cite: 65, 100].

## 🧠 Model Architecture Highlights
[cite_start]The framework utilizes **WSConv2d** (Weight-Scaled Convolutions) to ensure equalized learning rates across all layers and **PixelNorm** to prevent signal magnitude escalation[cite: 4]. [cite_start]During training, a **fade-in parameter ($\alpha$)** is used to smoothly transition between resolution steps, preventing training shocks[cite: 4].



### Architecture Summary:
1. [cite_start]**Generator:** Progressively grown from low to high resolution, using WSConv2d layers and PixelNorm for stable upsampling[cite: 4]. 
2. [cite_start]**Discriminator/Critic:** Mirrors the generator to ensure effective adversarial training and calculates feature scores[cite: 4, 84].
3. [cite_start]**Self-Attention:** Embedded at the 64x64 resolution stage to maintain global structural integrity[cite: 42].

## 📊 Quantitative Results
[cite_start]*Metrics recorded after a full 110-epoch training cycle on dual NVIDIA T4 GPUs[cite: 126, 155].*

| Metric | SA-MedGAN (Ours) | Baseline ProGAN | Description |
| :--- | :---: | :---: | :--- |
| **FID ↓** | `[PLACEHOLDER]` | `[Baseline FID]` | [cite_start]Feature distance (Lower is better)[cite: 101]. |
| **IS ↑** | `[PLACEHOLDER]` | `[Baseline IS]` | [cite_start]Image diversity/clarity (Higher is better)[cite: 105]. |
| **SSIM ↑** | `[PLACEHOLDER]` | `[Baseline SSIM]` | [cite_start]Structural similarity (Closer to 1.0 is better)[cite: 149]. |

## 🚀 Getting Started

### 1. Implementation Code
The complete implementation, including the model architecture, training logic, and evaluation metrics, is available in the provided Jupyter Notebook:
* **Notebook File:** `progan.ipynb` (Contains the modular Cell-by-Cell breakdown).

### 2. Pre-trained Models
Due to high resolution and model size, the trained weights (`g_sa.pth` and `c_sa.pth`) are hosted on Kaggle.
* **Kaggle Model URL:** `[PLACEHOLDER: Insert your Kaggle Model Link here]`

### 3. Dataset Preparation
[cite_start]The framework is trained on real CT and MRI scans[cite: 72]. To use your own data, structure it for `torchvision.datasets.ImageFolder`:
```text
/data/
    /kidney/
        img1.png
        img2.png
