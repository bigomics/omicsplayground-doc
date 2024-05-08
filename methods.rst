.. _Methods:


Methods
================================================================================


Here, we provide descriptions of the bioinformatic techniques and methods used in Omics Playground. You may want to use these information to describe the methods when using the Omics Playground. You can always access the R code (on github) to check exactly all steps implemented, or you can contact the bioinformatic staff at BigOmics Analytics should you have questions. 


Batch correction 
-----------------

Batch effects, or contamination by unwanted variables, was identified
by an F-test for the first three principal components. Continuous
variables were dichotomized into high/low before testing. Highly
confounding variables would appear as having high relative
contribution in the first or second principal component, often higher
than the variable of interest. Batch effects were also visually
assessed (before and after correction) using annotated heatmaps and
t-SNE plots colored by variables.

Batch correction was performed for explicit batch
variables or unwanted covariates. Parameters with a correlation r>0.3
with any of variables of interest (i.e. the model parameters) were
omitted from the regression. Correction was performed by regressing
out the covariate using the 'removeBatchEffect' function in the limma
R/Bioconductor package.

Technical correction was performed for intrinsic technical parameters such as library size (i.e. total
counts), mitochondrial and ribosomal proportions, cell cycle and
gender. These parameters were estimated from the data. The cell cycle
was estimated using the Seurat R/Bioconductor package. Gender (if not
given) was estimated by checking the absence/presence of expression of
gender specific genes on the X/Y chromosome. Parameters with a
correlation r>0.3 with any of the model parameters were omitted from
the regression. Correction was performed by regressing out the
covariate using the 'removeBatchEffect' function in the limma
R/Bioconductor package.

Unsupervised batch correction was performed using
'surrogate variable analysis' (SVA) (Leek 2007) by estimating the
latent surrogate variables and regressing out using the
'removeBatchEffect' function in the limma R/Bioconductor package.


Clustering
---------------------------

Heatmaps were generated using the ComplexHeatmap R/Bioconductor
package (Gu 2016) on scaled log-expression values (z-score) using
euclidean distance and Ward linkage. The standard deviation was used
to rank the genes for the reduced heatmaps.

T-distributed stochastic neighbor embedding (t-SNE) is a non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Unlike linear dimensionality reduction techniques like PCA, t-SNE may separate data that is not linearly separable. Furthermore, while PCA tends to preserve the global information in the data, t-SNE tends to preserve relative distances. t-SNE first calculates the distance between every pair of data points. Each data point is then placed within a Gaussian distribution while all other data points are distributed according to their distance. Points closer each other are more similar. Point more distanced are more diverse each other. A value, called 'Perplexity', is calculated to reflect the standard deviation of the data. The Perplexity value is the number of nearest neighbors considered in generating the probability of points being close each other. Smaller perplexity values may result in very localized outputs ignoring global information, while larger values may obscure smaller structures. For this reason, the Perplexity value is intended to be less than the size of data. Recommended values are in the range 5-50. To determine the representation of the data in the low dimensional space, a t-distribution is used with one degree of freedom. A gradient descent optimization involving an iterative process, is finally employed to determine the final low-dimensional data representation that reflects the high-dimension accurately. In OPG t-SNE is computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the t-SNE embedding. The perplexity heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation was performed using the `Rtsne` R package.

Uniform Manifold Approximation and Projection (UMAP) is another non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Similarly to t-SNE, UMAP can effectively separate data that is not linearly separable. When compared to t-SNE, UMAP tends to more clearly separate groups of similar categories from each other. Generally, UMAP can also preserve the global structure more than t-SNE. UMAP computation is also generally faster than t-SNE. To construct the initial high-dimensional graph, UMAP builds a weighted graph with edge weights representing the likelihood that two points are connected. Connectedness is inferred through radii outwards from each point. Smaller radii result to small, isolated clusters. Larger radii result to overconnection. To reduce these potential issues, each radius is chosen locally, based on the between each point and its nearest neighbor. UMAP then makes the graph "fuzzy" by decreasing the likelihood of connection as the radius grows. UMAP then projects the data into lower dimensions through a force-directed graph layout algorithm in a similar way than t-SNE. By ensuring that each point is connected to at least its closest neighbor, UMAP enables preservation of the local structure with respect to the global structure. In the OPG, UMAP was computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the UMAP embedding. The number of neighbours was heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation w as performed using the `uwot` R package.

Principal Component Analysis (PCA) is an unsupervised learning technique for dimensionality reduction. It is used to explain the variance–covariance structure of a set of variables through linear combinations of the variables. Principal components (PCs) are variables constructed as linear combinations of the initial variables. The PCs are uncorrelated and the greatest variation in the data is captured within the first PCs. The PCs represent the directions of the data that explain a maximal amount of variance. Though 10-dimensional data gives you 10 PCs, PCA put maximum possible information in the first component, followed by the second component, and so forth, under the constraint that each component is uncorrelated with the previous component. PCA can be performed through singular-value decomposition (SVD). [AZ: to-expand]. In OPG, PCA is performed using the `irlba` R package which


Statistical testing
---------------------------

