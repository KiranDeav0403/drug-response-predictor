# Cell Type-Specific Drug Response Prediction

Predicting which cancer cell subpopulations respond to specific drugs using single-cell RNA-seq and machine learning.

## Overview

Cancer tumors are heterogeneous - different cell populations within the same tumor respond differently to treatment. This project uses single-cell RNA sequencing to identify which cell types are sensitive or resistant to specific drugs, enabling precision medicine approaches that target all tumor subpopulations.

## Dataset

- **Source:** sci-Plex (Srivatsan et al., 2020)
- **Scale:** 800,000 single cells, 188 drug compounds, 3 cancer cell lines
- **Cell lines:** MCF7 (breast cancer), A549 (lung cancer), K562 (leukemia)
- **Current analysis:** Dose=10,000 nM, Time=24h

## Key Results

### Baseline Heterogeneity
- Identified 7 distinct subpopulations in untreated cancer cells
- Cell line identity (MCF7, A549, K562) is the dominant source of variation
- Clustering reveals both broad cell types and finer sub-populations

### Drug Response Patterns
- Analyzed 3 drugs (JAK inhibitor, EZH2 inhibitor, ROCK inhibitor) as proof-of-concept
- **MCF7 breast cancer cells showed consistent resistance** (+6-11% enrichment) across all three drugs
- **A549 and K562 cells were preferentially depleted**, demonstrating cell-type-specific drug sensitivity

![Control Cell Clustering](figures/03_control_umap_clustering.png)
*UMAP visualization of 7 clusters in control cells, colored by cell line (left), Leiden clustering resolution 0.5 (middle), and resolution 1.0 (right).*

## Progress

### ✅ Completed
1. **Data preprocessing**: Filtered to 15,472 control cells, 22,305 genes
2. **Quality control**: Verified data quality (median 1,506 UMI/cell, 968 genes/cell)
3. **Unsupervised clustering**: Identified 7 clusters using Leiden algorithm
4. **Marker gene identification**: Found differentially expressed genes per cluster
5. **Drug response analysis (proof-of-concept)**: Demonstrated cell-type-specific effects with 3 example drugs

### 🔜 Next Steps
1. Scale drug response analysis to all 188 compounds
2. Cluster within each cell line to identify cell state-specific responses
3. Build ML classifier for drug sensitivity prediction from gene expression signatures
4. Develop optimization algorithm for identifying synergistic drug combinations

## Methods

**Preprocessing:**
- Quality control (filter low-quality cells/genes)
- Normalization (scale to 10,000 counts per cell)
- Log transformation
- Highly variable gene selection (3,000 genes)

**Clustering:**
- Dimensionality reduction: PCA (50 components) → UMAP
- Graph-based clustering: Leiden algorithm
- Marker gene identification: Wilcoxon rank-sum test

**Drug Response:**
- Differential abundance analysis (compare treated vs control proportions)
- Cell-type-specific sensitivity quantification

**Tools:** Python, Scanpy, scikit-learn, pandas, matplotlib

## Getting Started

### Prerequisites
- Python 3.8+
- 32GB+ RAM recommended for full dataset

### Installation
```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/drug-response-predictor.git
cd drug-response-predictor

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Usage

Notebooks should be run sequentially:

1. `01_data_exploration.ipynb` - Data loading and initial exploration
2. `03_clustering_control.ipynb` - Unsupervised clustering of control cells
3. `04_drug_response_simple.ipynb` - Drug response analysis (proof-of-concept)

**Note:** The full sci-Plex dataset (~2GB) must be downloaded separately from [figshare](https://figshare.com/articles/dataset/sciPlex_dataset/24681285) and placed in `data/raw/`.

## Project Structure
```
├── data/
│   ├── raw/              # Original sci-Plex dataset (download separately)
│   └── processed/        # Preprocessed data (control, treated, clustered)
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 03_clustering_control.ipynb
│   └── 04_drug_response_simple.ipynb
├── figures/              # Generated visualizations
├── requirements.txt      # Python dependencies
└── README.md
```

## About

This project demonstrates how single-cell genomics can reveal cellular heterogeneity that drives treatment resistance in cancer. By identifying which cell populations respond to which drugs, we can design combination therapies that target all tumor subpopulations, potentially preventing relapse.

Developed as part of my Master's in Bioinformatics at Northeastern University, building on research experience at Harvard Medical School in multi-omics drug response prediction.

## Contact

**Kiran Deav Vivekanandan**  
Master's in Bioinformatics, Northeastern University  
📧 vivekanandan.k@northeastern.edu  
🔗 [LinkedIn](YOUR_LINKEDIN_URL)

*Graduating May 2026 | Seeking bioinformatics/computational biology opportunities*

---

## Citation

Dataset: Srivatsan et al., "Massively multiplex chemical transcriptomics at single-cell resolution." *Science* 367.6473 (2020): 45-51.