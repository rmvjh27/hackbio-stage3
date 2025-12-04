# SARS-CoV-2 Infection Dynamics
This project aims to reproduce the clustering and cell type annotation from a study by Ravindra et al. (2021) and perform trajectory analysis on human airway epithelial cells after three days of SARS-CoV-2 infection.
## Workflow:
### Installation of required libraries (scanpy, anndata, igraph, decoupler, fa2-modified) and data import
The data import stage involves grouping barcodes, features, and matrix files into separate directories based on their treatment groups (mock, 1dpi, 2dpi, 3dpi). This helps in loading data from each treatment group into separate AnnData objects.
### Quality control and normalization
- Removal of genes expressed in less than 3 cells, cells expressing less than 200 genes, and cells with mitochondrial reads above 10%, as performed by Ravindra et al. (2021)
- Normalization with log-transformation
### Dimensionality reduction and clustering
- Principal component analysis
- Dimensionality reduction using UMAP
- Clustering with the Leiden algorithm
### Cell type annotation
- Identification of cell types using marker genes that are specific to the lungs
- Visualization of gene expression levels across treatment groups (Target genes: ACE2, CTSL, TMPRSS2, TMPRSS4, ENO2, TUBB4B, ALDH1A1)
### Trajectory analysis
Pseudotime analysis to identify cell differentiation.

### Reference:
Ravindra NG, Alfajaro MM, Gasque V, Huston NC, Wan H, et al. (2021) Single-cell longitudinal analysis of SARS-CoV-2 infection in human airway epithelium identifies target cells, alterations in gene expression, and cell state changes. *PLOS Biology* 19(3): e3001143. https://doi.org/10.1371/journal.pbio.3001143
