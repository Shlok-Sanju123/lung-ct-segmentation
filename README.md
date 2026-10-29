Lung CT Segmentation
I developed a lung segmentation workflow in 3D Slicer 5.8.1 to extract the lungs from a chest CT scan and evaluate the result against a reference mask.
Workflow
- Generated an initial lung mask using CT intensity thresholding.
- Applied a body-mask constraint and connected-component cleanup to reduce unwanted regions.
- Smoothed the resulting mask and inspected it across axial, coronal, sagittal, and 3D views.
- Used the Slicer Python console to calculate overlap metrics against the reference segmentation.
Results
Metric	Score
Dice coefficient	0.949
Precision	0.9887
Recall	0.9124


These metrics are from a single scan and should not be interpreted as evidence of performance on unseen scans.
Tools
- 3D Slicer 5.8.1
- Python (within the Slicer console)
Repository contents
- evidence/ — screenshots of the workflow and results
- results/metrics.csv — final evaluation metrics
- docs/PROJECT_REPORT.md — method, interpretation, and limitations
The CT volume, reference mask, and saved .mrb scene are not included. The screenshots document the workflow; a fully reproducible pipeline would also require the exact processing script, parameter values, and reference-mask provenance.
