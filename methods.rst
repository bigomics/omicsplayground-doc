.. _Methods:


Methods
================================================================================


Here, we provide descriptions of the bioinformatic techniques and methods used in Omics Playground. You may want to use these information to describe the methods when using the Omics Playground. You can always access the R code (on github) to check exactly all steps implemented, or you can contact the bioinformatic staff at BigOmics Analytics should you have questions. 

Correlation analyses 
---------------------
**Correlation** is a statistical technique used to measure the strength and direction of the relationship between two variables.  It determines whether a relationship exists between two variables and its strength. The most used correlation types are Pearson's correlation (for linear relationships between normally distributed variables), Spearman's rank correlation (for ordinal or non-normal data), and Kendall's tau correlation (for ranked pairings). The correlation coefficient ranges from -1 to 1. -1 is a perfect negative correlation, and 1 is a perfect positive correlation.
A value of 0 means no correlation. Correlation does not imply causation. It only measures the degree of association between two variables. Pearson & Sperman correlations are by far the most used in biological research. A distict assessment concerns partial correlation, as discussed below.

**Pearson and Spearman correlation**: the Pearson correlation coefficient is a statistical measure that evaluates the strength and direction of the linear relationship between two continuous variables. Ideally, Pearson correlation should be used when the following assumptions are met: (i) the variables have a linear relationship each other; (ii) both variables are continuous and quantitative; (iii) the variables are normally distributed; (iv): no significant outliers populate the data. Typically, if any of these assumptions are unmet, Spearman correlation should be employed.

**Partial correlation**:  partial correlation measures the degree of association between two variables, while controlling for the effect of one or more additional factors/variables. It may determine if the relationship between two variables (e.g. X and Y) remains significant after accounting for the influence of a third ("controlling") variable (Z) on both X and Y. In other words, it estimates the correlation between X and Y after removing the variance that each shares with Z. In principle, partial correlation may reveal cases where an observed correlation between X and Y is due to their mutual association with a third variable Z, rather than a direct relationship between X and Y. The values of the partial correlation coefficient ranges from -1 to 1, similar to the regular correlation coefficient.

Batch correction
-----------------
Measurements in datasets generated in multiple centers are typically affected by multiple sources of technical variation, collectively known as ‘Batch Effects’ (BEs). BEs may also arise within a single laboratory, due to distinct sequencing runs, depths, use of different sample donors, or when processing occurs in separate days. BEs are predominant, unwanted source of noise that impact mean and variance and may confound real biological signal, altering false positive and false negative rates. BE correction methods can be categorized into supervised, such as ComBat and Limma RemoveBatchEffects, and unsupervised methods such as SVA and RUV. Supervised methods use linear models to adjust known batch effects, while unsupervised methods measure potential sources of variation without requiring prior knowledge of the batch vector.

**ComBat**: ComBat employs empirical Bayesian method to adjust the data for the known batch vector. It assumes that BEs have similar impact on many genes. Information across features is gathered within each batch to estimate batch-specific mean and variance. These BEs parameters are then shrunk toward the global BEs average and used to adjust for the BEs on each gene. The output is a batch-corrected data matrix that can be used for downstream analyses.

**Limma RemoveBatchEffects**: RemoveBatchEffects employs linear modeling to adjust BEs and additional covariates if specified. In most  cases it is employed to adjust BEs only. Multiple numeric covariates, if specified, are assumed to have additive effects. The output is a batch-corrected data matrix that can be used for downstream analyses.

**Surrogate Variable Analysis (SVA)**: SVA aims to define surrogate variables (SVs) that consistently capture latent sources of variation in the data. It employs singular value decomposition (SVD) on the batch uncorrected data, without the need for prior information on latent variables affecting the data. To preserve the biological effects of interest, the SVs need to capture variation uncorrelated with the primary variable of interest. The SVs are then regressed out from the gene expression data to generate a batch-corrected data matrix suitable for downstream analyses.

