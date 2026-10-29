# Project Report: Chest CT Lung Segmentation

## 1. Objective

The goal was to generate a binary lung mask from a chest CT volume using 3D Slicer, refine the threshold-derived mask, inspect it in axial/coronal/sagittal and 3D views, and compare it with a reference mask.

## 2. Software and data

- **Software:** 3D Slicer 5.8.1.
- **Input volume node:** `LungCTAnalyzerChestCT`.
- **Initial segment:** `Threshold_lungs`.
- **Refined segments:** `Cleaned lung prediction` and `Smoothed lung prediction`.
- **Reference:** a reference mask already loaded in the working scene. Its origin and licensing should be documented before public redistribution.

The CT and reference files themselves are not included in this documentation bundle.

## 3. Method

### 3.1 Threshold segmentation

A threshold-based mask was created from the CT intensities. This is a useful baseline because air-filled lung regions generally have low CT attenuation. However, a simple threshold may also select external air, airways, and other low-density regions, while missing some lung voxels affected by tissue, vessels, or partial-volume effects.

### 3.2 Mask restriction and cleanup

The mask was refined using a body-mask constraint and connected-component/island operations. A split-islands operation produced 17 segments during exploration and was undone; that intermediate result was not retained as the final segmentation. The cleanup process aimed to reduce disconnected false positives outside the lungs.

### 3.3 Smoothing

A smoothed candidate, named `Smoothed lung prediction`, was created and inspected in the three orthogonal slice views and the 3D view. Smoothing reduces small boundary irregularities, but should always be checked visually because excessive smoothing can erase thin structures or alter the anatomical boundary.

### 3.4 Evaluation

The Slicer Python console displayed the following final values:

| Metric | Value |
|---|---:|
| Dice coefficient | 0.949 |
| Precision | 0.9887 |
| Recall | 0.9124 |

Definitions:

- **Dice:** \(2TP/(2TP+FP+FN)\)
- **Precision:** \(TP/(TP+FP)\)
- **Recall:** \(TP/(TP+FN)\)

Here, TP is the number of overlapping foreground voxels, FP is the number of predicted foreground voxels absent from the reference, and FN is the number of reference foreground voxels missed by the prediction.

The values are transcribed from the final console screenshot. They should be recomputed from the saved prediction and reference masks before formal publication or use in a graded/research report.

## 4. Interpretation

A Dice coefficient of 0.949 indicates substantial voxel overlap for this case. Precision of 0.9887 indicates that the predicted foreground is highly consistent with the reference, while recall of 0.9124 indicates that a portion of the reference foreground remains unsegmented. The precision/recall balance is consistent with a relatively conservative mask.

These metrics do not identify where the errors occur. A slice-by-slice review and a false-positive/false-negative overlay would provide additional useful evidence.

## 5. Deliverable

The scene was saved in 3D Slicer as `2026-10-30-Scene.mrb` (Medical Reality Bundle). The screenshot `evidence/07_saved_project_in_downloads.png` documents the saved bundle alongside the CT and reference-mask files.

## 6. Limitations and next improvements

1. Record the exact threshold interval and all cleanup/smoothing parameters.
2. Preserve a standalone Python script or Slicer script that recreates the workflow from input files.
3. Document the reference mask's source, annotation method, and permission to share.
4. Recompute metrics after reopening the saved scene to confirm reproducibility.
5. Inspect false-positive and false-negative regions on multiple slices.
6. Evaluate on additional scans before making any general performance claim.

## 7. Conclusion

A threshold-based lung segmentation was refined using mask restriction, island cleanup, and smoothing. The final recorded metrics for the evaluated scan were Dice 0.949, precision 0.9887, and recall 0.9124. The Slicer scene was saved for later inspection. This is a promising single-case image-processing result, not a clinically validated segmentation system.
