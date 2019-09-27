.. _examples:

Reanalyzing Public Datasets
================================================================================
To illustrate the use case of the Omics Playground, we reanalyzed different types
of publics datasets to recapitulate similar results, including microarray,
bulk RNA-seq, single-cell RNA-seq and proteomic datasets.


Single-cell RNA-seq data
--------------------------------------------------------------------------------
For single-cell RNA-seq data, we downloaded the melanoma data set 
`GSE72056 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72056>`__ of
`Tirosh et al. <https://www.ncbi.nlm.nih.gov/pubmed/27124452>`__.
Our platform recapitulates well the original findings of the paper. 
The t-SNE clustering (**Fig. 1**) separates the different cell types. 
Fig. 2 and 3 show the volcano plot, MA plot and most differentially
expressed genes between malignant and non-malignant cells. 
The CNV map (Fig. 2d) confirms the major chromosomal copy number 
variations found in the malignant cells. Fig. 2e shows high enrichment
of a immune checkpoint signature, particularly concentrated in the T cells.
The biomarker heatmap (Fig. 2f) highlights the marker genes for
each cell type. Each gene cluster is furthermore automatically
annotated with the most correlated gene sets (Fig. 2g).

.. figure:: figures/fig2_a.pdf 
    :align: center
    :width: 50%
    

.. figure:: figures/fig2_b.pdf
    :align: center
    :width: 100%    
    
.. figure:: figures/fig2_c.pdf
    :align: center
    :width: 100%     

.. figure:: figures/fig2_d.pdf
    :align: center
    :width: 100% 
    
.. figure:: figures/fig2_e.png
    :align: center
    :width: 100%   
    
.. figure:: figures/fig2_f.pdf
    :align: center
    :width: 100% 
    
.. figure:: figures/fig2_g.pdf
    :align: center
    :width: 100%     

.. figure:: figures/fig2_h.pdf
    :align: center
    :width: 100% 

    
Microarray Data
--------------------------------------------------------------------------------

In this section, we perform the biomarker selection and 
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




RNA-sequencing Data
--------------------------------------------------------------------------------

To elucidate the mechanism of action of a new drug, or for the intention of drug 
repurposing, it is often useful to find other drugs that have similar or opposing
signatures compared to some given fold change profile.

As an example, using data from GSE114716
from \cite{Goswami2018Modulation}.

GSE114716: Drug mechanism of action 

Signature
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure2}f} shows the top ranked drugs with most similar
or most opposing signatures to Ipilimumab, a novel monoclonal antibody targeting
CTLA-4 used in tumour therapy. 

Biomarker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The list contains several known anti-tumoral drugs, such as bortezomib and 
palbociclib, but also highlights relationships with other compounds not normally
used in tumor therapy, such as emetine, an anti-protozoal drug with anti-tumoral
properties \cite{Foreman2018Emetine, Sun2015TheAlkaloid}.



Single-cell Data
--------------------------------------------------------------------------------

For single-cell RNA-seq data, we downloaded the melanoma data set 
`GSE72056 <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72056>`__ 
of `Tirosh et al <https://www.ncbi.nlm.nih.gov/pubmed/27124452>`__. 

t-SNE clustering
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Our platform recapitulates well the original findings of the paper. 
The t-SNE clustering separates the different cell types. 

Volcano plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure2}b} and \textbf{\ref{results_figure2}c} show the 
volcano plot, MA plot and most differentially expressed genes between malignant 
and non-malignant cells. 

CNV plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The CNV map (\textbf{Fig. \ref{results_figure2}d}) confirms the major chromosomal
copy number variations found in the malignant cells. 

Signature
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
\textbf{Fig. \ref{results_figure2}e} shows high enrichment of a immune checkpoint
signature, particularly concentrated in the T cells. 

Biomarker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The biomarker heatmap (\textbf{Fig. \ref{results_figure2}f}) highlights the marker
genes for each cell type. Each gene cluster is furthermore automatically annotated
with the most correlated gene sets (\textbf{Fig. \ref{results_figure2}g}). 



Proteomic Data
--------------------------------------------------------------------------------

With larger data sets, often the number of contrasts increases and complicates 
the overall analysis. 
For example, the proteomics data set of 
`Rieckmann et al. 2017 <https://www.ncbi.nlm.nih.gov/pubmed/28263321>`__
comprises 26 populations of seven major immune cell types, measured during resting and activated
states. There are more than 300 possible comparisons to make.


For example, the proteomics data set of 
`Rieckmann et al. 2017 <https://www.ncbi.nlm.nih.gov/pubmed/28263321>`__
comprises 26 
populations of seven major immune cell types, measured during resting and activated
states. There are more than 300 possible comparisons to make. 

Connectivity heatmap
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To gain a better overview, gene set connectivity heatmaps (\textbf{Fig. \ref{results_figure3}e})
help visualize the similarities between multiple contrasts on a functional level. 

Connectivity graph
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Alternatively, similarities can be visualized as a connectivity graph
(\textbf{Fig. \ref{results_figure3}f}). 

Classification tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For the same data set, \textbf{Fig. \ref{results_figure3}g} shows a computed 
partition tree that classifies the major cell types.