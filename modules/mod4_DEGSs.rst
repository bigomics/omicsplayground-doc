.. _DESGs:

Gene set enrichment analysis
================================================================================

This module visualises a differential expression analysis at a gene set level. 
Expression analysis for each gene set (or pathway) is computed from gene expression 
data using summary methods such as GSVA and ssGSEA \cite{hanzelmann2013gsva}. 
The platform has more than 50,000 gene sets and pathways in total, which are divided 
into 30 gene set collections such as Hallmark, MSigDB, KEGG and 
GO \cite{liberzon2015molecular, kanehisa2000kegg, gene2004gene}. 


Enrichment table
--------------------------------------------------------------------------------
:**A**: To perform the enrichment analysis, users have to first specify the 
        contrast they want to visually analyze using a particular gene 
        set collection. Gene sets can be optionally filtered by :option:`logFC` and 
        :option:`FDR` thresholds before performing the analysis.
        
:**B**: To ensure statistical reliability, the platform performs GSE analyses 
        using seven different methods, including Spearman rank correlation, GSVA, 
        ssGSEA, Fisher's exact test, GSEA, camera and fry \cite{kofler2012gowinda, 
        hanzelmann2013gsva, fisher1922interpretation, sergushichev2016algorithm, kuhl2011camera}. 
        
:**C**: Then the combined result from multiple methods is displayed under the 
        ``enrichment table``, where for each geneset the :option:`meta.q` corresponds
        to the highest :option:`q` value provided by the methods and the number of 
        stars indicate how many methods identified the geneset as significant 
        (:option:`q < 0.05`). The table is interactive; users can sort it by 
        :option:`logFC`, :option:`meta.q` and :option:`starts`.

.. figure:: figures/ug.015.png
    :align: center
    :width: 100%


Top enriched
--------------------------------------------------------------------------------
For a selected comparison in ***A*, top ten differentially enriched geneses or pathways
(five positive abd five negative) are displayed under top enriched section.

.. figure:: figures/ug.015.png
    :align: center
    :width: 100%


Plots
--------------------------------------------------------------------------------
:**E**: For a selected geneset from the enrichment table in **C**, a volcano plot
        of its genes and barplots of expressions per phenotype class are displayed
        under the ``plots`` tab.

:**E**: For a selected geneset from the enrichment table, it is also possible to 
        see the expression barplots per sample group and a scatter plot of gene to
        geneset expressions.

:**F**: Additionally, the gene list of the selected gene set in **C** is also
        visualised in a separate table with further statistics. 

.. figure:: figures/ug.016.png
    :align: center
    :width: 100%


Compare
--------------------------------------------------------------------------------
Individual gene sets expression profiles can be visualised 
against all available contrasts (\texttt{compare} tab) (\textbf{Supp. Fig. 16}).


Volcano (all)
--------------------------------------------------------------------------------
Under the \texttt{volcano (all)} tab, volcano plots for all contrasts are 
displayed (\textbf{Supp. Fig. 17}).

