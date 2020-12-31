# Annotated Kaggle's Mechanism of Action (MoA) dataset

Mechanism of Action (MoA) Prediction is a Kaggle's challenge created by the [Broad Institute of MIT and Harvard](https://clue.io/), the [Laboratory for Innovation Science at Harvard (LISH)](http://lish.harvard.edu/), and the [NIH Common Funds Library of Integrated Network-Based Cellular Signatures (LINCS)](https://lincsproject.org/). The goal of this challenge, as described in Kaggle, is the following:

> "In this competition, you will have access to a unique dataset that combines gene expression and cell viability data. The data is based on a new technology that measures simultaneously (within the same samples) human cells’ responses to drugs in a pool of 100 different cell types (thus solving the problem of identifying ex-ante, which cell types are better suited for a given drug). In addition, you will have access to MoA annotations for more than 5,000 drugs in this dataset.". https://www.kaggle.com/c/lish-moa/overview

However, the original dataset was anonymized, and genes and cell lines were not provided. After the competition, the organizers released the original mapping data to have access to the original NCBI Entrez accession numbers for the genes and the CCLE cell lines used (https://github.com/LISHarvard/moa_challenge). 

**In order to facilitate its use, this dataset contains the original data and a notebook to combine all the information into a single annotated csv file. Also, entrez ids were mapped to gene symbols and added into the final csv file for convenience.**
