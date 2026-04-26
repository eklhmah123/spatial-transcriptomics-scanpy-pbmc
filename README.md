# Scanpy Spatial Transcriptomics Analysis: Human Lymph Node

## Overview

This Jupyter notebook demonstrates a complete workflow for analyzing spatial transcriptomics data using **Scanpy**, a Python-based toolkit for single-cell and spatial gene expression analysis. The analysis uses the **Visium Spatial Gene Expression dataset** from human lymph node tissue.

## Notebook Structure

### 1. Setup and Installation
- Installation of required packages:
  - `scanpy` - Single-cell analysis toolkit
  - `matplotlib` - Visualization
  - `pandas` - Data manipulation
  - `seaborn` - Statistical visualizations
- Configuration of Scanpy settings
- Installation of `igraph` for graph-based clustering

### 2. Data Loading
- Loads the 10x Genomics Visium dataset: `V1_Human_Lymph_Node`
- Makes variable names unique
- Identifies mitochondrial genes (MT- genes) for quality control
- Calculates QC metrics

### 3. Quality Control (QC)

**Cell Filtering:**
- Minimum 5,000 counts per cell
- Maximum 35,000 counts per cell
- Removes cells with >20% mitochondrial reads

**Gene Filtering:**
- Filters genes detected in fewer than 10 cells

**Visualizations:**
- Histograms showing:
  - Total counts distribution
  - Counts distribution (zoomed view)
  - Number of genes per cell
  - Genes per cell (zoomed view)

<img width="1016" height="1091" alt="image" src="https://github.com/user-attachments/assets/8c3669d0-a960-48bd-b92d-34d5d2f837f7" />

### 4. Data Preprocessing
- Normalizes total counts per cell
- Log-transforms the data
- Extracts highly variable genes using Seurat flavor (top 2000 genes)

### 5. Dimensionality Reduction & Clustering
- Principal Component Analysis (PCA)
- Neighborhood graph construction
- UMAP (Uniform Manifold Approximation and Projection) for visualization
- Leiden clustering for community detection (10 clusters identified)

### 6. Visualization
- UMAP plots colored by:
  - `total_counts` - Total UMI counts per cell
  - `n_genes_by_counts` - Number of genes detected
  - `clusters` - Leiden cluster assignments
- Spatial visualization showing gene expression patterns across tissue coordinates
<img width="670" height="920" alt="image" src="https://github.com/user-attachments/assets/900745b4-ee28-4353-9c43-33c05daa8db3" />

## Key Findings

- **Initial dataset**: 3,861 cells remaining after QC filtering
- **Genes retained**: Filtered out 16,916 genes detected in fewer than 10 cells
- **Clusters identified**: 10 distinct cell populations via Leiden clustering

## Dependencies
scanpy>=1.12.0
matplotlib>=3.5.0
pandas>=1.4.0
seaborn>=0.11.0
igraph>=0.9.0

text

## Usage Notes

1. The notebook uses the `visium_sge` function from Scanpy (note: this function is deprecated; `squidpy.datasets.visium` is recommended for future use)
2. Spatial visualization uses `sc.pl.spatial` (deprecated; `squidpy.pl.spatial_scatter` is recommended for future use)
3. The analysis includes both standard single-cell QC metrics and spatial-specific considerations

## Output Files

The notebook generates:
- QC filtering statistics
- Normalized and log-transformed expression matrix
- Highly variable gene list
- UMAP embedding coordinates
- Leiden cluster assignments
- Spatial scatter plots
- 
<img width="1170" height="1084" alt="image" src="https://github.com/user-attachments/assets/7cc21a86-fe47-4692-b10f-b2f570b4e655" />

## References

- Scanpy documentation: https://scanpy.readthedocs.io/
- 10x Genomics Visium: https://www.10xgenomics.com/spatial-transcriptomics

  ✍️ Author
AQBA EJAZ

