# Dataset Download Instructions

This study uses three publicly available histopathology datasets.

## 1. BreakHis (Breast Cancer Histopathology)

- **Source**: Laboratory Visão Robótica e Imagem, UFPR, Brazil
- **Images**: 7,909 microscopic images
- **Download**: https://web.inf.ufpr.br/vri/databases/breast-cancer-histopathological-database-breakhis/
- **Citation**: Spanhol et al., IEEE TBE 2016

```bash
# After downloading, extract to:
data/BreakHis/
├── benign/
└── malignant/
```

## 2. BACH (Breast Cancer Histology Grand Challenge)

- **Source**: IPATIMUP, Portugal
- **Images**: 400 H&E-stained images
- **Download**: https://iciar2018-challenge.grand-challenge.org/
- **Citation**: Aresta et al., Medical Image Analysis 2019

```bash
# After downloading, extract to:
data/BACH/
├── Normal/
├── Benign/
├── InSitu/
└── Invasive/
```

## 3. MHIST (Minimalist Histopathology)

- **Source**: Dartmouth-Hitchcock Medical Center, USA
- **Images**: 3,152 colorectal polyp images
- **Download**: https://bmirds.github.io/MHIST/
- **Citation**: Wei et al., AIME 2021

```bash
# After downloading, extract to:
data/MHIST/
├── images/
└── annotations.csv
```

## Preprocessing

After downloading, run the preprocessing pipeline:

```bash
# Apply JPEG2000 compression at all CR levels
python src/preprocessing/compress_images.py --dataset all --cr_levels 1,15,25,50,100,500,1000

# Create train/val/test splits
python src/preprocessing/create_splits.py --dataset all
```

## Note

Due to licensing, we cannot redistribute the datasets. Please download from the official sources above.