**Remove Unwanted Variation (RUV)**: RUV estimates and removes known and unknown unwanted variation based on negative control variables and technical sample replicates that capture batch variation. It assumes the existence of negative control variables whose expression levels is robust to changes in the biological factors of interest. Factor analysis (e.g., SVD) on these controls is then used to estimate the factors representing unwanted variation, such as BEs. The expression of all features is then adjusted for the unwanted variation to get a batch-corrected dataset. 

**Nearest-Pair Matching (NPmatch)** (Zito et al., BioRxiv 2024): current methods for BE correction mostly rely on specific assumptions or complex models, and may not detect and adjust BEs adequately, impacting downstream analysis and discovery power. To address these challenges we (BigOmics Analytics) developed NPmatch (https://www.biorxiv.org/content/10.1101/2024.04.29.591524v1). NPmatch is a nearest-neighbor matching-based method that adjusts BEs satisfactorily and outperforms current methods in a wide range of datasets. Our method was inspired by principles of the statistical matching theory. It relies on distance-based matching to deterministically search for nearest neighbors with opposite labels, so-called “nearest-pair”, among samples. NPmatch requires knowledge of the phenotypes but not of the batch assignment. Differently to many other algorithms, NPmatch does not rely on specific models or underlying distribution. It does not require special experimental designs, randomized controlled experiments, control genes or batch information. NPmatch is based on the simple rationale that samples should empirically pair based on distance in biological profiles, such as transcriptomics profiles. The NPmatch algorithm initially selects the top variable features (genes). The features are feature-centered and then further centered per condition group. Inter-sample similarities are then determined by either computing the Pearson correlation matrix Dn x n (default) or Euclidean distance. The Pearson correlation matrix Dn x n is subsequently decomposed into the c phenotypic/condition groups. For each sample, a k nearest-neighbor like search is conducted to identify the closest k-nearest samples across each c phenotypic/condition group. The process results into a matrix Xn x (k x c) where for each sample, k-nearest samples are identified per each c condition. The Xn x (k x c) matrix is then used to derive a (i) vector of length L=n x k x c, storing all the computed pairs; (ii) a fully paired dataset Xp x L. As pairing may per-se imply duplication of correlated signals (which is a BE-like effect), Limma ‘RemoveBatchEffect’ is used to correct for the ‘pairing effects’ through linear regression. The batch-corrected X1 p x L matrix is finally condensed into its original p x n size by computing, per each feature, the average values across duplicated samples. Thus, the X1p x n matrix represents the batch-corrected dataset which can be used for further downstream analyses.

In OPG, batch effects, or contamination by unwanted variables, was identified by an F-test for the first three principal components. Continuous
variables were dichotomized into high/low before testing. Highly confounding variables would appear as having high relative contribution in the first or second principal component, often higher than the variable of interest. Batch effects were also visually assessed (before and after correction) using annotated heatmaps and t-SNE plots colored by variables.

Batch correction was performed for explicit batch variables or unwanted covariates. Parameters with a correlation r>0.3 with any of variables of interest (i.e. the model parameters) were omitted from the regression. Correction was performed by regressing out the covariate using the 'removeBatchEffect' function in the limma R/Bioconductor package.

Technical correction was performed for intrinsic technical parameters such as library size (i.e. total counts), mitochondrial and ribosomal proportions, cell cycle and gender. These parameters were estimated from the data. The cell cycle was estimated using the Seurat R/Bioconductor package. Gender (if not given) was estimated by checking the absence/presence of expression of gender specific genes on the X/Y chromosome. Parameters with a correlation r>0.3 with any of the model parameters were omitted from the regression. Correction was performed by regressing out the covariate using the 'removeBatchEffect' function in the limma R/Bioconductor package.

Unsupervised batch correction was performed using SVA by estimating the latent surrogate variables and regressing out using the 'removeBatchEffect' function in the limma R/Bioconductor package.


Clustering
---------------------------

Heatmaps were generated using the ComplexHeatmap R/Bioconductor
package (Gu 2016) on scaled log-expression values (z-score) using
euclidean distance and Ward linkage. The standard deviation was used
to rank the genes for the reduced heatmaps.

**t-distributed stochastic neighbor embedding (t-SNE)**: t-SNE is a non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Unlike linear dimensionality reduction techniques like PCA, t-SNE may separate data that is not linearly separable. Furthermore, while PCA tends to preserve the global information in the data, t-SNE tends to preserve relative distances. t-SNE first calculates the distance between every pair of data points. Each data point is then placed within a Gaussian distribution while all other data points are distributed according to their distance. Points closer each other are more similar. Point more distanced are more diverse each other. A value, called 'Perplexity', is calculated to reflect the standard deviation of the data. The Perplexity value is the number of nearest neighbors considered in generating the probability of points being close each other. Smaller perplexity values may result in very localized outputs ignoring global information, while larger values may obscure smaller structures. For this reason, the Perplexity value is intended to be less than the size of data. Recommended values are in the range 5-50. To determine the representation of the data in the low dimensional space, a t-distribution is used with one degree of freedom. A gradient descent optimization involving an iterative process, is finally employed to determine the final low-dimensional data representation that reflects the high-dimension accurately. In OPG t-SNE is computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the t-SNE embedding. The perplexity heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation was performed using the `Rtsne` R package.

**Uniform Manifold Approximation and Projection (UMAP)**: UMAP is another non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Similarly to t-SNE, UMAP can effectively separate data that is not linearly separable. When compared to t-SNE, UMAP tends to more clearly separate groups of similar categories from each other. Generally, UMAP can also preserve the global structure more than t-SNE. UMAP computation is also generally faster than t-SNE. To construct the initial high-dimensional graph, UMAP builds a weighted graph with edge weights representing the likelihood that two points are connected. Connectedness is inferred through radii outwards from each point. Smaller radii result to small, isolated clusters. Larger radii result to overconnection. To reduce these potential issues, each radius is chosen locally, based on the between each point and its nearest neighbor. UMAP then makes the graph "fuzzy" by decreasing the likelihood of connection as the radius grows. UMAP then projects the data into lower dimensions through a force-directed graph layout algorithm in a similar way than t-SNE. By ensuring that each point is connected to at least its closest neighbor, UMAP enables preservation of the local structure with respect to the global structure. In the OPG, UMAP was computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the UMAP embedding. The number of neighbours was heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation w as performed using the `uwot` R package.

**Principal Component Analysis (PCA)**: PCA is an unsupervised learning technique for dimensionality reduction. It is used to explain the variance–covariance structure of a set of variables through linear combinations of the variables. Principal components (PCs) are variables constructed as linear combinations of the initial variables. The PCs are uncorrelated and the greatest variation in the data is captured within the first PCs. The PCs represent the directions of the data that explain a maximal amount of variance. Though 10-dimensional data gives you 10 PCs, PCA put maximum possible information in the first component, followed by the second component, and so forth, under the constraint that each component is uncorrelated with the previous component. PCA can be performed through singular-value decomposition (SVD). [AZ: to-expand]. In OPG, PCA is performed using the `irlba` R package.


Biomarker analysis
---------------------------
The Food and Drug Administration (FDA) defines a biomarker as ‘a defined characteristic that is measured as an indicator of normal biological processes, pathogenic processes, or responses to an exposure or intervention, including therapeutic interventions. A biomarker could be almost any objective and quantifiable functional, physiological, biochemical, or molecular measurement. Examples of molecular biomarkers include the presence of proteins in the blood, such as prostate-specific antigen (PSA) used in the diagnosis of prostate cancer, or the presence of mutations in tumor suppressor genes, like those in BRCA1 or BRCA2, predictive of breast cancer risk. Therefore, novel biomarker discovery is crucial to many areas, including clinical diagnostics and drug development.Bioinformatics has revolutionized biomarker discovery by integrating computational tools with high-throughput data analysis from genomics, proteomics, transcriptomics, and metabolomics. Researchers can now efficiently identify and analyze potential biomarkers, leading to cost-effective and accelerated research outcomes. On the Omics Playground, we have made available to all users state-of-the-art machine learning (ML) methods.

**Sparse Partial Least Squares (sPLS)**: sPLS is a ML technique that  extends  partial least square (PLS) regression. It is designed to analyze relationships between two datasets where it can handle multivariate high-dimensional data where the number of variables exceeds the number of observations -a common scenario in biological research- while employing dimensional reduction and variable selection. sPLS aims to identify patterns and relationships between continuous data within complex datasets by reducing the dimensionality of the data while maintaining its predictive power. This method combines the strengths of Partial Least Squares (PLS) regression with sparsity-inducing penalties. It seeks for linear combination between variables and, compared to PLS, it allows multiple response variable selection on both datasets. This is achieved through the use of LASSO penalization. Compared to CCA (Canonical Correlation Analysis), PLS relies on covariance rather than correlation coefficient. By incorporating sparsity constraints, sPLS can effectively identify a subset of variables that are most relevant for predicting the outcome of interest. sPLS is widely used in bioinformatic applications for biomarker discovery in biomedical research.

**Glmnet**:  The glmnet package in R provides extensive functionalities to identify putative biomarkers and construct predictive models for distinct biological outcome variables, such as prognosis, risk to disease, response to treatment. It supports binary (through logistic regression), continuous (through linear regression), as well as survival (through Cox-regression) variables. Glmnet offers procedures for fitting LASSO and/or elastic-net regularization in linear, logistic, and multinominal regression. Typically, and similarly to other ML techniques, Glmnet requires a response variable, a predictor variables and a regularization type with regularization strength. It employs L1 and L2 regularizations, which are LASSO and ridge penalties, respectively. While the ridge penalty shrinks the coefficients of correlated predictors towards each other, the lasso penalty picks one and discard the others. The elastic net penalty is a combination of LASSO and ridge penalty. Generally, these regularizations help preventing overfitting by adding a penalty term to the objective function. Importantly, Glmnet also provides approaches to perform cross-validation (CV) analyses. CV enables assessment of models performance and generability of the predicted features. Glmnet is also computational-efficient for large dataset. In summary, Glmnet provides tools for the implementation of regularized regression models, enabling building predictive models.




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

**Fisher`s exact test**: Fisher's exact test is a statistical significance test used to determine if there is a non-random association between two categorical variables organized within a contingency table. It calculates the (exact) probability of obtaining the observed data as well as other more extreme patterns under the null hypothesis (Ho) of no association between the variables. The test initially calculates the probability of obtaining the observed contingency table under the Ho that the two variables are independent. This probability is calculated using the hypergeometric distribution, which gives the (exact) probability of drawing a specific number of successes in a sample without replacement. Next, the test calculates the probabilities of all other possible relationships. If the p-value for these other possible relationships is less than or equal to the pre-defined significance level (e.g., 0.05), the Ho is rejected. When Ho is rejected, a statistically significant association between the two variables is supported. The key advantages of Fisher's exact test are:

1. It is exact and does not rely on approximations, making it suitable for small sample sizes or sparse data where assumptions of other statistical tests may remain unmet.
2. It is valid for all sample sizes.
3. It assumes fixed marginal totals (row and column sums), which is appropriate for many experimental designs.
However, the test has limitations such as being computationally intensive for larger tables, and not providing an estimate of the strength or direction of association.


Functional analyses
---------------------------
Here below the describe the Gene Set Enrichment methods in OPG:

**CAMERA (Correlation Adjusted MEan RAnk gene set test)** (Wu et al., Nucleic Acids Research, 2012):  most competitive gene set tests assume that genes are independent units and rely on gene permutation of gene labels. However inter-gene correlation exist and may inflate discovery of false positives. CAMERA was develop to address the problem of correlated genes in the test set.  It is centered on the idea of using the variance inflaction factor of inter-gene correlation structure to adjust the parametric or rank-based gene set test statistics. This procedure has been shown detect differential gene representations while controlling the FDR even in datasets with a small number of biological replicates, regardless of inter-gene correlations.

**GSEA (Gene Set Enrichment Analysis)** (Mootha et al., 2003, Nat Gen): GSEA is a computational method to determine whether a prior defined set of genes show statistically significant, concordant differences between two biological states/phenotypes. GSEA calculates an enrichment score (ES), representing the degree to which a gene set is overrepresented at the extreme top or bottom or a ranked gene list. The ranked gene list typically contains genes from differential gene expression analyses between two phenotypes. The ES is calculated by Kolmogorov-Smirnov statistics: it increases the cumulative statistics when a gene is present in a gene set or decreases when the gene is not found in the gene set.  This generates a weighted ES that accounts for the position of the gene in the list. The ES' statistical significance is estimated by phenotype-based permutation that preserves the correlation structure of the gene expression data. Ultimately, the ES and its statistical significance allows to identify gene sets enriched among the most upregulated or downregulated genes between two states/phenotypes. Therefore, GSEA enables to study concordant and modest changes that may be missed in analyses at single-gene level.

**ssGSEA (single-sample GSEA)** (Barbie et al., 2009, Nature): ssGSEA calculates separate ESs for each pairing of a sample and gene set. Each ssGSEA ES represents the degree to which the genes in a particular gene set are coordinately up- or down-regulated within a sample. In other words, the ssGSEA ES reflects the degree of overexpression of a given gene set in an individual sample. Compared to standard GSEA, ssGSEA provides a score for each sample rather than across samples. Highly expressed genes contribute positively to the score, while lowly expressed genes contribute negatively.

**fGSEA (Fast Gene Set Enrichment Analysis)** (Korotkevitch et al., bioRxiv, 2021): Standard implementation of GSEA may have problems in accurately estimating low permutation P-values. Furthermore, time and memory requirement grow linearly with size of datasets and number of gene set collections. fGSEA aims to address these problems, thus expanding the applicability of GSEA. fGSEA provides higher estimation accuracy for low GSEA P-values at a substantially improved running time. The algorithms consist of (i) fGSEA-simple which estimates enrichment P-values with limited accuracy for the whole collection of gene sets being tested, and (ii) fGSEA multi-level which infers low P-value with higher accuracy for each individual gene set.

**GSVA (Gene Set Variation Analysis)** (Hanzelmann et al., BMC Bioinformatics 2013): existing methods for gene sets enrichment testing aim at identifying gene sets from large collection of gene signatures and/or select few enriched gene groups most relevant to the phenotype being investigated. Generally, existing methods may not account for the inherent variation in the gene expression data and associated pathways activity potentially impacted in highly heterogeneous data. Furthermore, conventional, competitive gene set enrichment methods have mostly been designed to handle two-groups comparisons (e.g., case-control studies). Therefore, they may not find direct applicability in population-level data where multiple, hierarchical phenotypes are simultaneously compared. GSVA is non-parametric and unsupervised approach that aims to address these challenges. It computes gene set enrichment score for each sample and then conducts an analysis of variation of the gene set enrichment and pathways activity across samples, independently of class labels. In this way GSVA facilitates post-hoc analyses of pathways including differential pathway activity analysis.

**fry**: Fry is a fast approximation method for gene set enrichment analysis based on the Rotation Gene Set Tests (ROAST) algorithm for linear models in the limma R package. Fry simulates the p-value obtained in case a large number of rotations with ROAST. To protect against potential false positives driven by correlated genes, a residual space rotation is used. Differently to a standard permutation test, this approach may work in experiment with small sample sizes. ROAST can be computationally intensive if applied to large collections of gene sets. Fry is faster by approximating p-values associated with an infinite number of tests. While both ROAST and Fry account for gene-gene correlation structures, for large gene collections Fry is much faster than ROAST in distinguishing the most significant gene sets.

Graph-weighted GO analysis. The enrichment score of a GO term was defined as the sum of q-weighted average fold-changes, (1-q)*logFC, of the GO term and all its higher order terms along the shortest path to the root in the GO graph. The fold-change of a gene set was defined as the average of the fold-change values of its member genes. This graph-weighted enrichment score thus reflects the enrichment of a GO term with evidence that is corroborated by its parents in the GO graph and therefore provides a more robust estimate of enrichment. The activation map visualizes the scores of the top-ranked GO terms for multiple contrasts as a heatmap.

KEGG pathway visualization was performed using the Pathview R/Bioconductor package using the foldchange as node color.

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
