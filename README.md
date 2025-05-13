# TCGA-BRCA-Subtypes_NN

# 🧬 Breast Cancer Subtype Classification Using TCGA RNA-Seq Data

This project applies deep learning to classify breast cancer subtypes using RNA-Seq gene expression data from the **TCGA-BRCA** dataset. It includes a complete pipeline from data acquisition to model training and evaluation, with step-by-step instructions.

---

## Project Overview

Breast cancer subtyping is critical for treatment planning. In this project, we classify samples into four molecular subtypes — **Luminal A**, **Luminal B**, **HER2-enriched**, and **Basal-like** — using gene expression profiles and the PAM50 label system. The model is implemented using Keras (TensorFlow backend) with several layers of regularization and optimization.

---

## Model Comparison Summary

| Model     | Feature Selection     | Architecture              | Regularization             | Final Accuracy | Final Loss | Notes                                 |
|-----------|-----------------------|----------------------------|-----------------------------|----------------|-------------|----------------------------------------|
| Model 1   | All genes             | 512 → 256 → 4             | None                        | ~74%           | ~2.79       | Simple baseline model                  |
| Model 2   | Top 57K by variance   | 512 → 256 → 4             | Dropout (0.3)               | ~71%           | ~0.87       | Mild regularization added              |
| Model 3   | Top 57K               | 512 → 256 → 4             | Dropout + EarlyStopping     | ~76% ✅        | ~1.51       | Best early-stage model                 |
| Model 4   | Top 2.5K              | 256 → 128 → 64 → 4        | BatchNorm + Dropout         | ~76% ✅        | ~1.02       | Well-regularized, compact              |
| Model 5   | Top 3K                | 512 → 256 → 128 → 64 → 4  | Dropout (0.5) + BN          | ~75.8% ✅      | ~0.9262     | Very consistent                        |
| Model 6   | Top 3K                | Same as above             | Dropout + LR scheduler      | **77.3%** ✅ | **0.8981**  | Best performance overall               |
| Model 7   | Top 3K                | Same + explicit val split | Dropout + LR scheduler      | ~76.6% ✅      | ~0.8688     | Very stable and generalizable         |

---

## ⚠️ Why Accuracy Isn't Higher?

Despite strong modeling, the best accuracy plateaus around 77%. Likely causes include:

- ✅ **Small sample size** (~500 samples)
- ⚠️ **Biological label noise** — PAM50 subtypes have overlap
- 🔬 **Single modality** — no clinical or CNV data included
- 🧪 **No data augmentation** — only expression data used

---

## 💡 Skills & Tools Demonstrated

| Area              | Skill / Tool                         |
|-------------------|---------------------------------------|
| Data Source       | TCGA-BRCA (GDC Portal)                |
| Preprocessing     | Log-transform, variance filtering     |
| ML Pipeline       | Deep Neural Network (Keras)           |
| Feature Selection | VarianceThreshold (Top 3K genes)      |
| Regularization    | Dropout, BatchNorm, EarlyStopping     |
| Optimization      | Adam, ReduceLROnPlateau               |
| Evaluation        | Train/val/test split, accuracy, loss  |
| Reproducibility   | Jupyter notebook, modular structure   |

---

## Data Source

- 🔗 **GDC Portal**: https://portal.gdc.cancer.gov/

- ⚖️ **Legal Use**: Data used here is from the **Open Access tier** and does not require dbGaP login.

> 🚫 **Note**: The dataset is **not uploaded to GitHub** due to size and licensing.
>
> However, we include full instructions to legally download and process the data from the GDC portal.

---

## 🧾 Citation

If you use this data or model, please cite:

> The Cancer Genome Atlas Network. *Comprehensive molecular portraits of human breast tumors*. Nature 490, 61–70 (2012). https://doi.org/10.1038/nature11412

---

## 📄 License

This project is licensed under the [MIT License](LICENSE), a permissive open-source license allowing reuse, modification, and distribution with attribution.



---

## ✅ Summary

This project demonstrates a practical application of machine learning in cancer subtype classification using RNA-Seq data. It balances accessibility with rigor and is built entirely from reproducible, open-access components.
