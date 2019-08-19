.. _Dataprep_example:

Data preparation examples
================================================================================

In this section we provide three example cases to guide users for preparing 
their input data and injecting it into the platform. Basically, the example cases 
illustriate how to prepare an input data:

1. from FASTQ files, 
2. from gene counts table or GEO repository data,
3. from single-cell data,
4. from LC-MS/MS proteomics data.


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
Users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

    R input_prep_from_counts.R


From single-cell data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

    R input_prep_from_singlecell.R


From LC-MS/MS proteomics data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

    R input_prep_from_singlecell.R



