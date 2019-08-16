.. _DEGs:

Differential expression analysis
================================================================================

The expression module contains a differentially expressed genes (DEG) analysis 
between contrasts (eg, tumor vs. control). The analysis begins with the selection 
of a contrast. There are further options to filter out some genes by functional 
families, logarithmic fold change (logFC) and false discovery rate (FDR).


Expression table
--------------------------------------------------------------------------------
DEG analysis is performed using four commonly accepted methods, namely: 
t-test (standard, Welch), limma (no trend, trend, voom), edgeR (QLF, LRT), 
and DESeq2 (Wald, LRT) \cite{ritchie2015limma, robinson2010edger, love2014moderated}.
For each selected contrast, the results of these methods are combined and reported 
under the \texttt{table} section, where meta.q for a gene represents the highest q 
value among the methods and the number of starts indicates how many methods have 
significant q values (q $<$ 0.05). Users can sort genes by logFC, meta.q, or average 
expression in an interactive table. 


Plots
--------------------------------------------------------------------------------
By clicking on a gene, it is possible to see which
gene sets include that gene, and check the status of the differential expression in 
other comparisons from the \texttt{plots} section.  The section can also display 
volcano and MA plots (\textbf{Supp. Fig. 11}). 


Top genes
--------------------------------------------------------------------------------
Furthermore, for the top 10 DEGs 
within the selected comparison, average expression plots across the samples are 
displayed in the \texttt{top genes} section (\textbf{Supp. Fig. 12}). 


Volcano (all)
--------------------------------------------------------------------------------
Another important feature of this module is the simultaneous visualisation of volcano
plots for all comparisons under the \texttt{volcano (all)} section (\textbf{Supp. Fig. 13}).

