# TCGA-BRCA-Subtypes_NN

# 🧬 Breast Cancer Subtype Classification Using TCGA RNA-Seq Data

This project applies deep learning to classify breast cancer subtypes using RNA-Seq gene expression data from the **TCGA-BRCA** dataset. It includes a complete pipeline from data acquisition to model training and evaluation, with step-by-step instructions.

---

## 📚 Project Overview

Breast cancer subtyping is critical for treatment planning. In this project, we classify samples into four molecular subtypes — **Luminal A**, **Luminal B**, **HER2-enriched**, and **Basal-like** — using gene expression profiles and the PAM50 label system. The model is implemented using Keras (TensorFlow backend) with several layers of regularization and optimization.

---

## 📊 Model Comparison Summary

| Model     | Feature Selection     | Architecture              | Regularization             | Final Accuracy | Final Loss | Notes                                 |
|-----------|-----------------------|----------------------------|-----------------------------|----------------|-------------|----------------------------------------|
| Model 1   | All genes             | 512 → 256 → 4             | None                        | ~74%           | ~2.79       | Simple baseline model                  |
| Model 2   | Top 57K by variance   | 512 → 256 → 4             | Dropout (0.3)               | ~71%           | ~0.87       | Mild regularization added              |
| Model 3   | Top 57K               | 512 → 256 → 4             | Dropout + EarlyStopping     | ~76% ✅        | ~1.51       | Best early-stage model                 |
| Model 4   | Top 2.5K              | 256 → 128 → 64 → 4        | BatchNorm + Dropout         | ~76% ✅        | ~1.02       | Well-regularized, compact              |
| Model 5   | Top 3K                | 512 → 256 → 128 → 64 → 4  | Dropout (0.5) + BN          | ~75.8% ✅      | ~0.9262     | Very consistent                        |
| Model 6   | Top 3K                | Same as above             | Dropout + LR scheduler      | **77.3%** ✅🔥 | **0.8981**  | Best performance overall               |
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

## 📥 Data Source

- 🔗 **GDC Portal**: https://portal.gdc.cancer.gov/
- Dataset: TCGA-BRCA
- Expression: HTSeq-FPKM files (Open Access)
- Labels: PAM50 subtypes from clinical data
- ⚖️ **Legal Use**: Data used here is from the **Open Access tier** and does not require dbGaP login.

> 🚫 **Note**: The dataset is **not uploaded to GitHub** due to size and licensing.
>
> ✅ However, we include full instructions to legally download and process the data from the GDC portal.

---

## 🧪 How to Reproduce

```bash
git clone https://github.com/yourusername/tcga-breast-cancer-subtypes.git
cd tcga-breast-cancer-subtypes
pip install -r requirements.txt
```

Then run the notebook:

```bash
jupyter notebook notebook.ipynb
```

The notebook will walk you through:

- downloading RNA-Seq data and clinical subtype labels
- matching samples
- preprocessing (log, variance filtering)
- training multiple deep learning models
- comparing performance

---

## 📘 Concepts Explained

| Term                 | Description                                                           |
|----------------------|-----------------------------------------------------------------------|
| **Variance**         | Measures feature variability; used to select most informative genes   |
| **Dropout**          | Regularization that randomly "drops" units during training            |
| **BatchNorm**        | Normalizes layer input for faster and more stable training            |
| **EarlyStopping**    | Stops training when validation loss stops improving                   |
| **Adam Optimizer**   | Adaptive optimizer; combines RMSProp + momentum                       |
| **Other Optimizers** | SGD, RMSProp, Adagrad, Adadelta, Nadam (can be tested optionally)     |

---

## 🧾 Citation

If you use this data or model, please cite:

> The Cancer Genome Atlas Network. *Comprehensive molecular portraits of human breast tumors*. Nature 490, 61–70 (2012). https://doi.org/10.1038/nature11412

---

## 📄 License

This project is licensed under the [MIT License](LICENSE), a permissive open-source license allowing reuse, modification, and distribution with attribution.

---

## 📁 Additional Files

- `notebook.ipynb`: full code with explanations
- `requirements.txt`: Python dependencies
- `LICENSE`: MIT license (auto-generated by GitHub)
- `.gitignore`: excludes cache, logs, data files, etc.

---

## 👩‍💻 Author

**Tara Khodaei**  
Postdoctoral Researcher in Computational Biology  
GitHub: [@yourusername](https://github.com/yourusername)

---

## ✅ Summary

This project demonstrates a practical application of machine learning in cancer subtype classification using RNA-Seq data. It balances accessibility with rigor and is built entirely from reproducible, open-access components.
