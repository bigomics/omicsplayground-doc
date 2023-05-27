.. _Dataprep:


Preparing your data for Omics Playground
================================================================================
The platform requires the transcriptomics and proteomics data to be in a 
structured format as an input. The easiest way is to prepare three csv files: **counts.csv**, **samples.csv** and an optional **contrast.csv**. 
When these files are ready, users can upload them direcly in Omics Playground.

**Input file requirements**
--------------------------------------------------------------------------------

1. :ref:`Counts file <counts>` Count/expression .csv file with gene on rows, samples as columns.
2. :ref:`Samples file <samples>` Samples .csv file with samples on rows, phenotypes as columns.
3. :ref:`Contrasts file <contrasts>` Contrast .csv file with samples on rows, conditions as columns. (optional)

.. seealso::

    If you have raw file formats, such as FASTQ files or LC-MS proteomics data (mzML, RAW, WIFF...), check our tutorials on how to prepare the counts matrix from these raw formats: :ref:`data preparation examples <Dataprep_example>`.