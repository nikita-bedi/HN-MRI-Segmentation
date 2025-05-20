 # Tumor Segmentation from Head & Neck MRI Using Deep Learning

This project explores the use of deep learning for 2D semantic segmentation of gross tumor volumes in T2-weighted MRI scans of head and neck cancer patients. The goal was to build and evaluate a complete computer vision pipeline, from preprocessing to model training and evaluation, with a focus on managing class imbalance and limited labeled data — both common challenges in medical imaging.

---

## Motivation

- Tumor segmentation from MRI is a critical step in radiotherapy planning and longitudinal assessment.
- Manual segmentation is time-consuming and varies between clinicians.
- This project aims to evaluate whether convolutional neural networks (CNNs), especially U-Net variants, can segment tumors (GTVp and GTVn) frame-by-frame in a reliable way.
- The work was done independently as a graduate computer vision final project.

---

## Dataset Overview

- Source: [HNTSMRG2024](https://hntsmrg24.grand-challenge.org/)
- Patients: 150 (oropharyngeal cancer and unknown primary)
- Imaging: Pre-RT and mid-RT T2-weighted MRIs
- Labels: Multi-class masks with 3 values:
  - 0 = background
  - 1 = primary tumor (GTVp)
  - 2 = metastatic lymph nodes (GTVn)

---

## Data Preparation

- Converted 3D `.nii.gz` scans into axial 2D slices.
- All slices resized to `256×256` to standardize input size.
- Intensity normalization (z-score) applied per volume.
- Extracted and saved over **25,000 slice-level `.pt` files** for efficient loading.
- Stratified patient-level split into train/val/test sets.
- Empty masks identified and optionally removed during "tumor-only" training phase.

---

## Model Architectures

Implemented and evaluated several convolutional architectures:

| Model             | Key Feature                  |
|------------------|------------------------------|
| **U-Net**         | Baseline encoder-decoder     |
| **Attention U-Net** | Gating for skip connections  |
| **U-Net++**       | Nested dense skip paths       |
| **Mamba U-Net**   | Residual state-space blocks   |
| **Pretrained U-Net** | First trained on tumor-only data |

Each model was tested with:
- **Cross-Entropy Loss**
- **Dice Loss**
- **Combined Loss (Dice + CE)**

---
## Environment

- Python 3.11
- PyTorch, TorchIO, scikit-learn
- Jupyter (Google Colab Pro)
- Dataset: ~15 GB MRI scans + masks

---

## Notes

This project was developed independently and serves as a demonstration of initiative, practical ML skills, and interest in applying computer vision to real-world medical problems. Results were limited by class imbalance and lack of 3D spatial context — future work will explore multi-slice or full 3D approaches.

---

## Author

**Nikita Bedi**  
Graduate Computer Vision Final Project  
Spring 2025 
Harvard Extension School
