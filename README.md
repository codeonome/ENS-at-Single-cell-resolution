# ENS-at-Single-cell-resolution
Replication of Morarach et al. (2019): Enteric Neuron Diversity
This project replicates the analysis from Morarach et al., which characterized the diversity of enteric neurons in the mouse small intestine using single-cell RNA sequencing.

Background:
The original study profiled myenteric neurons from postnatal day 21 (P21) Baf53b-Cre mice. Neurons were sequenced using scRNA-seq and analyzed using Seurat (v3.1.4). Here, we reproduce the same workflow using Scanpy, following the original filtering, clustering, and annotation strategy.

Preprocessing Steps (as per the paper):
Quality Filtering:
Remove cells with <1,500 or >8,000 detected genes.
Exclude cells with >60,000 UMI counts (potential doublets).

Filter cells with high mitochondrial content:
10% if <4,000 genes
25% if >4,000 genes

Normalization & Feature Selection:
Normalize using a regularized negative binomial model (SCTransform-like).
Regress out mitochondrial gene expression.
Retain top 3,000 highly variable genes.
Remove sex-specific (e.g., Xist, Uty) and immediate early genes (e.g., Fos, Jun).

Clustering Pipeline:

First-level clustering: 50 PCs, resolution = 1.5
→ Identify and remove non-neuronal/glial contaminants.

Second-level clustering: 35 PCs, resolution = 1.0
→ Separate glia vs neurons.

Third-level clustering: 30 PCs, resolution = 0.4
→ Final resolution of 12 (biologically meaningful) neuronal clusters.

Visualization:

UMAP: minimum distance = 0.5, n_neighbors = 30
Annotated clusters based on known marker gene profiles.
