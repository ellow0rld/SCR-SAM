# SCR-SAM: Spatial Continuity Regularisation for Hardware-Efficient 3D Medical Segmentation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/1201725749.svg)](https://doi.org/10.5281/zenodo.19426119)

This repository contains the official implementation of **SCR-SAM**, a lightweight longitudinal "tethering" strategy designed to bridge the dimensionality gap in 2D Vision Foundation Models (VFMs) for 3D medical volumes. 

By applying **Spatial Continuity Regularisation (SCR)** and **LoRA** adaptation, our method reduces Average Symmetric Surface Distance (ASSD) by **79%** while maintaining a peak training VRAM of only **12.70 GB** on standard Tesla T4 hardware.

---

## 🚀 Key Features
* **Hardware Efficient:** Optimized for consumer-grade GPUs (16GB VRAM).
* **Anatomically Plausible:** Eliminates "staircase artifacts" and "spatial jitter" in 3D reconstructions.
* **Foundation Model Native:** Leverages the Segment Anything Model (SAM) zero-shot weights.

## 📂 Repository Structure
* `SCR on KiTS.ipynb`: Full pipeline for the KiTS 19 dataset (Data Loading, SCR Training, and Evaluation).
* `SCR on BRaTS.ipynb`: Evaluation and Inference pipeline for the BraTS 2021 dataset.
* `README.md`: Usage guidelines and dataset links.

---

## 📊 Datasets & Pre-trained Weights

To replicate our findings, please download the datasets and weights from the following sources:

| Dataset | Type | Source Link | Pre-trained Weights (Kaggle) |
| :--- | :--- | :--- | :--- |
| **KiTS 19** | CT | [Kaggle Dataset](https://www.kaggle.com/datasets/user123454321/kits19-1) | [SCR-SAM KiTS Weights](https://www.kaggle.com/datasets/madhushreearavindan/sam3-trained-on-kits-scr-lora) |
| **BraTS 2021** | MRI | [Kaggle Dataset](https://www.kaggle.com/datasets/dschettler8845/brats-2021-task1) | [SCR-SAM BraTS Weights](https://www.kaggle.com/datasets/madhushreearavindan/sam3-trained-on-brats-scr-lora) |

---

## 🛠️ Usage Guidelines

### 1. Training (KiTS 19)
The `KiTS_SCR_LoRA.ipynb` notebook provides a comprehensive end-to-end implementation. 
* To train from scratch, ensure your data directory matches the paths in the notebook.
* The script utilizes **LoRA (Rank=4)** and our custom **SCR Loss** to ensure inter-slice continuity.

### 2. Adaptation for BraTS 2021
While the BraTS notebook focuses on evaluation, the training logic is identical to the KiTS pipeline. To train on BraTS:
1. Use the training loop architecture from the KiTS notebook.
2. Update the `DataLoader` to handle the 4-channel MRI modality ($T1, T1ce, T2, FLAIR$) used in BraTS 2021.
3. Adjust the intensity normalization to match MRI characteristics.

### 3. Evaluation & Inference
Use the respective notebooks to load the pre-trained weights and generate qualitative results. The notebooks include "Smoothness Checks" for Coronal views to verify 3D consistency.

---

## 🛠️ Requirements
* Python 3.8+
* PyTorch 1.10+
* Segment Anything Model (SAM)
* PEFT (for LoRA)
* SimpleITK / Nibabel (for .nii.gz files)
