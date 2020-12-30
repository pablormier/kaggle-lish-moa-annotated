
This repository contains a CSV file mapping Entrez gene IDs to gene IDs
used in Kaggle's [Mechanism of Action (MoA) prediction challenge](https://www.kaggle.com/c/lish-moa). 

filename: gene_mapping.csv 

- old = Entrez gene ID
- new = Kaggle's gene ID

It also contains a CSV file mapping the PRISM cell line IDs with the cell line IDs used in the challenge. 

filename: cell_mapping.csv 

- old = cell line ID
- new = Kaggle's cell line ID

This cell line ID can be used with another CSV file (cell_info.csv) to obtain the Cancer Cell Line Name (ccle_name).
Details about each Cancer Cell Line can be found by browsing [the DepMap portal](https://depmap.org). 