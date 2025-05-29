
# ScGRADES: Single-cell Grading and Dataset Evaluation System

---

## Installation

### conda environment (recommended for Seurat-based workflows)

```bash
# Create a conda environment with required R packages
conda create -n scgrades_env r-base=4.1 r-seurat r-dplyr r-tibble r-purrr r-optparse r-ggplot2 -c conda-forge -c bioconda
conda activate scgrades_env
```

### Local installation from GitHub

```r
# Install devtools if not already
install.packages("devtools")

# Install directly from GitHub
devtools::install_github("TongWu2022/ScGRADES")

#Install R package
install.pakages("ScGRADES")
```

### For development:

```bash
git clone https://github.com/TongWu2022/ScGRADES.git
```

```r
setwd("path/to/ScGRADES")
devtools::load_all()
```

---

## Dependencies

### R packages:

- Seurat (≥ 4.0)
- dplyr
- purrr
- tibble
- optparse
- ggplot2

---

## Usage

```r
library(ScGRADES)

# Load input data
seurat_obj <- readRDS("your_data.rds")

# Step 1: Cluster the cells at multiple resolutions
seurat_obj <- FindClusterAcrossRes(seurat_obj, resolutions = seq(0.1, 1.5, 0.1))

# Step 2: Compute PCA-based Euclidean distance
dist_mat <- BuildCellGraph(seurat_obj, reduction = "pca")

# Step 3: Identify core cells
Seurat_obj <- IdentifyCoreCells(seurat_obj, dist = dist_mat, top_n = 20, resolutions = seq(0.1, 1.5, 0.1))
```

---

## Output

- Adds a `CellClass` column to `seurat_obj@meta.data`, labeling cells as:
  - `Core-cell`: all top-N neighbors consistently cluster together across resolutions
  - `Middle-cell`: partial consistency
  - `Marginal-cell`: inconsistent neighbors


---

## Citation
