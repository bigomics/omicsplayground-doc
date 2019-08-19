.. _Dataprep_example:

Data preparation examples
================================================================================

We provide four types of example cases to guide users for preparing their input 
data and injecting it into the platform. Basically, the example cases 
illustriate how to prepare an input data:

1. from FASTQ files, 
2. from gene counts table or GEO repository data,
3. from single-cell data,
4. from LC-MS/MS proteomics data.

All the necessary scripts for data cleaning and preprocessing examples can be
found under the ``/scripts`` folder.


From FASTQ files
--------------------------------------------------------------------------------
If users have FASTQ files, we provide a collection of scripts to obtain
gene counts through quality control, trimming, quantification of gene abundance,
and so on. Users can run the following script to obtain a gene counts table::

    R counts_from_FASTQ.R

Although the script implements the Salmon, users can modify and use 
any other software, including Kallisto or Star.
Afterwards, users can continue with the instructions in the next 
section to prepare their input data from the gene counts table.


From gene counts table or GEO repository
--------------------------------------------------------------------------------
Users can also prepare an input data from their own gene counts or download a
relevant dataset from repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Some examples case are provided in

    +TCGA-BRCA: pgx-tcga-brca.R
    +TCGA-PRAD: pgx-tcga-prad.R
    +GSE10846: pgx-GSE10846-dlbcl.R
    +GSE114716: pgx-GSE114716-ipilimumab.R
    +GSE22886: pgx-GSE22886-immune.R
    +GSE28492: pgx-GSE28492-roche.R
    +GSE32591: pgx-GSE32591-lupusnephritis.R
    +GSE53784: pgx-GSE53784-wnvjev.R
    +GSE88808: pgx-GSE88808-prostate.R



From single-cell data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

    +GSE72056: pgx-GSE72056-scmelanoma.R
    +GSE92332: pgx-GSE92332-scintestine.R
    +GSE98638: pgx-GSE98638-scliver.R
    +GSE99795: pgx-GSE99795-scprostate.R
    +pbmc1k_10X: pgx-tenx-pbmc1k.R



From LC-MS/MS proteomics data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

    +Geiger et al. 2016: pgx-geiger2016-arginine.R
    +Rieckmann et al. 2017: pgx-rieckmann2017-immprot.R



