# Annotated Kaggle's Mechanism of Action (MoA) dataset

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1fushdQIoX_xGAoGzQ1hw4740D-Wlkb1D?usp=sharing)

Mechanism of Action (MoA) Prediction is a Kaggle's challenge created by the [Broad Institute of MIT and Harvard](https://clue.io/), the [Laboratory for Innovation Science at Harvard (LISH)](http://lish.harvard.edu/), and the [NIH Common Funds Library of Integrated Network-Based Cellular Signatures (LINCS)](https://lincsproject.org/). The goal of this challenge, as described in Kaggle, is the following:

> "In this competition, you will have access to a unique dataset that combines gene expression and cell viability data. The data is based on a new technology that measures simultaneously (within the same samples) human cells’ responses to drugs in a pool of 100 different cell types (thus solving the problem of identifying ex-ante, which cell types are better suited for a given drug). In addition, you will have access to MoA annotations for more than 5,000 drugs in this dataset.". https://www.kaggle.com/c/lish-moa/overview

However, the original dataset was anonymized, and genes and cell lines were not provided. After the competition, the organizers released the original mapping data to have access to the original NCBI Entrez accession numbers for the genes and the CCLE cell lines used (https://github.com/LISHarvard/moa_challenge). 

**In order to facilitate its use, this repository contains the original data and a notebook to combine all the information into a single annotated csv file. Also, entrez ids were mapped to gene symbols and added into the final csv file for convenience.**

## How to use

This repository already includes the annotated dataset (lish_moa_annotated.csv.zip) resulting from running the notebook `annotate.ipynb`. It can be loaded directly using pandas:

```python
>> import pandas as pd
>>
>> df = pd.read_csv("https://github.com/pablormier/kaggle-lish-moa-annotated/raw/master/lish_moa_annotated.csv.zip")
>> df
```
![dataframe](https://github.com/pablormier/kaggle-lish-moa-annotated/raw/master/img/dataframe.png)

Get only the training data (rows for which MoAs and drug ids are known)

```python
>> df_training = df.loc[df.training==True,]
>> df_training.shape
(23814, 1486)
```

Get the annotated gene features. The gene features (originally called g-XX) were replaced by g-GeneSymbol_ENTREZID:

```python
>> genes = [e for e in df_training.columns.values if e.startswith("g-")]
>> genes[:10]
['g-AARS1_16',
 'g-ABCF1_23',
 'g-ABL1_25',
 'g-ACAA1_30',
 'g-ACLY_47',
 'g-ADAM10_102',
 'g-ADH5_128',
 'g-PARP1_142',
 'g-ADRB2_154',
 'g-AGL_178']
```

Get the annotated cell lines. Cell viability features (originally called c-XX in Kaggle) were replaced by c-XX-CCLEcellName. The number following the 'c-' corresponds to the original number used in the kaggle dataset. Cell lines can be queried using the DepMap portal. For example, https://depmap.org/portal/cell_line/HEYA8_OVARY?tab=mutation

```python
>> cells = [e for e in df_training.columns.values if e.startswith("c-")]
>> cells[:10]
['c-0-HEYA8_OVARY',
 'c-1-RKO_LARGE_INTESTINE',
 'c-2-CAL62_THYROID',
 'c-3-HLF_LIVER',
 'c-4-T24_URINARY_TRACT',
 'c-5-ES2_OVARY',
 'c-6-YD15_SALIVARY_GLAND',
 'c-7-KYSE70_OESOPHAGUS',
 'c-8-KP4_PANCREAS',
 'c-9-A2780_OVARY']
```

Split the training data into features and labels:

```python
>> X = df_training.iloc[:, :-608]
>> Y = df_training.iloc[:, -608:]
>> X.shape, Y.shape
((23814, 878), (23814, 608))
```

The target labels used for evaluation in the Kaggle competition are only the first 206 labels:

```python
>> Y_target = Y.iloc[:,:206]
>> Y_target
```
![targets](https://github.com/pablormier/kaggle-lish-moa-annotated/raw/master/img/scored_targets.png)
