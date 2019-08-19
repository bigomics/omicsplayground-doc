.. _Dataprep:

Data cleaning and preprocessing
================================================================================

The data cleaning and preprocessing includes preparing the input data, filtering, 
normalising, and precomputing statistics for some analyses. The data cleaning and 
preprocessing is performed offline using scripts in order to support real-time 
interaction and minimize user interface latency. The platform comes with the 
necessary scripts under the ``/scripts`` folder for data cleaning and preprocessing.

.. seealso::

    See some data preparation example cases in :ref:`Data Cleaning Examples <Dataprep_example>`
    


Input data
--------------------------------------------------------------------------------
The platform requires the table of gene counts as input. Users can provide their 
own gene counts or download the relevant data from repositories such as `GEO 
<https://www.ncbi.nlm.nih.gov/geo/>`__. 
If they have FASTQ files, we provide scripts to obtain gene counts through quality 
control, trimming, quantification of gene abundance, and so on. Although the script 
default choice is Salmon, users can modify it and use any other software, 
including `Kallisto <https://pachterlab.github.io/kallisto/>`__ or 
`Star <http://labshare.cshl.edu/shares/gingeraslab/www-data/dobin/STAR/STAR.posix/doc/STARmanual.pdf>`__.

Filtering
--------------------------------------------------------------------------------
The data preprocessing includes some filtering criteria, such as filtering of 
genes based on variance, the expression across the samples, and the number of 
missing values. Similarly, samples can also be filtered based on the read quality, 
total abundance, unrelated phenotype, or an outlier criterion.

Normalisation
--------------------------------------------------------------------------------
The raw counts are converted into counts per million (CPM) and log2. Depending on 
the data set, a quantile normalization can be applied. Known batches in the data 
can be corrected with limma or ComBat. Other unknown batch 
effects and unwanted variation can be further removed using surrogate variable 
analysis in the sva package.

Offline computation
--------------------------------------------------------------------------------
Statistics for the differentially expressed genes (DEG) and gene set enrichment (GSE) 
analyses are precomputed to accelerate the visualisation on the interface.
