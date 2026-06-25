# JPEG2000 Compression Effects on AI Cancer Diagnosis in Histopathology

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![TensorFlow 2.15](https://img.shields.io/badge/TensorFlow-2.15-orange.svg)](https://www.tensorflow.org/)

This repository contains the code, trained models, and analysis scripts for our study: **"JPEG2000 Compression Thresholds for Deep Learning-Based Cancer Histopathology Classification: A Multi-Dataset, Multi-Tissue Evaluation with Compression-Aware Training"**

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
├── results/
│   ├── BreakHis/                    # BreakHis experiment results
│   ├── BACH/                        # BACH experiment results
│   ├── MHIST/                       # MHIST experiment results
│   └── model_selection/             # Architecture comparison results
│
├── figures/                         # Paper figures (PNG + PDF)
├── tables/                          # Paper tables (CSV)
├── notebooks/                       # Jupyter notebooks
├── data/                            # Dataset download instructions
│
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

---

## 🗃️ Datasets

We used three publicly available histopathology datasets:

| Dataset | Country | Cancer Type | Images | Source |
|---------|---------|-------------|--------|--------|
| **BreakHis** | 🇧🇷 Brazil | Breast | 7,909 | [Link](https://web.inf.ufpr.br/vri/databases/breast-cancer-histopathological-database-breakhis/) |
| **BACH** | 🇵🇹 Portugal | Breast | 400 | [Link](https://iciar2018-challenge.grand-challenge.org/) |
| **MHIST** | 🇺🇸 USA | Colorectal | 3,152 | [Link](https://bmirds.github.io/MHIST/) |

See `data/README.md` for detailed download instructions.

---

## 🔧 Installation

```bash
# Clone repository
git clone https://github.com/munna237/JPEG2000-Cancer-Histopathology.git
cd JPEG2000-Cancer-Histopathology

# Install dependencies
pip install -r requirements.txt
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
| 4 | DualDenseNet-Attention | 83.97% ± 9.59% |
| 5 | Xception-DenseNet169 | 83.84% ± 7.80% |
| ... | ... | ... |
| 12 | ResNet50 | 65.68% ± 6.96% |
| 13 | EfficientNetB0 | 62.23% ± 13.64% |

### Three Experiments

1. **Adaptation Study**: Train and test at matched compression levels
2. **Robustness Study**: Train on CR1, evaluate on all compression levels
3. **Compression-Aware Training (CAT)**: Train on mixed compression levels

---

## 📊 Results

### Key Findings

| Dataset | CR1 Acc | CR100 Drop | CR1000 Drop | CAT Recovery |
|---------|---------|------------|-------------|--------------|
| **BreakHis** 🇧🇷 | 85.61% | -3.18% | -6.98% | **+13.43%** |
| **BACH** 🇵🇹 | 77.75% | -11.00% | **-29.25%** | +1.75% |
| **MHIST** 🇺🇸 | 80.57% | -0.10% | -0.39% | -1.94% |

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

## 📈 Figures

| Figure | Description |
|--------|-------------|
| `fig1_adaptation_all_datasets` | Accuracy across compression levels |
| `fig2_robustness_vs_cat` | Robustness vs CAT comparison |
| `fig3_heatmap` | Cross-dataset performance heatmap |
| `fig4_cat_improvement` | CAT improvement visualization |
| `fig5_co2_by_cr_level` | CO₂ emissions by compression |
| `fig6_co2_distribution` | Emissions distribution |
| `fig7_accuracy_vs_co2` | Accuracy-sustainability trade-off |
| `fig_model_selection` | Model architecture comparison |

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
- **Email:** - mohammadmehedi.munna@gmail.com

---

## 🙏 Acknowledgments

- BreakHis dataset creators (Spanhol et al., 2016)
- BACH dataset organizers (Aresta et al., 2019)
- MHIST dataset creators (Wei et al., 2021)
- CodeCarbon for sustainability tracking
