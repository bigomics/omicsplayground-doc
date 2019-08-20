.. _DEGs:

Differential expression analysis
================================================================================

The expression module contains a differentially expressed genes (DEG) analysis 
between contrasts (eg, tumor vs. control).


Expression table
--------------------------------------------------------------------------------

:**A**: The user starts the DEG analysis by selecting a desireable contrast form
        the drop-down menu items.

:**B**: There are further options to filter out some genes by functional 
        families, logarithmic fold change (logFC) and false discovery rate (FDR).

:**C**: To increase the statistical reliability of the platform, the DEG analysis
        is performed using four commonly accepted methods in the literature, namely: 
        t-test (standard, Welch), 
        `limma <https://www.ncbi.nlm.nih.gov/pubmed/25605792>`__ (no trend, trend, voom), 
        `edgeR <https://www.ncbi.nlm.nih.gov/pubmed/19910308>`__ (QLF, LRT), 
        and 
        `DESeq2 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4302049/>`__ (Wald, LRT).

:**D**: For each selected contrast in **A**, the results of these methods are combined
        and reported under the ``DEG table`` section, where :option:`meta.q` for a gene 
        represents the highest :option:`q` value among the methods and the number of starts 
        indicates how many methods have significant q values (:option:`q < 0.05`). Users 
        can sort genes by :option:`logFC`, :option:`meta.q`, or average expression
        in an interactive table. 

:**E**: By clicking on a gene row in **D**, it is possible to see which genesets contain
        that gene from the geneset table located on the right. 

.. figure:: figures/ug.012.png
    :align: center
    :width: 100%


Plots
--------------------------------------------------------------------------------
:**F**: The ``plots`` section provides volcano  and MA (an application 
        of a Bland-Altman) plots.  
        
:**G**: This section shows the so-called 'signature', i.e. the top downregulated
        and overexpressed genes, for that contrast. The expression of the selected
        gene across all contrasts is also summarized. By clicking on a gene 
        row in **D**, it is possible to check the status of the differential 
        expression of that particular gene accross other comparisons.  

.. figure:: figures/ug.012.png
    :align: center
    :width: 100%


Top genes
--------------------------------------------------------------------------------
Furthermore, for the top 10 DEGs 
within the selected comparison, average expression plots across the samples are 
displayed in the ``top genes`` section. 

.. figure:: figures/ug.013.png
    :align: center
    :width: 100%

Volcano (all)
--------------------------------------------------------------------------------
Another important feature of this module is the simultaneous visualisation of volcano
plots for all comparisons under the ``volcano (all)`` section. This can provide
the user a statistical overview all comparisons at the same time, and the user
can immediately see which comparison is statistically weak or strong.


.. figure:: figures/ug.014.png
    :align: center
    :width: 100%
    
    
    