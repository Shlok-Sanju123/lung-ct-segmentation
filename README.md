# Lung CT Segmentation

A lung segmentation workflow developed in **3D Slicer 5.8.1** to extract lung regions from chest CT scans and evaluate segmentation accuracy against a reference mask.

## Workflow

- **Thresholding:** Generated an initial lung mask using CT intensity values.
- **Mask Refinement:** Applied a body-mask constraint and connected-component analysis to remove unwanted regions.
- **Smoothing:** Refined the segmentation to reduce noise and improve continuity.
- **Visualization:** Inspected results across axial, coronal, sagittal, and 3D views.
- **Evaluation:** Used Python in the Slicer console to calculate overlap metrics against a reference segmentation.

## Results

| Metric | Score |
|:--|--:|
| Dice Coefficient | **0.9490** |
| Precision | **0.9887** |
| Recall | **0.9124** |

*Metrics were obtained from a single CT scan and do not establish generalization to unseen scans.*

## Tools Used

- 3D Slicer 5.8.1
- Python
- NumPy

## Repository Contents

- `evidence/` — Screenshots documenting the workflow and results
- `results/metrics.csv` — Final evaluation metrics
- `docs/PROJECT_REPORT.md` — Methodology, interpretation, and limitations

## Limitations

This project was evaluated on a single scan. The CT volume, reference mask, and saved `.mrb` scene are not included in this repository. Reproducing the evaluation requires the corresponding input data and segmentation masks.

