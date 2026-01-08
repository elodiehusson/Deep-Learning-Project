# THCA – Machine Learning Pipeline for Mutation / Stage / Tumor Type Prediction

Course: MU5BIP012 – Artificial Intelligence and Deep Learning for Biology
Academic Year: 2025–2026
Formation : Master 2 AIDA 
Project Title: Deep Learning Analysis for Thyroid Cancer Stratification (THCA)

File type : Jupyter Notebook
Authors: Terry ASSOULINE, Elodie HUSSON and Pierre THEVENIN
Data : The Cancer Genome Atlas (TCGA) cohorte TCGA-THCA. 
Deadline : January 11th at 11:59 PM

____________________________________________________________________

This repository contains a full analysis pipeline on THCA (thyroid cancer) bulk RNA‑seq expression data, including:

- preprocessing of expression matrices,
- supervised classification,
- dimensionality reduction (PCA, UMAP),
- autoencoder latent representations and clustering,
- feature importance (permutation). 

____________________________________________________________________

Repository Structure

├── data/
│   └── THCA_expression_matrix_final.csv
│
├── results/
│   ├── evaluation_mutation.pdf
│   ├── evaluation_stade_tumoral.pdf
│   ├── evaluation_type_tumoral.pdf
│   ├── feature_importance_mutation.pdf
│   ├── PCA_mutation.pdf
│   ├── PCA_stade_tumoral.pdf
│   ├── UMAP_mutation.pdf
│   ├── UMAP_stade_tumoral.pdf
│   └── tableaux_congruence.pdf
│
├── results_autoencoder/
│   ├── autoencoder_loss_curves.pdf
│   ├── k_selection_silhouette.pdf
│   ├── latent_embedding.csv
│   ├── latent_tsne_clusters.pdf
│   ├── latent_umap_clusters.pdf
│   └── tableaux_croises_clusters.pdf
│
├── script/
│   ├── Début de pipeline.ipynb (on Python)
│   ├── expression matrix finale.ipynb (on R)
│   ├── pipeline_autoencoder.ipynb (on Python)
│   ├── df.rds
│   └── results.rds
│
└── README.md


____________________________________________________________________


## Metadata encoding

Clinical information is embedded directly in sample names, e.g.:

TCGA-XX-XXXX_AGE=65ANS_SEX=female_STAGE=Stade_II_MUT=BRAF


Parsed variables:

* AGE
* SEX (male/female)
* STAGE (Stade_I, Stade_II, Stade_III, Stade_IV)
* MUT (mutation class: BRAF, RAS, NO CANONICAL DRIVER, etc.)

____________________________________________________________________


## 1. "expression matrix finale.ipynb"

This file is the initial preprocessing of raw expression matrices, export of final expression matrix.

Outputs:
"THCA_expression_matrix_final.csv"
Matrix with :
- rows = genes 
- columns = samples (patients)
Run first if rebuilding data from raw sources.


### 2. "Début de pipeline.ipynb"

Metadatas :
AGE
SEX (male/female)
STAGE (Stade_I, Stade_II, Stade_III, Stade_IV)
MUT (mutation class: BRAF, RAS, NO CANONICAL DRIVER, etc.)

Main supervised learning pipeline, here are the main steps:

1. Load expression matrix
2. Parse metadata from sample names
3. Define prediction task:
   - "stade_tumoral"
   - "mutation"
4. Dimensionality reduction:
   - PCA
   - UMAP
5. Feature selection:
   - ANOVA (SelectKBest)
6. MLP training 
7. Evaluation:
   - confusion matrix
   - accuracy, precision, recall, F1
8. Cross-validation 
9. Permutation feature importance
10. Gene annotation (Ensembl → symbol)
11. Functional enrichment:
    - GO BP / MF / CC
    - KEGG pathways

Outputs:
- Evaluation PDFs
- PCA / UMAP plots
- Feature importance plots


## 3. "pipeline_autoencoder.ipynb"

Unsupervised analysis using autoencoder. Steps:

1. Autoencoder training on expression matrix
2. Latent space extraction
3. Clustering (k-means)
4. Cluster number selection (silhouette)
5. Visualization:
   - UMAP
   - t-SNE
6. Clinical association with clusters

Outputs (in "results_autoencoder/"):
- Loss curves
- Cluster visualization
- Latent embeddings (CSV)
- Cluster vs clinical variable tables


