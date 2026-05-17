# Scanpy Spatial Transcriptomics Analysis: Human Lymph Node

## Overview

This Jupyter notebook demonstrates a complete workflow for analyzing spatial transcriptomics data using **Scanpy**, a Python-based toolkit for single-cell and spatial gene expression analysis. The analysis uses the **Visium Spatial Gene Expression dataset** from human lymph node tissue.

google drive link

https://drive.google.com/drive/folders/1dM6Bci38y6S0OUFczNE5yBTvC_xm4w28?usp=drive_link


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

  

  # Visium Fluorescence Data Analysis with Squidpy

## Overview

This project demonstrates a complete spatial transcriptomics analysis workflow using the Squidpy library on 10x Genomics Visium fluorescence data. The analysis integrates high-resolution tissue imaging with gene expression data to explore the spatial organization of the tissue at the molecular level.

## What We Did

### 1. Data Loading and Setup
- Loaded a pre-processed Visium fluorescence dataset, including a high-resolution fluorescence tissue image and an AnnData object containing gene expression counts, spatial coordinates, and pre-computed clustering results.
- 
<img width="660" height="493" alt="image" src="https://github.com/user-attachments/assets/afddc1b3-c2f9-46ba-9728-38352331e748" />

### 2. Exploratory Visualization
- Visualized the spatial distribution of pre-computed Leiden clusters directly on the tissue image to identify distinct spatial patterns of cell populations.
- Displayed individual channels of the fluorescence image to examine marker expression patterns across the tissue section.

### 3. Image Processing and Segmentation
- Applied image smoothing to reduce noise and enhance structural features.
- Performed watershed segmentation on the processed image to identify distinct morphological regions and cellular compartments.
- Visualized the segmentation results alongside the original image for quality assessment.
- 
<img width="549" height="289" alt="image" src="https://github.com/user-attachments/assets/6d742ee1-e56e-4a95-80b9-b7feb8f91fce" />

### 4. Feature Extraction
- Extracted segmentation-based features from the fluorescence image, including mean pixel intensity values per channel for each segmented region.
- Integrated these image-derived features into the AnnData object for downstream analysis.

### 5. Integrated Spatial Analysis
- Compared the extracted image-based segmentation features with the original gene expression-based clustering.
- Visualized multiple features simultaneously (clustering labels and channel mean intensities) in spatial context to reveal relationships between tissue morphology and transcriptional profiles.

## Key Outcomes

- Successfully demonstrated an integrated approach combining imaging data with transcriptomic information for spatial tissue analysis.
- Generated segmentation masks that identify distinct tissue regions based on morphological features.
- Extracted quantitative image features that can be correlated with gene expression patterns.
- Visualized the spatial heterogeneity of both cellular organization and molecular signatures across the tissue section.
<img width="1107" height="845" alt="image" src="https://github.com/user-attachments/assets/5b48b7fb-2ae3-4a72-b824-2c7d82b9e685" />

  <img width="2408" height="1182" alt="image" src="https://github.com/user-attachments/assets/ede53ae4-8b75-4c7f-b1af-108f402ceb70" />


## Tools and Libraries Used

- **Squidpy**: For spatial data analysis and image processing
- **Scanpy**: For single-cell and spatial gene expression analysis
- **AnnData**: For handling annotated data matrices
- **Matplotlib**: For visualization
- **Pandas**: For data manipulation

  

  # Spatial Transcriptomics Analysis of Visium H&E Data

## Overview

This Jupyter notebook demonstrates a complete spatial transcriptomics analysis workflow using **Squidpy**, a Python library for spatial omics data. The dataset is from the mouse hippocampus (HNE region) and includes both gene expression data and a matching H&E-stained histology image. The analysis integrates molecular and imaging data to uncover spatial patterns, cell-cell interactions, and tissue architecture.

## Requirements

The notebook requires the following Python libraries:
- `numpy`
- `pandas`
- `anndata`
- `scanpy`
- `squidpy`
- `matplotlib`
- `seaborn`
- `leidenalg` (for clustering)

These are installed automatically via `pip` within the notebook.

## Workflow Steps

### 1. Setup and Data Loading
- Load required libraries and set up inline plotting.
- Download a pre-processed Visium dataset (`visium_hne_adata.h5ad`) and its corresponding H&E image (`visium_hne_image.tiff`) using `sq.datasets.visium_hne_adata()` and `sq.datasets.visium_hne_image()`.

### 2. Initial Visualization
- Visualize the spatial distribution of pre-defined gene expression clusters using `sq.pl.spatial_scatter(adata, color="cluster")`.
- 
<img width="662" height="229" alt="image" src="https://github.com/user-attachments/assets/93c347e4-4a8f-4f25-a846-ac22ede30f15" />

### 3. Image Feature Extraction
- Extract summary image features at multiple spatial scales (1.0 and 2.0) using `sq.im.calculate_image_features()`.
- Combine features from both scales into a single dataframe and store in `adata.obsm["features"]`.
- Ensure no duplicated feature names using `anndata.utils.make_index_unique()`.

### 4. Feature-Based Clustering
- Cluster spots based on image features (using PCA + Leiden clustering) via a custom function `cluster_features()`.
- Add resulting cluster labels to `adata.obs["features_cluster"]`.
- Compare image-based clusters (`features_cluster`) with gene expression clusters (`cluster`) using spatial scatter plots.
- 
<img width="1471" height="435" alt="image" src="https://github.com/user-attachments/assets/d950e1d9-9bf5-46e4-baf9-a5e26228bbcb" />

