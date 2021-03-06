.. _Expression:

Expression
================================================================================

The **Expression** module is divided into two main panels. The **Differential Expression** 
panel compares expression between two conditions (i.e. tumor versus control), 
which is one of the fundamental analysis in the transcriptomics data analytics workflow. 
For each comparison of two conditions (also called a 'contrast'), the analysis identifies 
which genes are significantly downregulated or overexpressed in one of the groups.

The **Correlation Analysis** panel computes the correlation between genes and finds 
coregulated modules.


Differential expression
--------------------------------------------------------------------------------

Input panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The input panel on the left contains a link to a tutorial for relevant, as well as some settings 
for the analysis. Users can start the differntial expression (DE) analysis by selecting a contrast 
of their interest in the ``Contrast`` setting and specifying a relevent gene family in the 
``Gene family`` setting. It is possible to set the false discovery rate (FDR) and the 
logarithmic fold change (logFC) thresholds under the ``FDR`` and ``logFC threshold`` settings, respectively. 
Under "Options", users can select to display all genes in the table (not only significant genes) 
and also select different combinations of statistical methods for the analysis.

.. figure:: figures/psc4.0.png
    :align: center
    :width: 30%

Table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Table ``I`` shows the results of the statistical tests slected in the 
``Statistical methods``. By default, this table reports 
the meta (combined) results of 
`DESeq2 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4302049/>`__ (Wald),
`edgeR <https://www.ncbi.nlm.nih.gov/pubmed/19910308>`__ (QLF), and 
`limma <https://www.ncbi.nlm.nih.gov/pubmed/25605792>`__ (trend) only.
Users can filter top N = {10} differently expressed genes in the table by 
clicking the ``top 10 genes``  and also show the q-values from individual statistical methods 
by ticking ``show individual q-values`` from the table *Settings*.

.. figure:: figures/psc4.1.0.png
    :align: center
    :width: 30%
    
For a selected comparison under the ``Contrast`` setting, the results of the selected 
methods are combined and reported in Table ``I``, where ``meta.q`` for a gene 
represents the highest ``q`` value among the methods and the number of stars for 
a gene indicate how many methods identified significant ``q`` values (``q < 0.05``). 
The table is interactive (scrollable, clickable); users can sort genes by ``logFC``, 
``meta.q``, or average expression in either conditions.

.. figure:: figures/psc4.1.png
    :align: center
    :width: 100%

By clicking on a gene in the Table ``I`` (highlighted in purple in the figure), 
it is possible to see the correlation and enrichment value of gene sets that 
contain the gene in Table ``II``.

Foldchange (all)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Foldchange (all)** tab reports the gene fold changes for all contrasts in the selected dataset.
The column ``fc.var`` corresponds to the variance of the fold-change across all contrasts.


.. figure:: figures/psc4.1.1.png
    :align: center
    :width: 100%

FDR table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **FDR table** tab reports the number of significant genes at different FDR thresholds for 
all contrasts and methods within the dataset. This enables to quickly see which 
methods are more sensitive. The left part of the table (in blue) correspond 
to the number of significant down-regulated genes, the right part (in red) 
correspond to the number of significant overexpressed genes.


.. figure:: figures/psc4.1.2.png
    :align: center
    :width: 100%

Plot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Plot** panel shows the following plots:

:**a**: An interactive volcano plot for the chosen contrast. Unless a specific gene is selected 
        from the differential expression analysis table, all significant genes are highlighted in blue.

:**b**: An interactive MA plot for the chosen contrast. Unless a specific gene is selected 
        from the differential expression analysis table, all significant genes are highlighted in blue.

:**c**: Differential expression boxplot for a gene that is selected from the 
        differential expression analysis table. Users can customise the plot via the settings icon on top 
        to ungroup samples and change the scale to counts per million (CPM).

:**d**: Fold change summary barplot across all contrasts for a gene that is selected 
        from the differential expression analysis table.

.. figure:: figures/psc4.1.3.png
    :align: center
    :width: 100%

Top genes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Top genes** section shows the average expression plots across the samples for the top differentially 
(both positively and negatively) expressed genes for the selected comparison from the ``Contrast`` setting.


.. figure:: figures/psc4.2.png
    :align: center
    :width: 100%

The plot can be customised via the settings to remove the log scale, ungroup samples and show only samples 
included in the selected contrast.


.. figure:: figures/psc4.2.0.png
    :align: center
    :width: 30%

Volcano (all)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the **Volcano (all)** tab, the platform simultaneously displays multiple volcano plots 
for genes across all contrasts. By comparing multiple volcano plots, 
the user can immediately see which comparison is statistically weak or strong.
Experimental contrasts with better statistical significance will show 
volcano plots with 'higher' wings.


.. figure:: figures/psc4.3.png
    :align: center
    :width: 100%

Volcano (methods)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the **Volcano (methods)** tab, the platform displays the volcano plots provided by 
multiple differential expression calculation methods for the selected contrast. 
Methods showing better statistical significance will show volcano 
plots with 'higher' wings.


.. figure:: figures/psc4.4.png
    :align: center
    :width: 100%


Correlation analysis
--------------------------------------------------------------------------------

Input panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users can find more information by clicking ``Info``. The panel contains the main settings for the analysis. 
The analysis can be started by selecting a gene of interest from the ``Gene`` settings. 
Under *Options*, users can filter for a specific gene family by using the ``Gene family`` setting.
By using the ``Filter samples`` setting they con focus only on specific sample groups.


.. figure:: figures/psc4.5.0.png
    :align: center
    :width: 30%

Correllation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the **Correlation** tab, the platform displays three different outputs:

:**a**: A plot displaying the highest correlated genes in respect to the selected gene. 
        The plot can be customised via the settings icon on top to include no partial correlection, 
        a fast partial correlation calculation or a calculation with all methods. 


.. figure:: figures/psc4.5.1.png
    :align: center
    :width: 30%


:**b**: A correlation graph centered on selected gene with top most correlated features.
        The plot can be customised via the settings icon on top. From it users can adjust the rho value 
        via a sliding bar and change the graph layout via ``Layout``.


.. figure:: figures/psc4.5.2.png
    :align: center
    :width: 30%


:**c**: Pairwise scatter plots for the expression values of the gene pairs across the samples.


.. figure:: figures/psc4.5.png
    :align: center
    :width: 100%

Functional
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Four outputs are generated under the **Functional** tab:

:**a**: A series of gene set enrichment analysis (GSEA) plots using the correlation as rank metric.
        The black bars denote the genes in the gene set and their position in the sorted rank metric.

:**b**: A table containing the statistical results from the GSEA. The table displays 
        normalised enrichment scores (NES), adjusted and non-adjusted p-values,size of the gene set 
        and a link to gene set information.

:**c**: A plot of the frequency of leading edge genes in top correlated genesets.

:**d**: A table of the leading edge genes and rank statistics (rho) of the selected geneset.


.. figure:: figures/psc4.6.png
    :align: center
    :width: 100%


    