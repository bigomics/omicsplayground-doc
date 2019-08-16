.. _Functional:

Functional analysis
================================================================================

This module provides higher level functional and visual analysis of the contrast space using the KEGG and GO graph structures. Given the profile of a particular contrast, it also searches for the closest drug profiles from the L1000 drug expression database \cite{subramanian2017next}.

Within the \texttt{KEGG graph} section, each pathway is scored for the selected contrast profile and reported in an interactive table. The scoring is performed by considering the total number of genes in the pathway (n), the number of genes in the pathway supported by the contrast profile (k), the ratio of k/n, and the ratio of $|$upregulated or downregulated genes$|$/k. Additionally, the table contains the list of the upregulated and downregulated genes for each pathway and a q value from the Fisher's test for the overlap. Pathway maps can be summoned from the interactive table, with individual genes coloured according to their differential expression (upregulation: red;  downregulation: blue). Another important feature is an activation-heatmap including the comparison of activation levels of pathways (or pathway keywords) across multiple contrast profiles (\textbf{Supp. Fig. 18}). 

All the features described under the \texttt{KEGG graph} tab, such as scoring the gene sets and drawing an activation-heatmap, can be performed for the GO database under the \texttt{GO graph} tab. Instead of pathway maps, an annotated graph structure provided by the GO database is plotted for every selected gene set (\textbf{Supp. Fig. 19}).

The drug connectivity map (\texttt{Drug C-Map}) section correlates the selected contrast profile with more than 5000 known drug profiles from the L1000 database \cite{subramanian2017next}, and shows the top 10 similar and opposite profiles by running the GSEA algorithm \cite{sergushichev2016algorithm} on the contrast-drug profile correlation space. It also provides an activation-heatmap for drugs across multiple contrast profiles. Users can perform the contrast-drug profile correlation analysis in mono (single drug) or combo (combination of two drugs) mode (\textbf{Supp. Fig. 20}).

