# scRNAseq_GSE183276
scRNA-seq analysis workflow in R for kidney fibrosis dataset (GSE183276) including preprocessing, quality control, clustering, batch correction, visualization, and downstream analysis.

Dataset
GEO Accession: GSE183276
Download counts matrix: wget https://ftp.ncbi.nlm.nih.gov/geo/series/GSE183nnn/GSE183276/suppl/GSE183276_Kidney_Healthy-Injury_Cell_Atlas_scCv3_Counts_03282022.RDS.gz

Additional files used:
Metadata file
Protein-coding gene list from GENCODE
CellTypist reference models

Workflow Overview

The pipeline includes:

Seurat object creation
Quality control filtering
Normalization and scaling
PCA and UMAP visualization
Clustering analysis
Harmony batch correction
Cell type annotation
Differential expression analysis

Quality Control Parameters
| Metric                   | Threshold             |
| ------------------------ | --------------------- |
| Minimum genes per cell   | `nFeature_RNA > 200`  |
| Maximum genes per cell   | `nFeature_RNA < 7000` |
| Mitochondrial percentage | `percent.mt < 15%`    |
| Ribosomal percentage     | `percent.rb < 10%`    |
| UMI outlier filtering    | Mahalanobis distance  |

R Dependencies
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


Batch Correction
Harmony integration was used for correction of sample-specific batch effects.

