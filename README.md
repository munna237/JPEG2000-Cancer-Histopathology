# JPEG2000 Compression Effects on AI Cancer Diagnosis in Histopathology

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![TensorFlow 2.15](https://img.shields.io/badge/TensorFlow-2.15-orange.svg)](https://www.tensorflow.org/)

This repository contains the code, trained models, and analysis scripts for our study: **"Safe JPEG2000 Limits for AI Cancer Diagnosis in Histopathology: Balancing Storage, Accuracy, and Sustainability"**

## 📋 Overview

We systematically evaluated JPEG2000 compression effects on deep learning-based cancer classification across three international histopathology datasets, establishing tissue-specific compression guidelines for clinical deployment.

### Key Findings

| Finding | Description |
|---------|-------------|
| 🟢 **Safe Zone** | CR ≤ 100 is universally safe (<5% accuracy loss) |
| 🟡 **Caution Zone** | CR 100-500 requires validation for breast tissue |
| 🔴 **Danger Zone** | CR > 500 risks significant degradation (except colorectal) |
| 🎯 **CAT Benefit** | Compression-Aware Training recovers up to +13.43% accuracy |

### Highlights

- **3 Datasets**: BreakHis (Brazil), BACH (Portugal), MHIST (USA)
- **2 Cancer Types**: Breast and Colorectal
- **13 Models Evaluated**: Systematic architecture selection
- **7 Compression Ratios**: CR1 (original) to CR1000
- **3 Experiments**: Adaptation, Robustness, Compression-Aware Training
- **Sustainability Tracking**: 529g CO₂ total emissions

---

## 📁 Repository Structure

```
JPEG2000-Cancer-Histopathology/
│
├── 📁 data/
│   ├── README.md                    # Dataset download instructions
│   └── sample_images/               # Example images at each CR level
│
├── 📁 src/
│   ├── __init__.py
│   │
│   ├── 📁 preprocessing/
│   │   ├── compress_images.py       # JPEG2000 compression pipeline
│   │   ├── create_splits.py         # Train/val/test splitting
│   │   └── augmentation.py          # Data augmentation utilities
│   │
│   ├── 📁 models/
│   │   ├── inception_densenet_attention.py  # Final selected model
│   │   ├── single_backbones.py      # ResNet50, DenseNet121/169, EfficientNetB0
│   │   ├── attention_modules.py     # CBAM, SE-Block, Channel Attention
│   │   └── hybrid_architectures.py  # Xception+DenseNet, DualDenseNet, etc.
│   │
│   ├── 📁 training/
│   │   ├── train.py                 # Main training script
│   │   ├── callbacks.py             # Custom callbacks
│   │   └── config.py                # Training configuration
│   │
│   ├── 📁 experiments/
│   │   ├── experiment1_adaptation.py       # Train & test at same CR
│   │   ├── experiment2_robustness.py       # Train CR1, test all CR
│   │   ├── experiment3_cat.py              # Compression-Aware Training
│   │   └── model_selection.py              # Architecture comparison
│   │
│   └── 📁 analysis/
│       ├── cross_dataset_analysis.py       # Generate paper figures/tables
│       ├── sustainability_analysis.py      # Carbon emissions analysis
│       ├── statistical_tests.py            # Paired t-tests, Cohen's d
│       └── visualization.py                # Plotting utilities
│
├── 📁 notebooks/
│   ├── 01_data_preparation.ipynb           # Dataset setup
│   ├── 02_compression_pipeline.ipynb       # JPEG2000 compression
│   ├── 03_model_selection.ipynb            # Architecture comparison
│   ├── 04_experiment1_adaptation.ipynb     # Adaptation study
│   ├── 05_experiment2_robustness.ipynb     # Robustness study
│   ├── 06_experiment3_cat.ipynb            # CAT experiments
│   ├── 07_cross_dataset_analysis.ipynb     # Generate paper materials
│   └── 08_sustainability_analysis.ipynb    # Carbon tracking
│
├── 📁 results/
│   ├── 📁 BreakHis/
│   │   ├── experiment1_adaptation.csv
│   │   ├── experiment2_robustness.csv
│   │   ├── experiment3_compression_aware.csv
│   │   └── sustainability_analysis.csv
│   │
│   ├── 📁 BACH/
│   │   └── (same structure)
│   │
│   ├── 📁 MHIST/
│   │   └── (same structure)
│   │
│   ├── 📁 model_selection/
│   │   ├── quick_test_v3.csv               # Single backbones
│   │   ├── hybrid_test_v2.csv              # Hybrid architectures
│   │   └── texture_hybrid_results.csv      # Final selection
│   │
│   └── 📁 cross_dataset/
│       ├── 📁 tables/
│       │   ├── table1_dataset_characteristics.csv
│       │   ├── table2_adaptation_results.csv
│       │   ├── table3_robustness_vs_cat.csv
│       │   ├── table4_key_findings.csv
│       │   ├── table5_sustainability_by_dataset.csv
│       │   ├── table6_co2_by_cr_level.csv
│       │   ├── table_model_selection.csv
│       │   └── statistical_analysis.csv
│       │
│       └── 📁 figures/
│           ├── fig1_adaptation_all_datasets.png
│           ├── fig2_robustness_vs_cat.png
│           ├── fig3_heatmap.png
│           ├── fig4_cat_improvement.png
│           ├── fig5_co2_by_cr_level.png
│           ├── fig6_co2_distribution.png
│           ├── fig7_accuracy_vs_co2.png
│           └── fig_model_selection.png
│
├── 📁 paper/
│   ├── manuscript.tex                       # LaTeX manuscript
│   ├── references.bib                       # Bibliography
│   ├── supplementary.tex                    # Supplementary materials
│   └── figures/                             # High-res paper figures
│
├── requirements.txt
├── setup.py
├── LICENSE
└── README.md
```

---

## 🗃️ Datasets

We used three publicly available histopathology datasets:

| Dataset | Country | Cancer Type | Images | Resolution | Source |
|---------|---------|-------------|--------|------------|--------|
| **BreakHis** | 🇧🇷 Brazil | Breast | 7,909 | 700×460 | [Link](https://web.inf.ufpr.br/vri/databases/breast-cancer-histopathological-database-breakhis/) |
| **BACH** | 🇵🇹 Portugal | Breast | 400 | 2048×1536 | [Link](https://iciar2018-challenge.grand-challenge.org/) |
| **MHIST** | 🇺🇸 USA | Colorectal | 3,152 | 224×224 | [Link](https://bmirds.github.io/MHIST/) |

### Dataset Preparation

```bash
# Download datasets (see data/README.md for detailed instructions)
python src/preprocessing/download_datasets.py

# Apply JPEG2000 compression at all CR levels
python src/preprocessing/compress_images.py --dataset breakhis --cr_levels 1,15,25,50,100,500,1000

# Create train/val/test splits
python src/preprocessing/create_splits.py --dataset breakhis --patient_wise
```

---

## 🔧 Installation

```bash
# Clone repository
git clone https://github.com/munna237/JPEG2000-Cancer-Histopathology.git
cd JPEG2000-Cancer-Histopathology

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or: venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt
```

### Requirements

```txt
tensorflow==2.15.0
glymur==0.12.1
scikit-learn==1.3.0
pandas==2.0.0
numpy==1.24.0
matplotlib==3.7.0
seaborn==0.12.0
codecarbon==2.3.1
scipy==1.11.0
pillow==10.0.0
tqdm==4.65.0
```

---

## 🧪 Experiments

### Model Selection

We evaluated 13 architectures on BreakHis (CR1, 5-fold CV):

| Rank | Model | Accuracy |
|------|-------|----------|
| 1 | **Inception-DenseNet-Attention** | **84.97% ± 7.23%** ✅ |
| 2 | CBAM-DenseNet169 | 84.96% ± 7.08% |
| 3 | DenseNet169 | 84.77% ± 8.18% |
| ... | ... | ... |
| 12 | ResNet50 | 65.68% ± 6.96% |
| 13 | EfficientNetB0 | 62.23% ± 13.64% |

### Experiment 1: Adaptation Study

Train and test at matched compression levels:

```bash
python src/experiments/experiment1_adaptation.py \
    --dataset breakhis \
    --cr_levels 1,15,25,50,100,500,1000 \
    --folds 5
```

### Experiment 2: Robustness Study

Train on CR1, evaluate on all compression levels:

```bash
python src/experiments/experiment2_robustness.py \
    --dataset breakhis \
    --train_cr 1 \
    --test_cr 1,15,25,50,100,500,1000 \
    --folds 5
```

### Experiment 3: Compression-Aware Training (CAT)

Train on mixed compression levels:

```bash
python src/experiments/experiment3_cat.py \
    --dataset breakhis \
    --train_cr 1,15,25,50,100 \
    --test_cr 1,15,25,50,100,500,1000 \
    --folds 5
```

---

## 📊 Results

### Key Findings

| Dataset | CR1 Acc | CR100 Drop | CR1000 Drop | CAT Recovery |
|---------|---------|------------|-------------|--------------|
| **BreakHis** | 85.61% | -3.18% | -6.98% | **+13.43%** |
| **BACH** | 77.75% | -11.00% | **-29.25%** | +1.75% |
| **MHIST** | 80.57% | -0.10% | -0.39% | -1.94% |

### Statistical Significance

| Comparison | BreakHis | BACH | MHIST |
|------------|----------|------|-------|
| CR1 vs CR100 | ns | * (p=0.039) | ns |
| CR1 vs CR1000 | ** (p=0.002) | *** (p<0.001) | ns |

### Sustainability

| Metric | Value |
|--------|-------|
| Total CO₂ | 529.03 g |
| Total Energy | 0.554 kWh |
| Training Time | 5.96 hours |

---

## 📈 Reproduce Paper Figures

```bash
# Generate all tables and figures
python src/analysis/cross_dataset_analysis.py \
    --results_dir results/ \
    --output_dir results/cross_dataset/

# Generate sustainability analysis
python src/analysis/sustainability_analysis.py \
    --results_dir results/ \
    --output_dir results/cross_dataset/
```

---

## 📝 Citation

If you use this code or findings, please cite:

```bibtex
@article{munna2026jpeg2000,
  title={Safe JPEG2000 Limits for AI Cancer Diagnosis in Histopathology: 
         Balancing Storage, Accuracy, and Sustainability},
  author={Munna, Mohammad Mehedi Hasan and Kabir, Acramul Haque},
  journal={PLOS ONE},
  year={2026},
  publisher={Public Library of Science}
}
```

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add new feature'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.

---

## 📧 Contact

- **Mohammad Mehedi Hasan Munna** - [@munna237](https://github.com/munna237)


---

## 🙏 Acknowledgments

- BreakHis dataset creators (Spanhol et al., 2016)
- BACH dataset organizers (Aresta et al., 2019)
- MHIST dataset creators (Wei et al., 2021)
- CodeCarbon for sustainability tracking

