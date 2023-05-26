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


Where to upload data in Omics Playground
--------------------------------------------------------------------------------

.. _`uploading through the interface`:

Users can import their data from the **Upload data** panel located under the 
:ref:`Home` module. The platform requires the list of files as shown in the
figure below. The format of files must be comma-separated-values (CSV) text.
It is important to name the files exactly as shown.
Be sure the dimensions, rownames and column names match for all files. 
It is required to provide a unique name and brief description for the data set
while uploading.

.. figure:: ../modules/figures/psc1.3.png
    :align: center
    :width: 100%



