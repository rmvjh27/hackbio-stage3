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
## Results:
### Identified cell types:
- mock: Ciliated cells, ionocytes, alveolar type I cells
- 1dpi: Ciliated cells, club cells (labelled as Clara cells in the figures), alveolar type I cells, airway goblet cells, ionocytes
- 2dpi: Club cells, ciliated cells, alveolar type I cells, ionocytes
- 3dpi: Ciliated cells, club cells, ionocytes

![mock_celltypes](https://github.com/rmvjh27/hackbio-stage3/blob/main/mock_celltypes.png)
![1dpi_celltypes](https://github.com/rmvjh27/hackbio-stage3/blob/main/1dpi_celltypes.png)
![2dpi_celltypes](https://github.com/rmvjh27/hackbio-stage3/blob/main/2dpi_celltypes.png)
![3dpi_celltypes](https://github.com/rmvjh27/hackbio-stage3/blob/main/3dpi_celltypes.png)

Clusters with no labelled cell type likely belong to the same cell type as the clusters nearest to them, based on marker gene levels.

Mock marker gene levels:
![mock_markers](https://github.com/rmvjh27/hackbio-stage3/blob/main/mock_markers.png)

Marker gene levels 1dpi:
![1dpi_markers](https://github.com/rmvjh27/hackbio-stage3/blob/main/1dpi_markers.png)

Marker gene levels 2dpi:
![2dpi_markers](https://github.com/rmvjh27/hackbio-stage3/blob/main/2dpi_markers.png)

Marker gene levels 3dpi:
![3dpi_markers](https://github.com/rmvjh27/hackbio-stage3/blob/main/3dpi_markers.png)

### Levels of target genes (ACE2, CTSL, TMPRSS2, TMPRSS4, ENO2, TUBB4B, ALDH1A1)
- **ACE2**:
![mock_ace2](https://github.com/rmvjh27/hackbio-stage3/blob/main/mock_ACE2.png)
![1dpi_ace2](https://github.com/rmvjh27/hackbio-stage3/blob/main/1dpi_ace2.png)
![2dpi_ace2](https://github.com/rmvjh27/hackbio-stage3/blob/main/2dpi_ace2.png)
![3dpi_ace2](https://github.com/rmvjh27/hackbio-stage3/blob/main/3dpi_ace2.png)

- **ENO2**:
![mock_eno2](https://github.com/rmvjh27/hackbio-stage3/blob/main/mock_ENO2.png)
![1dpi_eno2](https://github.com/rmvjh27/hackbio-stage3/blob/main/1dpi_ENO2.png)
![2dpi_eno2](https://github.com/rmvjh27/hackbio-stage3/blob/main/2dpi_ENO2.png)
![3dpi_eno2](https://github.com/rmvjh27/hackbio-stage3/blob/main/3dpi_ENO2.png)

*The figures for other target genes (CTSL, TMPRSS2, TMPRSS4, TUBB4B, and ALDH1A1) can be seen in the Jupyter Notebook (**Single_Cell_Analysis_With_Trajectory.ipynb**)*

### Trajectory Analysis
Inference of differentiation in bronchial epithelial cells 3 days after infection, with club cells (Clara cells) as the root cell:
![pseudotime](https://github.com/rmvjh27/hackbio-stage3/blob/main/3dpi_pseudotime.png)

## Discussion
### Cell type identification
All the identified cell types that make up the airway epithelium are thus the primary targets of SARS-CoV-2. All of these cell types express ACE2, which encodes a cell surface receptor that is necessary for the entry of SARS-CoV-2 into target cells. Ciliated cells are the main target cells, as these cells retain their proportion of abundance relative to other cell types across all stages of infection, while club cells are secondary target cells, as the abundance of club cells increases as the infection progresses. This is in line with the results found by Ravindra et al. (2021). Furthermore, ACE2 expression levels are higher in ciliated and club cells compared to other cell types after SARS-CoV-2 infection, indicating that SARS-CoV-2 may preferentially infect these two cell types. Ciliated and club cells also have higher expression levels of CTSL and TMPRSS2. These genes code for cathepsin L and transmembrane serine protease 2, respectively, which are also implicated in SARS-CoV-2 entry. Cathepsin L and transmembrane serine protease 2 cleave the SARS-CoV-2 spike protein, which allows membrane fusion between the virus and the host cell, promoting the entry of the virus (Zhao et al. 2021; Koyou et al. 2025).
### ACE2 and ENO2 expression levels
Expression levels of ENO2, particularly in ciliated cells, show more correlation with SARS-CoV-2 infection than those of ACE2, as ENO2 expression is significantly lower in infected cells when compared with mock cells. Additionally, expression of ENO2 lowers as the infection progresses, indicated by ENO2 expression levels that relatively decrease as more days pass after infection. In comparison, ACE2 expression levels do not change significantly between uninfected (mock) and infected cells, and show no significant change between one stage of infection and another. In conclusion, ENO2 is a better marker for tracking COVID-19 infection than ACE2.
### Trajectory analysis
Trajectory analysis reveals the differentiation of club cells into ciliated cells and ionocytes after 3 days of infection. Club cells can act as stem cells and help regenerate the bronchiolar epithelium in response to damage by differentiating into ciliated cells, goblet cells, and alveolar cells in case of alveolar damage (Zheng et al. 2017; Davis and Wypych 2021). This indicates that SARS-CoV-2 infection leads to damage to the airway epithelium, causing differentiation of club cells as a repair mechanism. However, the differentiation of club cells into ionocytes lacks sufficient evidence. Club cells and ionocytes have been known to arise from different differentiation paths taken by basal and parabasal stem cells (Cumplido-Laso et al. 2023).

## References
- Cumplido-Laso, G., Benitez, D.A., Mulero-Navarro, S. and Carvajal-Gonzalez, J.M. 2023. Transcriptional regulation of airway epithelial cell differentiation: insights into the notch pathway and beyond. *International Journal of Molecular Sciences* 24(19), p. 14789.
- Davis, J.D. and Wypych, T.P. 2021. Cellular and functional heterogeneity of the airway epithelium. *Mucosal Immunology* 14(5), pp. 978–990. Available at: https://doi.org/10.1038/s41385-020-00370-7.
- Koyou, H.L., Salleh, M.N., Jelemie, C.S., Badrin, M.J.Q., Prastiyanto, M.E. and Ramachandran, V. 2025. TMPRSS2: A Key Host Factor in SARS-CoV-2 Infection and Potential Therapeutic Target. *Medeniyet Medical Journal* 40(2), p. 101.
- Ravindra, N.G. et al. 2021. Single-cell longitudinal analysis of SARS-CoV-2 infection in human airway epithelium identifies target cells, alterations in gene expression, and cell state changes. *PLoS Biology* 19(3), p. e3001143.
- Zhao, M.-M. et al. 2021. Cathepsin L plays a key role in SARS-CoV-2 infection in humans and humanized mice and is a promising target for new drug development. *Signal Transduction and Targeted Therapy* 6(1), p. 134. Available at: https://doi.org/10.1038/s41392-021-00558-8.
- Zheng, D. et al. 2017. Differentiation of club cells to alveolar epithelial cells in vitro. *Scientific Reports* 7(1), p. 41661.
