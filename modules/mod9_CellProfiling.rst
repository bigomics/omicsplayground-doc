.. _scProfiling:

Single-Cell Profiling
================================================================================
The **Single-Cell Profiling** module is specifically developed for the analysis
and visualization of single-cell datasets. The main applications are 
identification of immuner cell types and visualisations of markers, copy number 
variations, phenotypes, and 
proportions across the cells.


The **Cell type** panel infers the type of cells using computational deconvolution
methods and reference datasets from the literature. 
The **Markers** panel provides potential marker genes, which are the top genes 
with the highest standard deviation within the expression data across the samples.
It is also possible to perform a copy number variation analysis under the **CNV**
panel. 
The **iTALK** consists of a computational approach from the literature
to characterize and illustrate intercellular communication signals in the 
multicellular tumor ecosystem.
Users can find figures visualizing the distribution of the phenotype information
under the **Phenotypes** panel.
The Proportions panel visualizes the interrelationships between two categorical 
variables (so-called cross tabulation).
Finally, for each combination of gene pairs, the platform can generate a 
cytometry-like plot of samples under the **Cytoplot** panel.


.. note::

    This module is supported in the EXPERT MODE ONLY.


Input slider
--------------------------------------------------------------------------------
Users can filter relevant samples in the ``Filter samples`` settings under the 
the main ``Options``. They can also specify to use a ``tsne`` or ``pca`` layout
for the figures, and group/ungroup the samples in the ``group`` settings.

.. figure:: figures/psc10.0.png
    :align: center
    :width: 30%


Cell type
--------------------------------------------------------------------------------
The **Cell type** profiling infers the type of cells using computational 
deconvolution methods and reference datasets from the literature. 
Currently, we have implemented a total of 8 methods and 9 reference datasets 
to predict immune cell types (4 datasets), tissue types (2 datasets), 
cell lines (2 datasets) and cancer types (1 dataset). However, we plan to expand 
the collection of methods and databases and to infer other cell types.
Under the plot *Settings*, users can specify the ``plot type``: distribution, dotmap,
or heatmap. They can select the reference dataset and the method for 
the cell type prediction in the ``reference`` and ``method`` settings, respectively.

.. figure:: figures/psc10.1.0.png
    :align: center
    :width: 30%

Based on their configuration settings, user will get a similar cell type prediction
plot below.

.. figure:: figures/psc10.1.png
    :align: center
    :width: 100%


Markers
--------------------------------------------------------------------------------
The **Markers** panel produces for the top marker genes, a t-SNE with samples 
colored in red when the gene is overexpressed in corresponding samples. 
The top genes (N=36) with the highest standard deviation are plotted.

In the plotting *Settings*, users can also restrict the marker analysis by 
selecting a particular functional group in which genes are divided into 89 groups,
such as chemokines, transcription factors, genes involved in immune checkpoint 
inhibition, and so on.

.. figure:: figures/psc10.2.0.png
    :align: center
    :width: 30%

    
.. figure:: figures/psc10.2.png
    :align: center
    :width: 100%


CNV
--------------------------------------------------------------------------------
It is also possible to perform a gene copy number variation (CNV) analysis under 
the **CNV** tab. The copy number is estimated from gene expression data by 
computing a moving average of the relative gene expression along the chromosomes.
A heatmap of samples versus chromosomes is generated, where samples can be 
annotated further with a phenotype class provided in the data.

.. figure:: figures/ug.036.png
    :align: center
    :width: 100%



Proportions
--------------------------------------------------------------------------------
The **proportions** tab visualizes the interrelationships between two categorical
variables (so-called cross tabulation). Although this feature is very suitable
for a single-cell sequencing data, it provides useful information about the
proportion of different cell types in samples obtained by the bulk sequencing method.

.. figure:: figures/ug.033.png
    :align: center
    :width: 100%



Cytoplot
--------------------------------------------------------------------------------
For each gene pairs combination, the platform can generate a cytometry-like plot 
of samples under the **cytoplot** tab. The aim of this feature is to observe
the distribution of samples in relation to the selected gene pairs. For instance,
when applied to single-cell sequencing data from immunological cells, it can mimic
flow cytometry analysis and distinguish T helper cells from other T cells by 
selecting the CD4 and CD8 gene combination.

.. figure:: figures/ug.034.png
    :align: center
    :width: 100%