Multi-method statistical testing. For gene-level testing, statistical
significance was assessed using three independent statistical methods:
DESeq2 (Wald test), edgeR (QLF test) and limma-trend (Love 2014;
Robinson 2010; Ritchie 2015). The maximum q-value of the three methods
was taken as aggregate q-value, which corresponds to taking the
intersection of significant genes from all three tests.


Statistical testing of differential enrichment of genesets was
performed using an aggregation of multiple statistical methods:
Fisher's exact test, fGSEA (Korotkevich 2019), Camera (Wu 2012) and
GSVA/limma (Hanzelmann 2013, Ritchie 2015). The maximum q-value of the
selected methods was taken as aggregate meta.q value, which
corresponds to taking the intersection of significant genes from all
tests. As each method uses different estimation parameters (NES for
GSEA, odd-ratio for fisher, etc.) for the effect size, for
consistency, we took the average log fold-change of the genes in the
geneset as sentinel value. We used more than 50000 genesets from
various public databases including: MSigDB (Subramanian 2005; Liberzon
2015), Gene Ontology (Ashburner 2000), and Kyoto Encyclopedia of Genes
and Genomes (KEGG) (Kanehisa 2000).


Functional analysis
---------------------------

Graph-weighted GO analysis. The enrichment score of a GO term was
defined as the sum of q-weighted average fold-changes, (1-q)*logFC, of
the GO term and all its higher order terms along the shortest path to
the root in the GO graph. The fold-change of a gene set was defined as
the average of the fold-change values of its member genes. This
graph-weighted enrichment score thus reflects the enrichment of a GO
term with evidence that is corroborated by its parents in the GO graph
and therefore provides a more robust estimate of enrichment. The
activation map visualizes the scores of the top-ranked GO terms for
multiple contrasts as a heatmap.

KEGG pathway visualization was performed using the Pathview
R/Bioconductor package using the foldchange as node color.

Cell type profiling
--------------------

Cell type profiling was performed using the LM22 signature matrix as
reference data set (Chen 2018). We have evaluated a total of 6 computational deconvolution
methods: DeconRNAseq (Gong 2013), DCQ (Altboum 2014), I-NNLS (Abbas
2009), NNLM (Lin 2020), rank-correlation and a meta-method. For NNLM,
we repeated NNLM for non-logarithmic (NNLM.lin) and ranked signals
(NNLM.rnk). The latter meta-methods, meta and meta.prod, summarize the
predictions of all the other methods as the mean and/or geometric mean
of the normalized prediction probabilities, respectively.

[1] Gong T, Szustakowski JD. DeconRNASeq: a statistical framework for
deconvolution of heterogeneous tissue samples based on mRNA-Seq
data. Bioinformatics. 2013. 

[2] Altboum Z, et al. Digital cell quantification identifies global immune
cell dynamics during influenza infection. Mol Syst Biol. 2014 Feb
28;10(2):720. 

[3] Abbas A, et al. Deconvolution of Blood Microarray Data Identifies
Cellular Activation Patterns in Systemic Lupus Erythematosus, PLOS
One, 2009. 

[4] Lin X, Boutros PC. Optimization and expansion of non-negative matrix
factorization. BMC Bioinformatics. 2020.

[5] Chen B, et al. Profiling Tumor Infiltrating Immune Cells with
CIBERSORT. Methods Mol Biol. 2018.


Scripting and visualization
---------------------------

Data preprocessing was performed using bespoke scripts using R (R Core
Team 2013) and packages from Bioconductor (Huber 2015). Statistical
computation and visualization have been performed using the Omics
Playground version vX.X.X (Akhmedov 2020).



REFERENCES 
---------------------------

Akhmedov M, Martinelli A, Geiger R and Kwee I. Omics Playground: A
comprehensive self-service platform forvisualization, analytics and
exploration of Big Omics Data. NAR Genomics and Bioinformatics, Volume
2, Issue 1, March 2020,

Ashburner et al. Gene ontology: tool for the unification of
biology. Nat Genet. May 2000;25(1):25-9.


Huber W, et al. (2015) Orchestrating high-throughput genomic analysis
with Bioconductor. Nature Methods 12:115-121; doi:10.1038/nmeth.3252

Kanehisa, M. and Goto, S.; KEGG: Kyoto Encyclopedia of Genes and
Genomes. Nucleic Acids Res. 28, 27-30 (2000).

Leek J., Storey J. Capturing heterogeneity in gene expression studies
by ‘surrogate variable analysis’ PLoS Genet. 2007

Love MI, Huber W, Anders S (2014). “Moderated estimation of fold
change and dispersion for RNA-seq data with DESeq2.” Genome Biology,
15, 550.

R Core Team (2013). R: A language and environment for statistical
computing. R Foundation for Statistical Computing, Vienna, Austria.
URL http://www.R-project.org/.

Ritchie ME, Phipson B, Wu D, Hu Y, Law CW, Shi W, Smyth GK
(2015). “limma powers differential expression analyses for
RNA-sequencing and microarray studies.” Nucleic Acids Research, 43(7)


Robinson MD, McCarthy DJ, Smyth GK (2010). “edgeR: a Bioconductor
package for differential expression analysis of digital gene
expression data.” Bioinformatics, 26(1), 139-140.
