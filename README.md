# Head & Neck Cancer Tumour Marker Identification Pipeline

A reproducible R-based differential expression pipeline for identifying consensus tumour markers in head and neck tumours, validated across two independent public datasets. Developed as part of a PhD-adjacent research collaboration in cancer biology (Griffith University).

---

## 🎯 Aim

To identify a robust panel of upregulated markers in HPV-negative HNSCC tumours versus normal tissue, replicated across two independent datasets, suitable for downstream wet lab validation via immunofluorescence.

---

## 📊 Datasets

| Dataset | Platform | Samples | Source |
|---------|----------|---------|--------|
| TCGA-HNSC | RNA-seq (STAR counts) | HPV-negative tumours + solid tissue normals | GDC Portal via `TCGAbiolinks` |
| GSE65858 | Microarray (normalised) | HPV-negative tumours + normal controls | GEO via `GEOquery` |

Both datasets were filtered to **HPV-negative tumours only**, as HPV-positive HNSCC represents a biologically distinct disease subtype with a different molecular profile. All normal tissue samples were retained as the reference group.

---

## 🔬 Methods

### TCGA-HNSC
- Count data downloaded via `TCGAbiolinks` (STAR — Counts workflow)
- Low-expression genes removed (≥10 counts in ≥10 samples)
- Differential expression via `DESeq2` (Tumour vs Normal, padj < 0.05, |log2FC| > 1)
- VST normalisation for visualisation

### GSE65858
- Pre-normalised microarray expression matrix extracted via `GEOquery`
- Differential expression via `limma` (empirical Bayes moderation, BH correction)
- Significance threshold: adj.P.Val < 0.05, |logFC| > 1

### Consensus Marker Selection
- Top 30 upregulated genes identified independently in each dataset
- Consensus panel = genes significantly upregulated in **both** datasets
- Final 5-marker panel selected for wet lab validation

---

## ✅ Final Marker Panel

| Marker | Function |
|--------|----------|
| **MMP1** | Matrix metalloproteinase — extracellular matrix degradation, invasion |
| **MMP13** | Matrix metalloproteinase — collagen degradation, tumour remodelling |
| **MMP11** | Matrix metalloproteinase — stromal remodelling |
| **CA9** | Carbonic anhydrase IX — hypoxia marker, tumour microenvironment |
| **MAGEA4** | Cancer-testis antigen — tumour-specific expression |

These 5 markers were validated as consensus upregulated genes across TCGA-HNSC and GSE65858, and are proceeding to immunofluorescence validation in patient-derived head and neck cancer tumouroids.

---

## 📁 Repository Structure

```
head-neck-tumouroid-DEG/
├── HNC_marker_pipeline.Rmd       # Full annotated analysis pipeline
├── HNC_marker_report.html        # Knitted HTML report with all figures
├── .gitignore                    # Excludes large data files (.rds, GDCdata/)
└── README.md                     # This file
```

> **Note:** Raw data files (`.rds`, GDC downloads) are excluded via `.gitignore` due to size. Data can be reproduced by running the `eval=FALSE` download chunks in the `.Rmd` file.

---

## ⚙️ Requirements

```r
# Bioconductor
BiocManager::install(c("TCGAbiolinks", "DESeq2", "limma", "edgeR", "GEOquery"))

# CRAN
install.packages(c("tidyverse", "pheatmap", "ggrepel", "RColorBrewer", "openxlsx"))
```

R version ≥ 4.2.0 recommended.

---

## 🚀 How to Run

1. Clone this repository
2. Open `HNC_marker_pipeline.Rmd` in RStudio
3. Run the `eval=FALSE` download chunks once to fetch TCGA and GEO data
4. Knit the document to reproduce the full HTML report

---

## 📄 Output

The knitted report (`HNC_marker_report.html`) includes:
- Volcano plots for both datasets
- Top 30 upregulated marker tables
- Heatmaps (VST-normalised / microarray expression)
- Boxplots for top 10 markers per dataset
- Consensus overlap analysis and final marker panel

---

## 👩‍🔬 Author

**Khushi Bhardwaj**
BSc (Microbiology, Infection & Immunity) / BBiomedSc — University of Queensland
Graduate Certificate in IT | Master of Bioinformatics 

Bioinformatics analysis contributed to a PhD research project in head and neck cancer tumouroid biology.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/khushi-bhardwaj-0495692b6)
[![GitHub](https://img.shields.io/badge/GitHub-k--bhardwajj-333333?style=flat-square&logo=github)](https://github.com/k-bhardwajj)
