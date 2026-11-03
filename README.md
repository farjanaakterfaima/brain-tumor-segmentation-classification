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



# MOTUM Dataset Preprocessing Report

## 1. Dataset Overview

The MOTUM dataset was used as a secondary multi-parametric MRI dataset for the brain tumor segmentation and classification research project.

The dataset contains four MRI modalities:

- FLAIR
- T1
- T1CE
- T2

A total of 64 subjects with available MRI volumes were processed. Three additional clinical records did not have corresponding original MRI volumes.

## 2. Dataset Integrity Verification

The original MRI volumes and segmentation masks were checked for:

- File availability and readability
- Matching image dimensions
- Matching affine transformations
- Consistent image orientation
- Valid numerical values

All 64 MRI subjects had four available modalities and two corresponding segmentation masks.

The original MRI volumes and masks were found to have matching spatial dimensions and affine transformations within each subject.

## 3. Binary Mask Preparation

Two separate segmentation masks were processed:

- FLAIR mask (Label 1)
- T1CE mask (Label 2)

The original mask labels were converted into binary masks using:

`(original_mask > 0).astype(np.uint8)`

The original mask files were not modified.

A total of 128 binary masks were generated successfully:

| Mask type | Number |
|---|---:|
| FLAIR binary masks | 64 |
| T1CE binary masks | 64 |
| Total | 128 |

All generated masks were verified to contain valid binary labels (0 and 1).

## 4. MRI Normalization

Z-score normalization was applied separately to each MRI modality for each subject.

The normalization formula was:

\[
I_{norm} = \frac{I-\mu}{\sigma+\epsilon}
\]

Where:

- \(I\) = Original MRI intensity
- \(\mu\) = Mean intensity of non-zero voxels
- \(\sigma\) = Standard deviation of non-zero voxels
- \(\epsilon\) = Small numerical constant

Background voxels were preserved as zero.

A total of 256 normalized MRI volumes were generated.

| Modality | Normalized volumes |
|---|---:|
| FLAIR | 64 |
| T1 | 64 |
| T1CE | 64 |
| T2 | 64 |
| **Total** | **256** |

All 256 normalized volumes passed the numerical integrity verification.

## 5. Subject-wise Dataset Splitting

The dataset was divided at the subject level to prevent slices from the same subject from appearing in multiple subsets.

A fixed random seed (42) was used.

| Subset | Number of subjects |
|---|---:|
| Training | 44 |
| Validation | 10 |
| Testing | 10 |
| **Total** | **64** |

The split was saved in `subject_split.json`.

## 6. 2D Slice Extraction

The normalized MRI volumes were converted into 2D slices along the third volume axis.

For each slice, the four MRI modalities were stacked in the following order:

1. FLAIR
2. T1
3. T1CE
4. T2

The corresponding FLAIR and T1CE binary masks were stored separately.

Each slice was saved in compressed NumPy (`.npz`) format to preserve floating-point MRI intensity values and associated mask data.

### Extracted Slice Statistics

| Subset | Number of slices |
|---|---:|
| Training | 929 |
| Validation | 225 |
| Testing | 216 |
| **Total** | **1,370** |

## 7. Final Quality Verification

All extracted slices were checked for:

- Correct four-channel MRI array shape
- Matching image and mask dimensions
- Valid binary mask labels
- Absence of NaN and infinite values

The final verification results were:

| Verification | Result |
|---|---:|
| Total slices checked | 1,370 |
| Expected slices | 1,370 |
| Failed slices | 0 |
| Errors | 0 |

All 1,370 extracted slices passed the implemented verification checks.

## 8. Output Directory Structure

The processed dataset is organized as follows:

```text
BRAIN TUMOR PROJECT DATASET/
│
├── MOTUM_normalized/
│   ├── sub-0001/
│   ├── sub-0002/
│   ├── ...
│   └── subject_split.json
│
├── MOTUM_binary_masks/
│   ├── sub-0001/
│   ├── sub-0002/
│   └── ...
│
└── MOTUM_2D_slices/
    ├── train/
    ├── validation/
    └── test/
```

## 9. Important Limitations and Considerations

1. The non-zero voxel region was used as a practical approximation of the brain region during normalization. It should not be considered a perfect anatomical brain mask.

2. Three subjects (`sub-0025`, `sub-0037`, and `sub-0039`) had T1CE masks with label 1 instead of the expected label 2. The original labels were preserved before binary conversion.

3. The extracted 2D slices have not yet undergone a complete clinical or visual segmentation-quality assessment.

4. The subject split has not yet been evaluated for clinical class balance.

5. The number of extracted slices does not represent the number of independent patients. Model evaluation must remain subject-wise.

6. MOTUM's clinical labels and segmentation annotations must be examined separately before defining a unified classification task with BRISC.

## 10. Conclusion

The MOTUM dataset preprocessing pipeline was successfully completed for 64 subjects.

The process generated 256 normalized MRI volumes, 128 binary segmentation masks, and 1,370 aligned 2D MRI slices across the training, validation, and testing subsets.

All extracted slices passed the implemented numerical and structural verification checks without any reported failures.

The processed MOTUM dataset is now organized for subsequent research and model-development experiments, subject to further clinical-label assessment and segmentation-quality review.

## 11. Dataset Reference

MOTUM: A Multi-Center, Multi-Parametric MRI Dataset of Primary and Secondary Brain Tumors.

Scientific Data (2025).

DOI: https://doi.org/10.1038/s41597-024-03634-0

Official repository: https://github.com/hongweilibran/MOTUM
