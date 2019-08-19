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

* `TCGA-BRCA <https://portal.gdc.cancer.gov/projects/TCGA-BRCA>`__: ``pgx-tcga-brca.R``
* `TCGA-PRAD <https://www.cbioportal.org/study/summary?id=prad_tcga>`__: ``pgx-tcga-prad.R``
* `GSE10846 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE10846>`__: ``pgx-GSE10846-dlbcl.R``
* `GSE114716 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE114716>`__: ``pgx-GSE114716-ipilimumab.R``
* `GSE22886 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE22886>`__: ``pgx-GSE22886-immune.R``
* `GSE28492 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE28492>`__: ``pgx-GSE28492-roche.R``
* `GSE32591 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE32591>`__: ``pgx-GSE32591-lupusnephritis.R``
* `GSE53784 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE53784>`__: ``pgx-GSE53784-wnvjev.R``
* `GSE88808 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE88808>`__: ``pgx-GSE88808-prostate.R``



From single-cell data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

* `GSE72056 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72056>`__: ``pgx-GSE72056-scmelanoma.R``
* `GSE92332 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE92332>`__: ``pgx-GSE92332-scintestine.R``
* `GSE98638 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE98638>`__: ``pgx-GSE98638-scliver.R``
* `GSE99795 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE99795>`__: ``pgx-GSE99795-scprostate.R``
* `pbmc1k_10X <>`__: ``pgx-tenx-pbmc1k.R``



From LC-MS/MS proteomics data
--------------------------------------------------------------------------------
Similarly, users can provide their own gene counts or download the relevant data from 
repositories such as `GEO <https://www.ncbi.nlm.nih.gov/geo/>`__.
Users can run the following script to obtain a gene counts table::

* `Geiger et al. 2016 <https://www.ncbi.nlm.nih.gov/pubmed/27745970>`__: ``pgx-geiger2016-arginine.R``
* `Rieckmann et al. 2017 <https://www.ncbi.nlm.nih.gov/pubmed/28263321>`__: ``pgx-rieckmann2017-immprot.R``



