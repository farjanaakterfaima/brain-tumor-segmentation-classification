
# BRISC Dataset Preprocessing Report

## 1. Dataset Information

Dataset: BRISC 2025 - Brain Tumor MRI Dataset

Task: Brain Tumor Segmentation

Image type: T1-weighted MRI

Preprocessed image size: 256 x 256 pixels

## 2. Dataset Split

| Split | MRI Images | Segmentation Masks |
|---|---:|---:|
| Training | 3933 | 3933 |
| Testing | 860 | 860 |
| Total | 4793 | 4793 |

## 3. Preprocessing Operations

### 3.1 Image Conversion
- MRI images were converted to RGB format.

### 3.2 Image Resizing
- Target size: 256 x 256 pixels.
- Aspect ratio was preserved.
- Padding was added to fit the target dimensions.
- Bilinear interpolation was used for MRI images.

### 3.3 Mask Processing
- Masks were converted to grayscale.
- A provisional threshold of 128 was applied:
  - Pixel values >= 128 were converted to 255.
  - Pixel values < 128 were converted to 0.
- Nearest Neighbor interpolation was used for mask resizing.
- Zero padding was applied.

### 3.4 Output Format
- Preprocessed MRI images: PNG, RGB.
- Preprocessed masks: PNG, grayscale binary.
- Image dimensions: 256 x 256.
- Mask pixel values: 0 and 255.

## 4. Preprocessing Results

### Training Dataset
- Source images: 3933
- Successfully processed: 3933
- Missing masks: 0
- Failed files: 0

### Testing Dataset
- Source images: 860
- Successfully processed: 860
- Missing masks: 0
- Failed files: 0

## 5. Output Verification

- Training image count: 3933
- Training mask count: 3933
- Testing image count: 860
- Testing mask count: 860
- Missing training masks: 0
- Extra training masks: 0
- Missing testing masks: 0
- Extra testing masks: 0

Ten training image-mask pairs and ten testing image-mask pairs
were checked for dimensions and mask pixel values.

All inspected samples had matching 256 x 256 dimensions.
Their mask values were 0 and 255.

Note: Sample verification does not constitute a complete
pixel-level validation of every output file.

## 6. Important Methodological Note

The threshold value of 128 was used provisionally because the
dataset README describes binary segmentation masks but does not
specify an exact grayscale threshold.

The threshold must be confirmed against the dataset's original
mask encoding or dataset authors' documentation before making
a final scientific claim about mask interpretation.

## 7. Output Directory

BRISC_preprocessed_256_v2/
    train/
        images/
        masks/
    test/
        images/
        masks/

## 8. Data Integrity

The original BRISC dataset was kept unchanged.
Preprocessed files were saved in a separate output directory.

The original training and testing split was preserved.

## 9. Completion Status

Training preprocessing: Completed
Testing preprocessing: Completed
Filename matching: Completed
Sample output verification: Completed

Documentation generated: 2026-11-03

