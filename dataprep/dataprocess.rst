.. _dataprocess:

Data processing inside Omics Playground
================================================================================

Filtering of features (genes) and samples
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The data preprocessing includes some filtering criteria, such as filtering of 
genes based on variance, the expression across the samples, and the number of 
missing values. Similarly, samples can also be filtered based on the read quality, 
total abundance, unrelated phenotype, or an outlier criterion.

Normalisation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The raw counts are converted into counts per million (CPM) and log2. Depending on 
the data set, a quantile normalization can be applied. Known batches in the data 
can be corrected with limma or ComBat. Other unknown batch 
effects and unwanted variation can be further removed using surrogate variable 
analysis in the sva package.


Offline computation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Statistics for the differentially expressed genes analysis and gene set enrichment
analysis are precomputed to accelerate the visualisation on the interface.