### 5. Neighborhood Enrichment Analysis
- Compute spatial neighbors using `sq.gr.spatial_neighbors()`.
- Perform neighborhood enrichment analysis with `sq.gr.nhood_enrichment()` and visualize the results using `sq.pl.nhood_enrichment()`.
- 
<img width="1315" height="1021" alt="image" src="https://github.com/user-attachments/assets/b63184f1-72d7-425d-b1ac-a2428ec16d25" />

### 6. Co-occurrence Analysis
- Compute co-occurrence of clusters within spatial neighborhoods using `sq.gr.co_occurrence()`.
- Visualize co-occurrence for a specific cluster (e.g., "Hippocampus") with `sq.pl.co_occurrence()`.

### 7. Ligand-Receptor Interaction Analysis
- Perform permutation-based ligand-receptor interaction testing using `sq.gr.ligrec()`.
- Visualize significant interactions from a source group ("Hippocampus") to target groups (e.g., "Pyramidal_layer", "Pyramidal_layer_dentate_gyrus") using `sq.pl.ligrec()`, with filters for mean expression and statistical significance.

## Key Results

- **Image features** provide complementary spatial information to gene expression clusters.
- **Feature-based clustering** reveals histological domains that may not be captured by transcriptomics alone.
- **Neighborhood enrichment** and **co-occurrence** analyses identify statistically significant spatial associations between clusters.
- **Ligand-receptor analysis** highlights potential signaling pathways active between anatomical regions.
- 
<img width="2434" height="418" alt="image" src="https://github.com/user-attachments/assets/70efcb76-18d9-407d-bb59-c22f354ca364" />

## Notes

- The notebook includes a FutureWarning about transitioning from `leidenalg` to `igraph` backend for faster Leiden clustering.
- Ligand-receptor analysis may generate large plots; filters are applied to focus on significant interactions.
- All visualizations are rendered inline with `%matplotlib inline`.

## Outputs

- Spatial scatter plots comparing gene expression clusters and image-based feature clusters.
- Heatmaps of neighborhood enrichment and co-occurrence.
- Heatmap of ligand-receptor interactions with statistical significance.

## Conclusion

This notebook provides a reproducible workflow for integrating histology images and transcriptomics data in spatial biology studies. It highlights the power of Squidpy for extracting biologically meaningful insights from Visium data.

# Xenium Spatial Transcriptomics Data Analysis

## Overview

This Jupyter notebook provides a complete workflow for analyzing **Xenium spatial transcriptomics data** from 10x Genomics. The pipeline demonstrates loading, processing, and visualizing high-resolution spatial gene expression data from human lung cancer FFPE tissue samples.

## Key Technologies & Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| `spatialdata` | 0.7.2 | Spatial omics data structures |
| `spatialdata-io` | 0.6.0 | Xenium data loader |
| `scanpy` | 1.12.1 | Single-cell analysis |
| `squidpy` | 1.8.1 | Spatial analysis & visualization |
| `leidenalg` | 0.11.0 | Community detection clustering |
| `matplotlib` | - | Visualization |
| `seaborn` | - | Statistical visualizations |

## Dataset

- **Platform**: Xenium In Situ (v1)
- **Sample**: Human Lung Cancer, FFPE tissue
- **Source**: 10x Genomics official dataset
- **File**: `Xenium_V1_humanLung_Cancer_FFPE_outs.zip`
- **Size**: ~7.44 GB
# 🔬 Analysis Workflow


### Step 1: Environment Setup & Data Loading

``python
# Import required libraries
import spatialdata as sd
from spatialdata_io import xenium
import scanpy as sc
import squidpy as sq
import matplotlib.pyplot as plt
import seaborn as sns
import os

# Load Xenium data
sdata = xenium("./Xenium_Lung_Cancer", cells_as_circles=True)
adata = sdata.tables["table"]

# Calculate QC metrics
sc.pp.calculate_qc_metrics(adata, percent_top=(10, 20, 50, 150), inplace=True)

# Filter low-quality cells and genes
sc.pp.filter_cells(adata, min_counts=10)
sc.pp.filter_genes(adata, min_cells=5)

# Store raw counts and normalize
adata.layers["counts"] = adata.X.copy()
sc.pp.normalize_total(adata, inplace=True)
sc.pp.log1p(adata)

# Dimensionality reduction
sc.pp.pca(adata)
sc.pp.neighbors(adata)
sc.tl.umap(adata)

# Clustering
sc.tl.leiden(adata)

<img width="654" height="276" alt="image" src="https://github.com/user-attachments/assets/e4970086-fe58-4eef-ac33-43387aefd158" />

<img width="1614" height="515" alt="image" src="https://github.com/user-attachments/assets/06ed8bcf-85f0-4fda-9423-3667d997fc32" />


Step 4: Visualizations
Quality Control Histograms
Four-panel figure showing distributions of:

Total transcripts per cell

Unique transcripts per cell

Segmented cell area

Nucleus-to-cell area ratio

UMAP Visualization
UMAP plots colored by:

Total transcript counts

Number of genes by counts

Leiden cluster assignments

Spatial Scatter Plot
Cell positions overlaid on tissue morphology

Colored by Leiden cluster identity

Reveals spatial organization of cell types

<img width="1018" height="1014" alt="image" src="https://github.com/user-attachments/assets/878617a5-1c30-4bd9-b4b7-780af34bdbf3" />

<img width="654" height="216" alt="image" src="https://github.com/user-attachments/assets/838a1545-ed8c-4f0a-8cb8-cd4742a92faf" />


  ✍️ Author
AQBA EJAZ

