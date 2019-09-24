.. _microarray_data:

Microarray Data
================================================================================

We reanalyzed different types of publics datasets to illustrate the use case of 
the Omics Playground. In this section, we perform the biomarker selection and 
survival analysis using the 
`GSE10846 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE10846>`__
microarray gene expression dataset of diffuse large B-cell lymphoma (DLBCL) 
patients.


Volcano plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure3}a} shows the volcano plots corresponding to eight
different statistical tests comparing time-dependent activation of T cells at 
48h vs. 12h \cite{Geiger2016Larginine}. We see that both standard t-test and the 
Welch t-test show much less power to detect significant genes compared to the other
methods. The result from edgeR-QLF is close to those of the two limma based methods,
while edgeR-LRT is very similar to the results of DESeq2-Wald. \textbf{Fig.


Biomarker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure3}c} and \textbf{\ref{results_figure3}d} show the 
variable importance plot and a survival tree on the overall survival of the DLBCL 
patients, respectively.


Survival analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure3}c} and \textbf{\ref{results_figure3}d} show the 
variable importance plot and a survival tree on the overall survival of the DLBCL 
patients, respectively.