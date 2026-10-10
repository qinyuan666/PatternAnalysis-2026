# HipMRI 2D segmentation: U-Net versus Improved U-Net

This individual COMP3710 project investigates whether an Improved U-Net reduces
prostate boundary errors compared with a standard 2D U-Net at an acceptable GPU
cost. The selected task is HipMRI segmentation, with a Normal-difficulty main
model. The immediate deliverable is a one-page midpoint feasibility review and
reproducible preliminary engineering evidence, not a completed clinical study.

## Planned investigation

- Dataset: the course-provided HipMRI 2D NIfTI slices under
  `/home/groups/comp3710/HipMRI_Study_open/keras_slices_data`.
- Baseline: a standard encoder-decoder 2D U-Net with skip connections [1].
- Main model: a 2D adaptation of the Improved U-Net in Isensee et al. [2], using
  residual context blocks, instance normalization and deep supervision.
- Compare both on identical patient-disjoint splits and training budgets.
- Report per-class Dice/IoU, patient-level results, boundary errors, parameter
  count, peak training GPU memory and batch-one inference latency.
- Analyse 3–5 actual failure cases before making an evidence-based recommendation.

## Data status

Real HipMRI data and its label dictionary have not yet been provided. Patient IDs,
prostate label values, slice ordering and physical spacing must be audited before
real-data training. No real-data accuracy or Dice result is claimed.

The example CSV contains fictitious filenames. Use an explicit manifest rather
than guessing patient IDs from filenames. Local manifests, images and weights
must not be committed. Curated synthetic diagnostic figures may be committed
when clearly labelled as synthetic.

## Reproducibility

Dependency versions are recorded in `requirements.txt`. Training and prediction
commands and measured results will be documented as the midpoint experiment is
completed. The code will use an explicit synthetic mode for infrastructure checks;
such checks do not establish medical segmentation performance.

## Artificial Intelligence Usage Disclosure

OpenAI Codex assisted with interpreting the assessment, setting up the GitHub fork,
planning the project and drafting code/documentation. Verification includes review
against the cited papers, patient-leakage and label-handling tests, forward/backward
checks, checkpoint reload checks and measured resource experiments. The student
must personally inspect, understand and verify the submission and keep this
disclosure accurate. No clinical experiment or tutor check-off is claimed.

## References

1. Ronneberger, Fischer and Brox (2015). *U-Net: Convolutional Networks for
   Biomedical Image Segmentation*. https://arxiv.org/abs/1505.04597
2. Isensee et al. (2018). *Brain Tumor Segmentation and Radiomics Survival
   Prediction: Contribution to the BRATS 2017 Challenge*.
   https://arxiv.org/abs/1802.10508
3. Course assessment: `COMP3710_Report_2026_draft_v2.2.pdf`, Sections 2.2 and 3.
