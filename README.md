# Cell Type-Specific Drug Response Prediction

Predicting which cancer cell subpopulations respond to specific drugs using single-cell RNA-seq and machine learning.

## Dataset
- **sci-Plex**: 800K single cells, 188 drugs, 3 cancer cell lines
- **Cell lines**: MCF7 (breast), A549 (lung), K562 (leukemia)
- **Analysis focus**: dose=10,000, time=24h

## Progress

### ✅ Completed
1. **Data preprocessing**: Filtered to 15,472 control cells, 22,305 genes
2. **Quality control**: Verified data quality (median 1,506 UMI/cell, 968 genes/cell)
3. **Clustering**: Identified 7 clusters using Leiden algorithm
   - 3 major clusters representing cell line identity
   - 4 minor clusters representing sub-populations
4. **Marker gene identification**: Found differentially expressed genes per cluster

### 📊 Key Results
![Control Cell Clustering](figures/03_control_umap_clustering.png)

### 🔜 Next Steps
1. Analyze drug response across clusters
2. Build ML model for drug sensitivity prediction
3. Identify optimal drug combinations

## Methods
- **Tools**: Python, Scanpy, scikit-learn, PyTorch
- **Clustering**: PCA (50 components) → UMAP → Leiden clustering
- **Statistical testing**: Wilcoxon rank-sum for marker genes

## Project Structure
```
├── data/
│   ├── raw/              # Original sci-Plex dataset
│   └── processed/        # Filtered, normalized data
├── notebooks/            # Analysis notebooks
├── figures/              # Generated plots
└── README.md
```
