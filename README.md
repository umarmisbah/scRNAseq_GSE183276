# scRNAseq_GSE183276
scRNA-seq analysis workflow in R for kidney fibrosis dataset (GSE183276) including preprocessing, quality control, clustering, batch correction, visualization, and downstream analysis.

## DATA \& DEPENDENCIES

### DATASET: GSE183276 - Diabetic Kidney Disease scRNA-seq :- GEO Accession Page

GEO Accession: GSE183276
Download counts matrix: wget https://ftp.ncbi.nlm.nih.gov/geo/series/GSE183nnn/GSE183276/suppl/GSE183276_Kidney_Healthy-Injury_Cell_Atlas_scCv3_Counts_03282022.RDS.gz

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

#### Bioconductor packages

if (!requireNamespace("BiocManager", quietly = TRUE))
install.packages("BiocManager")

BiocManager::install(c("batchelor", "zellkonverter", "SingleCellExperiment"))

|Package|Purpose / Use|
|-|-|
|`Seurat`|Core single-cell RNA-seq analysis (QC, normalization, clustering, UMAP/tSNE).|
|`SeuratDisk`|Convert Seurat objects to/from `.h5ad` / `.h5seurat` for interoperability with Python (Scanpy) or saving intermediate results.|
|`dplyr`|Data manipulation, filtering, and summarization of metadata or gene-level data.|
|`R.utils`|Utility functions, e.g., for handling compressed files (.gz).|
|`ggplot2`|High-quality plotting (violin plots, scatter plots, heatmaps).|
|`ggExtra`|Enhances ggplot2 plots with marginal histograms or density plots.|
|`RColorBrewer`|Color palettes for plots (clusters, conditions).|
|`openxlsx`|Export tables and results to Excel files (e.g., DEG results).|
|`scales`|Scales and formatting for ggplot2 axes and legends.|
|`HGNChelper`|Corrects gene symbols to HGNC-approved names. Useful for DEG/pathway analysis.|
|`dittoSeq`|Simplified plotting for scRNA-seq data (boxplots, dotplots, UMAPs, heatmaps).|
|`harmony`|Batch correction to integrate multiple samples or donors.|
|`batchelor`|Alternative batch correction for SingleCellExperiment objects.|
|`zellkonverter`|Read/write between `SingleCellExperiment` and `.h5ad` (Scanpy) formats.|
|`SingleCellExperiment`|Core S4 class for single-cell data in R (used by `batchelor` and other Bioconductor packages).|

## Quality Control Parameters
| Metric                   | Threshold             |
| ------------------------ | --------------------- |
| Minimum genes per cell   | `nFeature_RNA > 200`  |
| Maximum genes per cell   | `nFeature_RNA < 7000` |
| Mitochondrial percentage | `percent.mt < 15%`    |
| Ribosomal percentage     | `percent.rb < 10%`    |
| UMI outlier filtering    | Mahalanobis distance < 0.05  |

#### AUTHOR
UMAR MISBAH 
