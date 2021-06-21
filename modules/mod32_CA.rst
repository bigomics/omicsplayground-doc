.. _Correlation analysis:

Correlation analysis
================================================================================

Input panel
--------------------------------------------------------------------------------
Users can find more information by clicking ``Info``. The panel contains the main settings for the analysis. 
The analysis can be started by selecting a gene of interest from the ``Gene`` settings. 
Under *Options*, users can filter for a specific gene family by using the ``Gene family`` setting.
By using the ``Filter samples`` setting they con focus only on specific sample groups.


.. figure:: figures/psc4.5.0.png
    :align: center
    :width: 30%


Correllation
--------------------------------------------------------------------------------
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
--------------------------------------------------------------------------------
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