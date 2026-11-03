# Explainable Hybrid Swin Transformer and EfficientNet for Multi-Source MRI-Based Brain Tumor Segmentation and Classification

## Project Overview

This project focuses on developing a software-based brain tumor segmentation and classification system using deep learning and Explainable AI (XAI).

The proposed approach combines Swin Transformer and EfficientNet architectures to explore hybrid feature extraction for MRI-based brain tumor analysis.

## Current Progress

**Phase 1: BRISC Dataset Preprocessing — Completed**

The BRISC 2025 dataset was used to begin the preprocessing phase.

### Dataset Summary

| Dataset Split | MRI Images | Segmentation Masks |
|---|---:|---:|
| Training | 3,933 | 3,933 |
| Testing | 860 | 860 |
| **Total** | **4,793** | **4,793** |

### Preprocessing Methods

- MRI image conversion to RGB.
- Image resizing to 256 × 256 pixels.
- Aspect-ratio preservation with padding.
- Bilinear interpolation for MRI images.
- Grayscale conversion for segmentation masks.
- Nearest Neighbor interpolation for masks.
- Binary mask conversion using a provisional threshold of 128.

**Important:** The threshold of 128 is provisional. The BRISC dataset README describes binary masks but does not specify an exact grayscale threshold. This needs further confirmation.

### Verification Results

- All 3,933 training image-mask pairs were processed.
- All 860 testing image-mask pairs were processed.
- No missing masks were found.
- No extra masks were found.
- Ten training and ten testing samples were inspected.
- Inspected images and masks had matching 256 × 256 dimensions.

## Project Directory Structure

```text
brain-tumor-segmentation-classification/
│
├── README.md
│
├── BRISC_preprocessing.ipynb
│
└── BRISC_preprocessing_report.md
```

## Technologies

- Python
- Google Colab
- NumPy
- Pillow (PIL)
- Matplotlib
- PyTorch (planned for model development)

## Planned Workflow

1. BRISC and MOTUM dataset preparation.
2. MRI preprocessing.
3. Brain tumor segmentation.
4. Hybrid Swin Transformer and EfficientNet feature extraction.
5. Feature fusion and classification.
6. Explainable AI visualization.
7. Model evaluation.
8. Software application development.

## Repository Purpose

This repository documents the code, preprocessing procedures, and development progress of the research project.

**Note:** The MRI datasets are not included in this repository. Please obtain the datasets from their respective official sources and follow their usage and citation requirements.

## Research Status

Currently, BRISC preprocessing is completed. Further dataset preparation, model development, evaluation, and software implementation are planned.
