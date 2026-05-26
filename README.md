# GSE183276 scRNA-seq Analysis
scRNA-seq analysis workflow in R for the kidney fibrosis dataset GSE183276 including preprocessing, quality control, clustering, batch correction, visualization, and downstream analysis.
## DATA and DEPENDENCIES

### DATASET: GSE183276 - Diabetic Kidney Disease scRNA-seq

GEO Accession: GSE183276
Download counts matrix: 
```bash
wget https://ftp.ncbi.nlm.nih.gov/geo/series/GSE183nnn/GSE183276/suppl/GSE183276_Kidney_Healthy-Injury_Cell_Atlas_scCv3_Counts_03282022.RDS.gz
```

**Additional files used:**
- Metadata file 
- Protein-coding gene list from GENCODE
- CellTypist reference models

## Workflow Overview

**The pipeline includes:**

- Seurat object creation
- Quality control filtering
- Normalization and scaling
- PCA and UMAP visualization
- Clustering analysis
- Harmony batch correction
- Cell type annotation
- Differential expression analysis


### R Dependencies

#### CRAN packages
```r
install.packages(c(
  "Seurat",
  "SeuratDisk",
  "dplyr",
  "R.utils",
  "ggplot2",
  "ggExtra",
  "RColorBrewer",
  "openxlsx",
  "scales",
  "HGNChelper",
  "dittoSeq",
  "harmony"
))
```

#### Bioconductor packages
```r
if (!requireNamespace("BiocManager", quietly = TRUE))
install.packages("BiocManager")

BiocManager::install(c("batchelor", "zellkonverter", "SingleCellExperiment"))
```

## Repository Structure

```text
├── input/
├── output/
├── plots/
├── README.md
├── qc_batchcorrection.Rmd
└── Protein_coding_genes.txt
```

## Quality Control Parameters
| Metric                   | Threshold             | Explanation |
| ------------------------ | --------------------- | ------------ |
| Minimum genes per cell   | `nFeature_RNA > 200`  | Remove low-quality cells and empty droplets |
| Maximum genes per cell   | `nFeature_RNA < 7000` | Reduce potential doublets or multiplets |
| Mitochondrial percentage | `percent.mt < 15%`    | Remove stressed or dying cells with high mitochondrial RNA |
| Ribosomal percentage     | `percent.rb < 10%`    | Reduce ribosomal-dominant low-information cells |
| UMI outlier filtering    | Mahalanobis distance  | Identify global count outliers |

## Author

Umar Misbah
