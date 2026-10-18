# JPEG2000 Compression Thresholds for Deep Learning-Based Cancer Histopathology Classification

Code and results for:

> Munna MMH, Aman N, Kabir AH, Tulona RF, Saha S, Kabir SS, Habib I, Dhrubo V, Sultana T.
> **JPEG2000 Compression Thresholds for Deep Learning-Based Cancer Histopathology Classification:
> A Multi-Dataset, Multi-Tissue Evaluation with Compression-Aware Training.** Under review, *PLOS ONE*.

The study measures how JPEG2000 compression (target ratios CR1–CR1000) affects an
Inception-DenseNet169 attention hybrid on three histopathology datasets (BreakHis, BACH,
NCT-CRC-HE-100K) under three protocols: **adaptation** (train and test at the same ratio),
**robustness** (train on CR1, test at every ratio), and **Compression-Aware Training (CAT)**
(train on CR1–CR100). The revision adds re-predicted metrics, revised statistics, achieved
compression ratios, and a size-matched CAT control.

## Where each result comes from

| Paper item | Produced by | Result files |
|---|---|---|
| Datasets, compression pipeline | `notebooks/01_compression/` | – |
| Model selection | `notebooks/02_model_selection/` | – |
| Rate-distortion table and figure (PSNR, SSIM) | `01_compression/compress_BreakHis.ipynb` (BreakHis), `04_analysis_and_figures/rate_distortion_BACH_NCT-CRC.ipynb` (BACH, NCT-CRC) | `results/rate_distortion/` |
| Achieved vs target compression ratios | `05_revision/tierA_reprediction_metrics_statistics.ipynb` (Section 4) | `results/rate_distortion/*_achieved_cr_summary.csv`, `*_reencode_per_image.csv` |
| Adaptation, robustness, and CAT tables and figures | `notebooks/03_experiments/experiments_{BreakHis,BACH,NCT-CRC}.ipynb` | `results/fold_level/<dataset>/` |
| Additional metrics (balanced accuracy, sensitivity, specificity, MCC, AUC) and NCT-CRC metrics figure | `05_revision/tierA_reprediction_metrics_statistics.ipynb` (Sections 5–6) | `results/revision/tierA/full_metrics_all.csv`, `results/predictions/tierA/` |
| Statistical analysis (corrected resampled t-test, paired bootstrap, Holm) | `05_revision/tierA_reprediction_metrics_statistics.ipynb` (Section 6), `scripts/make_revision_figures.py` | `results/revision/tierA/paired_comparisons.csv`, `results/revision/tierA/adaptation_corrected_t_all_comparisons.csv` |
| Size-matched CAT control (volume vs diversity effect) | `05_revision/R2-5_cat_size_matched_control.ipynb` | `results/revision/r25_control/`, `results/predictions/r25_control/` |
| Sustainability (CO₂) table and figure | `04_analysis_and_figures/sustainability_and_cross_dataset_analysis.ipynb` | `results/sustainability/` |
| Figures of the original submission | `04_analysis_and_figures/figures_*.ipynb` | – |
| Revision figures (NCT-CRC metrics, CAT control, compression zones) | `scripts/make_revision_figures.py` | `figures_revision/` (generated) |
| NCT-CRC subset and splits; test folds | experiment and revision notebooks | `splits/` |

Executed notebooks keep their outputs, so reported numbers can be checked against the printed run logs.
`results/revision/tierA/reprediction_check.csv` shows that predictions recomputed from the saved models
reproduce the fold-level result files to within one or two images per fold.

## Data

The datasets are not redistributed. Download them from the original sources:

- **BreakHis:** https://web.inf.ufpr.br/vri/databases/breast-cancer-histopathological-database-breakhis/
- **BACH (ICIAR 2018):** https://iciar2018-challenge.grand-challenge.org/
- **NCT-CRC-HE-100K:** https://doi.org/10.5281/zenodo.1214456

The compression notebooks regenerate every compressed version. `splits/nct_crc_subset_splits.csv`
lists the 7,799 NCT-CRC images used and their train/validation/test assignment.

## Reproducing

1. Run `notebooks/01_compression/` for each dataset to create the CR1–CR1000 folders.
2. Run `notebooks/03_experiments/` for each dataset (adaptation, robustness, CAT).
3. Run `notebooks/05_revision/tierA_reprediction_metrics_statistics.ipynb` (re-prediction, metrics,
   statistics, achieved ratios), then `notebooks/05_revision/R2-5_cat_size_matched_control.ipynb`
   (size-matched CAT control; about 6 h on an NVIDIA L4).
4. Run `python scripts/make_revision_figures.py` from the repository root.

The notebooks were run on Google Colab with Google Drive storage; paths of the form
`/content/drive/MyDrive/...` must be adapted to your environment. The NCT-CRC notebook defines its own
model-building function (fusion head and mixed-precision setting are in the notebook).

**Software:** Python 3, TensorFlow/Keras (version printed at the top of each executed notebook;
2.20–2.21 for the NCT-CRC and revision runs), Glymur/OpenJPEG, scikit-learn, CodeCarbon.
**Hardware:** NVIDIA T4 and L4 GPUs (Google Colab).

## Trained models

The trained model weights (about 150 `.keras` files of about 150 MB each) exceed GitHub's file-size
limit and are not included. They are available from the corresponding author on request.

## Contact

Mohammad Mehedi Hasan Munna — mohammadmehedi.munna@gmail.com

## Citation

See `CITATION.cff`. Please also cite the original dataset publications.

## License

Code: MIT (see `LICENSE`). Result files in `results/` and `splits/`: CC BY 4.0.
