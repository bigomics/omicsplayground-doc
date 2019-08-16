.. _Signature:

Signature analysis
================================================================================

In this module, users can test gene signatures by calculating an enrichment score.
They can use a sample list provided on the platform or upload their own gene list.
Instead of a short list, a profile can also be selected, which is a complete gene
list derived from one of the contrasts in the analysis.


Markers
--------------------------------------------------------------------------------
After uploading a gene list, the \texttt{markers} section produces a t-SNE plot of 
samples for each gene, coloured by expression levels (upregulation: red;  
downregulation: blue) (\textbf{Supp. Fig. 25}). 


Phenotypes
--------------------------------------------------------------------------------
??


Enrichment
--------------------------------------------------------------------------------
The \texttt{enrichment} tab performs
the enrichment analysis of the gene list against all contrasts by running the GSEA
algorithm \cite{sergushichev2016algorithm} and plots enrichment outputs. 


Signature c-map
--------------------------------------------------------------------------------
The \texttt{signature c-map} section associates the provided signature list or contrast
profile with similar profiles of other experiments, obtained from ten published 
datasets. 


Overlap/similarity
--------------------------------------------------------------------------------
Finally, under the \texttt{overlap/similarity} tab, users can compare
their gene list with all the gene sets and pathways in the platform through statistics
such as the total number of genes in the gene set (K), the number of intersecting genes
between the list and the gene set (k), the overlapping ratio of k/K, as well as the p
and q values by the Fisher's test for the overlap test (\textbf{Supp. Fig. 26-28}).


