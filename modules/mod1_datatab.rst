.. _Datatab:

Data table
================================================================================

For the selected dataset, the data table module provides a descriptive 
statistical analysis at a gene level with visualizations. It has four sections
which are described below.


Plots
--------------------------------------------------------------------------------
:**A**: For a gene specified by the user, the ``plots`` section displays figures 
        related to the expression level of the gene, correlation with other genes,
        and average expression ranking within the dataset. 

:**B**: In the visual analysis, users can filter out some samples or collapse
        the samples by phenotype class. It is also possible to visualize the 
        information on a raw count level (CPM) instead of a log2 level (logCPM).

:**C**: For further information from the literature, hyperlinks are provided to 
        link the selected gene to databases like `OMIM <https://www.ncbi.nlm.nih.gov/omim/>`__, 
        `KEGG <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC102409/>`__, 
        and `GO <http://geneontology.org/>`__.

:**D**: It also correlates the gene to the expressions of other genes across 
        datasets such as `ImmProt <https://www.ncbi.nlm.nih.gov/pubmed/28263321>`__ 
        and `HPA <https://www.nature.com/articles/nbt1210-1248>`__, 
        and plots the cumulative correlation.

:**E**: Furthermore, tissue expression for a selected gene is displayed using
        the `GTEx <https://www.ncbi.nlm.nih.gov/pubmed/23715323>`__ database. 

.. figure:: figures/ug.006.png
    :align: center
    :width: 100%



Counts
--------------------------------------------------------------------------------
:**F**: The total number of counts (abundance) per sample and their distribution
        among the samples are displayed in the ``counts`` section. 

:**G**: For each sample, the user can also see the percentage of counts for major
        gene types, such as CD molecules, kinases or RNA binding motifs.

.. figure:: figures/ug.007.png
    :align: center
    :width: 100%


Gene table
--------------------------------------------------------------------------------
Further correlation analysis across the samples can be performed under 
the ``gene table`` section, where genes are ordered in the table according
to the correlations with the selected gene. The gene-wise average expression
of samples per phenotype classes is also presented in the table. 

.. figure:: figures/ug.008.png
    :align: center
    :width: 100%


Sample table
--------------------------------------------------------------------------------
More detailed information about the samples and comparisons are reported under
the ``sample table`` section.

.. figure:: figures/ug.009.png
    :align: center
    :width: 100%
