.. _microarray_data:

Microarray Data
================================================================================


To illustrate the use cases of the Omics Playground, we reanalyzed some publics
data sets.

\ref{results_figure3}b} shows a microarray gene expression data set, GSE10846 
\cite{Lenz2018Stromal}, of diffuse large B-cell lymphoma (DLBCL).


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