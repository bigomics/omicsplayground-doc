.. _Clustering:

Clustering
================================================================================

The **Clustering** module performs unsupervised clustering analysis of the data. 
After having done the QC, it is probably the first way to explore your data. 
The main purpose is to discover patterns and subgroups in the data, show correlation
with known phenotypes, detect outliers, or investigate batch effects.

In the **Heatmap** panel hierarchical clustering can be performed on gene level 
or gene set level. The **PCA/tSNE** panel shows unsupervised clustering of the samples 
in 2D/3D as obtained by PCA or tSNE algorithms. The **Parallel** panel displays the 
expression levels of selected genes across all conditions.
On the right, the **Annotate cluster** panel provides a functional annotation for each 
feature cluster in the heatmap. Users can select from a variety of annotation databases 
from the literature. The **Phenotypes** panel shows the phenotype distribution as colors
on the t-SNE plot. Finally, the **Feature ranking** panel  shows a plot that ranks 
the discriminative power of feature sets (or gene sets) as the cumulative discriminant 
score for all phenotype variables.


Input panel
--------------------------------------------------------------------------------
Users can find more information by clicking ``Info`` in the input
panel. It also contains main settings for the analysis, where users can select
 a family of features in the ``Features`` scroll-down menu, group samples by phenotype
 using ``Group by`` and filter and select samples with ``Filter samples``. 
 Furthermore, under *Options*, users can choose the level of analysis (gene or geneset) 
 and exclude genes in the X and Y chromosomes

.. figure:: figures/psc3.0.png
    :align: center
    :width: 30%


Heatmap
--------------------------------------------------------------------------------
In the **Heatmap** panel hierarchical clustering can be performed on
gene level or gene set level expression. For the latter, for each gene
set (or pathway), a single-sample enrichment value is computed from
the gene expression data using summary methods such as `GSVA
<https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-7>`__
and `ssGSEA
<https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-7>`__.

Under the plot configuration settings, usesrs can select to display a static or interactive hetmap.
Users can also split the samples by a phenotype class (e.g., tissue, cell type, or gender) using the
 ``split`` by setting. In addition, users can specify the top N = (50, 150, 500) features to be used 
 in the heatmap.
 The ordering of top features is selected under ``top mode``. The criteria to select the top features are:

* SD - features with the highest standard deviation across all the samples,
* specific - features that are overexpressed in each phenotype class compared to the rest, or by
* PCA - by principal components.

The number of gene clusters to be displayed can be selected under ``K``.
Users can also choose between 'relative' or 'absolute' expression
scale. Under the ``CexCol`` and ``CexRow`` settings, it is also possible to adjust the font sizes
for the column and row labels.

.. figure:: figures/psc3.1.0.png
    :align: center
    :width: 30%
        
The complex heatmap below is generated after tuning the options and settings. 
It is a clustered heatmap showing gene expression sorted by 2-way hierarchical
clustering. Red corresponds to overexpression, blue to underexpression of the gene.
At the same time, gene clusters are functionally annotated in the **Annotate clusters**
panel on the right.

.. figure:: figures/psc3.1.png
    :align: center
    :width: 100%

The **iHeatmap** is an interactive version of the clustered heatmap
and can be selected in the plot settings. Users are warned that for
large datasets (such as single-cell RNA-seq data) this plot can become
rather slow.

.. figure:: figures/psc3.2.png
    :align: center
    :width: 100%


Annotate clusters
--------------------------------------------------------------------------------
The features in the heatmap are divided into clusters depending on the
selected ``top mode`` in the heatmap panel settings. For each cluster,
the **Annotate cluster** section provides a functional annotation
using more than 42 published reference databases, including but not
limited to well-known databases such as `MSigDB
<http://software.broadinstitute.org/gsea/msigdb/index.jsp>`__, `KEGG
<https://www.ncbi.nlm.nih.gov/pmc/articles/PMC102409/>`__, and `GO
<http://geneontology.org/>`__.  In the plot settings, users can
specify the level and reference set to be used under the ``Reference
level`` and ``Reference set`` settings, respectively. 
Users can also select a Fisher test weighting for gene sets.

