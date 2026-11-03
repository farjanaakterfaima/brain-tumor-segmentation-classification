# MOTUM Dataset Preprocessing Report

## 1. Dataset Overview
- Total subjects: 64
- MRI modalities: FLAIR, T1, T1CE, T2

## 2. Binary Mask Preparation
- FLAIR binary masks: 64
- T1CE binary masks: 64
- Total binary masks: 128

## 3. MRI Normalization
- Total normalized MRI volumes: 256
- Failed files: 0

## 4. Subject-wise Dataset Split

| Split | Subjects |
|---|---:|
| Training | 44 |
| Validation | 10 |
| Testing | 10 |
| Total | 64 |

## 5. 2D Slice Extraction

| Split | Slices |
|---|---:|
| Training | 929 |
| Validation | 225 |
| Testing | 216 |
| Total | 1370 |

## 6. Final Verification
- Total slices checked: 1370
- Failed slices: 0
- Errors: 0

## 7. Conclusion
MOTUM preprocessing was completed for 64 subjects.
A total of 256 normalized MRI volumes, 128 binary masks,
and 1370 aligned 2D slices were generated.

All extracted slices passed the implemented structural
and numerical verification checks.

## 8. Dataset Reference
DOI: https://doi.org/10.1038/s41597-024-03634-0

Official repository:
https://github.com/hongweilibran/MOTUM
