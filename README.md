# Brain Tumor MRI Dataset Leakage Audit


This repo audits internal train/test leakage and cross-dataset overlap across seven public brain tumor MRI datasets, and reports a controlled experiment comparing naive (image-level) vs. patient-level splitting on the Figshare dataset.

## What's here

- `notebook/` — the full pipeline: manifest construction, internal leakage detection, cross-dataset detection, manual validation, and the patient-split experiment.
- `manifest/` — the image manifest (dataset, split, label, hashes) for all 34,525 images used in this study.
- `results/` — all output CSVs: internal leakage tables, cross-dataset overlap tables, manual validation ratings, per-class metrics.
- `figures/` — the figures used in the paper.

## Datasets used

None of the raw images are redistributed here — only hashes, embeddings-derived similarity scores, and metadata. Get the original images from their sources:

| Dataset | Source |
|---|---|
| Figshare (Cheng et al.) | https://figshare.com/articles/dataset/brain_tumor_dataset/1512427 |
| Nickparvar | https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset |
| BRISC | https://doi.org/10.1038/s41597-026-06753-y |
| Sartaj | https://www.kaggle.com/datasets/sartajbhuvaji/brain-tumor-classification-mri |
| Br35H | https://www.kaggle.com/datasets/ahmedhamada0/brain-tumor-detection |
| Rahman | https://doi.org/10.17632/mk56jw9rns.1 |
| BDNeuro-MRI | https://doi.org/10.17632/zwr4ntf94j.7 |

## Reproducing this

1. Download the datasets above into one root folder, following the structure noted in `notebook/`.
2. Run the notebook top to bottom. GPU recommended for the cross-dataset embedding step and the patient-split experiment — both are slow on CPU.
3. Outputs land in `results/` and `figures/`, matching what's in this repo already.

## Manual validation

`results/manual_validation_final.csv` has the 75 pairs used to check the cross-dataset similarity threshold, rated independently by two people blind to the similarity score. Both raters agreed on all 75 pairs.

## Citation

If you use this manifest, code, or checklist, please cite:

```
[citation once the paper is published — will update after acceptance]
```

## License

MIT — see LICENSE. This covers the code and the manifest/results in this repo. It does not cover the original MRI images, which belong to their respective original authors/datasets linked above.

## Contact

Questions or issues: 22103395@iubat.edu.
