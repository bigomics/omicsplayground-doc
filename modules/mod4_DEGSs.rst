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
Users specify which contrast they want to visually analyze using a particular gene 
set collection. To ensure statistical reliability, the platform performs GSE 
analyses using seven different methods, including Spearman rank correlation, GSVA, 
ssGSEA, Fisher's exact test, GSEA, camera and fry \cite{kofler2012gowinda, 
hanzelmann2013gsva, fisher1922interpretation, sergushichev2016algorithm, kuhl2011camera}. 
The results are combined and gene sets can be optionally filtered by logFC and 
FDR thresholds before being visualised in an interactive and sortable table under
the  \texttt{enrichment table} menu (\textbf{Supp. Fig. 14}). 


Top enriched
--------------------------------------------------------------------------------
For each gene set, 
a meta.q value and stars qualifier are calculated as described previously and volcano 
plots of its genes and barplots of expressions per phenotype class are displayed 
(under \texttt{plots}) (\textbf{Supp. Fig. 15}). Additionally, the list of genes in 
that gene set are visualised in a separate table and for every gene it is possible 
to see the barplot of expressions per phenotype class and a scatter plot of gene to 
gene set expressions. 


Plots
--------------------------------------------------------------------------------
For each gene set, 
a meta.q value and stars qualifier are calculated as described previously and volcano 
plots of its genes and barplots of expressions per phenotype class are displayed 
(under \texttt{plots}) (\textbf{Supp. Fig. 15}). Additionally, the list of genes in 
that gene set are visualised in a separate table and for every gene it is possible 
to see the barplot of expressions per phenotype class and a scatter plot of gene to 
gene set expressions. 


Compare
--------------------------------------------------------------------------------
Individual gene sets expression profiles can be visualised 
against all available contrasts (\texttt{compare} tab) (\textbf{Supp. Fig. 16}).


Volcano (all)
--------------------------------------------------------------------------------
Under the \texttt{volcano (all)} tab, volcano plots for all contrasts are 
displayed (\textbf{Supp. Fig. 17}).

