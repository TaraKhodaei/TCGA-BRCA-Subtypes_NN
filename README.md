# 🧬 Breast Cancer Subtype Classification Using TCGA RNA-Seq Data

This project applies deep learning to classify breast cancer subtypes using RNA-Seq gene expression data from the **TCGA-BRCA** dataset. It includes a complete pipeline from data acquisition to model training and evaluation, with step-by-step instructions.

---

## Project Overview

Breast cancer subtyping is critical for treatment planning. In this project, we classify samples into four molecular subtypes — **Luminal A**, **Luminal B**, **HER2-enriched**, and **Basal-like** — using gene expression profiles and the PAM50 label system. The model is implemented using Keras (TensorFlow backend) with several layers of regularization and optimization.

---

## Model Comparison Summary

| Model     | Feature Selection     | Architecture              | Regularization             | Final Accuracy | Final Loss | 
|-----------|-----------------------|----------------------------|-----------------------------|----------------|-------------|
| Model 1   | All genes             | 512 → 256 → 4             | None                        | ~74%           | ~2.79       | 
| Model 2   | Top 57K by variance   | 512 → 256 → 4             | Dropout (0.3)               | ~71%           | ~0.87       | 
| Model 3   | Top 57K               | 512 → 256 → 4             | Dropout + EarlyStopping     | ~76%        | ~1.51       | 
| Model 4   | Top 2.5K              | 256 → 128 → 64 → 4        | BatchNorm + Dropout         | ~76%        | ~1.02       | 
| Model 5   | Top 3K                | 512 → 256 → 128 → 64 → 4  | Dropout (0.5) + BN          | ~75.8%       | ~0.9262     | 
| Model 6   | Top 3K                | Same as above             | Dropout + LR scheduler      | **77.3%**  | **0.8981**  | 
| Model 7   | Top 3K                | Same + explicit val split | Dropout + LR scheduler      | ~76.6%       | ~0.8688     | 

---

Despite strong modeling, the best accuracy plateaus around 77%. Likely causes include:

- **Small sample size** (~500 samples)
- **Biological label noise** — PAM50 subtypes have overlap
- **Single modality** — no clinical or CNV data included
- **No data augmentation** — only expression data used
- **Note** - This project focuses on transparency and reproducibility using only expression data and standard preprocessing to establish a baseline model. Future work could integrate multi-omics, larger datasets, or domain-specific embeddings for further gains.

---

## Data Source

- 🔗 **GDC Portal**: https://portal.gdc.cancer.gov/

- ⚖️ **Legal Use**: Data used here is from the **Open Access tier** and does not require dbGaP login.

> 🚫 **Note**: The dataset is **not uploaded to GitHub** due to size and licensing.
>
> However, we include full instructions to legally download and process the data from the GDC portal.

---

## Citation

If you use this data or model, please cite:

> The Cancer Genome Atlas Network. *Comprehensive molecular portraits of human breast tumors*. Nature 490, 61–70 (2012). https://doi.org/10.1038/nature11412

## Citation

If you use this **data**, please cite the TCGA consortium:

> The Cancer Genome Atlas Network. *Comprehensive molecular portraits of human breast tumors*. Nature 490, 61–70 (2012). https://doi.org/10.1038/nature11412

If you use this **modeling pipeline or notebook**, please credit this repository with a link or citation in your work:

> *TCGA-BRCA Subtype Classification with Deep Learning*.  
> GitHub Repository: [your GitHub URL here]

---

## License

This project is licensed under the [MIT License](LICENSE), a permissive open-source license allowing reuse, modification, and distribution with attribution.



---

## Summary

This project presents a reproducible deep learning pipeline for classifying breast cancer subtypes using RNA-Seq expression profiles from the TCGA-BRCA dataset. 
The workflow demonstrates core skills in biomedical data preprocessing, model architecture design, and robust evaluation using TensorFlow/Keras. It also emphasizes responsible handling of open-access genomic data and provides a solid baseline for future extensions involving multi-omics or clinical data integration.

