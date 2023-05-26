.. _Dataprep:


Data preparation examples
================================================================================
The platform requires the transcriptomics and proteomics data to be in a 
structured format as an input. The easiest way is to prepare three csv files: **counts.csv**, **samples.csv** and an optional **contrast.csv**. 
When these files are ready, users can upload them direcly in Omics Playground.

Requirements:

1. :ref:`Counts file <counts>` Count/expression .csv file with gene on rows, samples as columns.
2. :ref:`Samples file <samples>` Samples .csv file with samples on rows, phenotypes as columns.
3. :ref:`Contrasts file <contrasts>` Contrast .csv file with samples on rows, conditions as columns. (optional)

.. seealso::

    If you have raw file formats, such as FASTQ files or LC-MS proteomics data (mzML, RAW, WIFF...), check our tutorials on how to prepare the counts matrix from these raw formats: :ref:`data preparation examples <Dataprep_example>`.


Uploading data through the interface
--------------------------------------------------------------------------------

.. _`uploading through the interface`:

Users can import their data from the **Upload data** panel located under the 
:ref:`Home` module. The platform requires the list of files as shown in the
figure below. 
The format of files must be comma-separated-values (CSV) text.
It is important to name the files exactly as shown.
Be sure the dimensions, rownames and column names match for all files. 
It is required to provide a unique name and brief description for the data set
while uploading.



.. figure:: ../modules/figures/psc1.3.png
    :align: center
    :width: 100%


Data import and precomputation
================================================================================

The data import and precomputation involve preparing the input data through 
filtering, normalising and precomputing statistics for some analyses and 
importing it into the platform. The data cleaning and precomputation is 
performed offline to support real-time interaction by minimizing user interface
latency.

Data import
--------------------------------------------------------------------------------
Users can import their transcriptomics or proteomics data to the platform by 
either uploading the data through
the interface or preparing an input object using scripts.
For uploading, the platform requires the counts, samples information and optionally contrasts tables in CSV format. 
On the other hand, an input object can be prepared using scripts from different 
types and formats of data, including counts and FASTQ.
With scripts it is also possible to do more detailed data 
cleaning, filtering, normalisation and preprocessing. 


.. seealso::

    See :ref:`data preparation examples <Dataprep_example>` how
    to prepare an input data for the platform. You can find more detailed 
    information regarding the filtering and normalisation methods for preparing
    an input from different sources of experiments.
    

Filtering
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





