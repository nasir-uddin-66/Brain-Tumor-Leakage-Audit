# Data Leakage and Unverified Provenance in Public Brain Tumor MRI Datasets: A Systematic Audit


This repo audits internal train/test leakage and cross-dataset overlap across seven public brain tumor MRI datasets, and reports a controlled experiment comparing naive (image-level) vs. patient-level splitting on the Figshare dataset.

## What's here

- `notebook/` — the full pipeline (`brain-tumor-leakage-audit.ipynb`): manifest construction, internal leakage detection, cross-dataset detection, manual validation, backbone sensitivity check, de-duplication correction, and the patient-split experiment.
- `manifest/` — the image manifest (`manifest.csv`: dataset, split, label, hashes) for all 34,525 images used in this study.
- `checksums/` — `dataset_aggregate_sha256.csv`, aggregate SHA-256 checksums per dataset, to confirm you downloaded the same version.
- `results/` — all output CSVs (see below).
- `manual validation/` — rated validation sheets and the page images shown to the raters (see below).
- `figures/` — the figures used in the paper (see below).

### `results/`

| File(s) | Contents |
|---|---|
| `SUMMARY_internal_leakage.csv` | Per dataset/eval split: counts and % of eval images that are true duplicates (A), adjacent slices (B), or false alarms (C) relative to the training set. |
| `internal_leakage_final.csv` | Final per-pair internal leakage table. |
| `internal_embeddings_<dataset>.csv` | Embedding-based internal similarity pairs for BDNeuro-HIra, BRISC, Masoud Nickparvar and Shartaj. |
| `SUMMARY_cross_dataset.csv` | Per source→target dataset pair: source size, confirmed matches, and % overlap. |
| `cross_<A>__vs__<B>.csv` | Matched image pairs for each cross-dataset comparison (17 pairs). |
| `backbone_sensitivity_check.csv` | Cross-dataset overlap % under ResNet50 vs. DenseNet121 embeddings, with the absolute difference. |
| `dedup_correction_check.csv` | Test performance on the full eval set vs. the leakage-removed ("clean") set, with z-tests for the difference. |
| `dedup_per_class_accuracy.csv` | Per-class accuracy on the full vs. clean eval sets. |
| `naive_per_class_metrics.csv`, `patient_per_class_metrics.csv` | Per-class metrics for the naive (image-level) vs. patient-level split experiment on Figshare. |

### `manual validation/`

Human checks of the automatic similarity threshold. Each pair was rated independently by two raters blind to the similarity score.

| File | Pairs | Description | Rater agreement |
|---|---|---|---|
| `MANUAL_VALIDATION_SHEET_RATED.csv` | 75 | Cross-dataset pairs used to check the similarity threshold | 75 / 75 |
| `MANUAL_VALIDATION_SHEET_BELOW_THRESHOLD_RATED.csv` | 50 | Cross-dataset pairs just below the threshold | 48 / 50 |
| `MANUAL_VALIDATION_SHEET_INTERNAL_BELOW_RATED.csv` | 25 | Internal (eval vs. train) pairs below the threshold | 24 / 25 |

`validation_sheet_*page*.png` are the contact-sheet pages the raters viewed (`validation_sheet_page*` for the main set, `_below_page*` for below-threshold cross-dataset, `_internal_below_page*` for internal).

### `figures/`

| File | Description |
|---|---|
| `fig_1_full_pipeline.png` | Fig. 1 — full audit pipeline |
| `fig2_example_duplicates.png` | Fig. 2 — example internal duplicates |
| `fig3_external_duplicates_sample.png` | Fig. 3 — sample cross-dataset duplicates |
| `fig4a_split_comparison.png` | Fig. 4a — naive vs. patient-level split comparison |
| `fig4b_confusion_matrices.png` | Fig. 4b — confusion matrices |
| `supplimentary_internal_leakage.png` | Supplementary — internal leakage by dataset |
| `supplimentary_cross_dataset_overlap.png` | Supplementary — cross-dataset overlap |

## Datasets used

None of the raw images are redistributed here — only hashes, embedding-derived similarity scores, and metadata. Get the original images from their sources:

| Dataset | Source |
|---|---|
| Figshare (Cheng et al.) | https://figshare.com/articles/dataset/brain_tumor_dataset/1512427 |
| Nickparvar | https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset |
| BRISC | https://doi.org/10.1038/s41597-026-06753-y |
| Sartaj (`Shartaj` in result files) | https://www.kaggle.com/datasets/sartajbhuvaji/brain-tumor-classification-mri |
| Br35H | https://www.kaggle.com/datasets/ahmedhamada0/brain-tumor-detection |
| Rahman | https://doi.org/10.17632/mk56jw9rns.1 |
| BDNeuro-MRI | https://doi.org/10.17632/zwr4ntf94j.7 |

Dataset names in `results/` follow the notebook's labels (e.g. `Masoud_Nickparvar`, `Shartaj`, `BDNeuro-HIra`, `Brain_Cancer_Mizanur`).

## Reproducing this

1. Download the datasets above into one root folder, following the structure noted in `notebook/`. Verify them against `checksums/dataset_aggregate_sha256.csv`.
2. Run the notebook top to bottom. GPU recommended for the cross-dataset embedding step and the patient-split experiment — both are slow on CPU.
3. Outputs land in `results/` and `figures/`, matching what's in this repo already.

## Citation

If you use this manifest, code, or checklist, please cite:

```
[citation once the paper is published — will update after acceptance]
```

## License

MIT — see LICENSE. This covers the code and the manifest/results in this repo. It does not cover the original MRI images, which belong to their respective original authors/datasets linked above.

## Contact

Questions or issues: open a GitHub issue, or email 22103395@iubat.edu.