.. figure:: figures/psc3.4.0.png
    :align: center
    :width: 30%

The functional annotation for the clusters are displayed below, with
the highest ranking annotation features (by correlation) displayed for
each gene cluster. Length of the bars corresponds to the average
correlation of the cluster with the annotation term. In the table
below the barplots, users can view the correlation values of
annotation features for each cluster.

.. figure:: figures/psc3.4.png
    :align: center
    :width: 100%


PCA/tSNE
--------------------------------------------------------------------------------
The **PCA/tSNE** panel visualizes unsupervised clustering obtained by the principal
components analysis (`PCA <https://www.ncbi.nlm.nih.gov/pubmed/19377034>`__) or 
t-distributed stochastic embedding 
(`tSNE <http://jmlr.org/papers/volume15/vandermaaten14a/vandermaaten14a.pdf>`__) algorithms. 
This plot shows the relationship (or similarity) between the samples for visual 
analytics, where similarity is visualized as proximity of the points. 
Samples that are 'similar' will be placed close to each other.

Users can customise the PCA/tSNE plot in the plot settings, including
the ``color`` and ``shape`` of points using a phenotype class, label the points, 
display 2D and 3D visualisation of the PCA/tSNE plot, normalize the matrix and choose
between a t-SNE, PCA or UMAP ``layout``. The number of genes to be considered for 
dimensionality reduction can also be altered via ``Ntop``.

.. figure:: figures/psc3.3.0.png
    :align: center
    :width: 30%

Based on their configuration settings, users will obtain a similar
PCA/tSNE plot as below.

.. figure:: figures/psc3.3.png
    :align: center
    :width: 100%


Parallel
--------------------------------------------------------------------------------
The **Parallel** panel visualizes the expression levels of selected genes across all conditions.
The expression values are scaled but scaling can be removed via the plot settings.
This interactive plot is particularly useful to users working with time series experiments, 
as samples can be grouped by condition (i.e. time) and ordered manually, as shown below.
A table containing average expression levels of selected genes across conditions is also generated.


.. figure:: figures/psc3.3B.png
    :align: center
    :width: 100%
    

Phenotypes
--------------------------------------------------------------------------------
The **Phenotypes** panel visualizes the distribution of the available phenotype data. 
It provides plots showing the distribution of the phenotypes superposed on the 
tSNE clustering. Often, we can expect the t-SNE distribution to be driven by the
particular phenotype that is controlled by the experimental condition or unwanted
batch effects. Users can choose to put the group labels in the 
figure or as separate legend in the ``Label`` setting, under the plot *Settings*.

.. figure:: figures/psc3.5.0.png
    :align: center
    :width: 30%

The output figure of the panel (phenotype distribution) is shown below. 
    
.. figure:: figures/psc3.5.png
    :align: center
    :width: 100%


Feature ranking
--------------------------------------------------------------------------------
The **Feature ranking** panel provides the ranked discriminant score for top feature sets.
It ranks the discriminitive power of the feature set (genes or gene sets) as a 
cumulative discriminant score for all phenotype variables. 
In this way, we can find which feature set (gene or gene family/set) can explain 
the variance in the data the best.

Under the plot configuration *Settings*, users can specify the ``Method`` for 
computing the discriminant score.

.. figure:: figures/psc3.6.0.png
    :align: center
    :width: 30%

* P-value based scoring is computed as the average negative log p-value from the ANOVA.
* Correlation-based discriminative power is calculated as the average '(1-cor)' 
  between the groups. Thus, a feature set is highly discriminative if the 
  between-group correlation is low.
* The 'meta' method combines the score of the former methods in a multiplicative manner.
 

The following plot represents the resulting feature-set ranking.

.. figure:: figures/psc3.6.png
    :align: center
    :width: 100%
