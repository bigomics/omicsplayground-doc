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

Identification of outlier samples
---------------------------------
Sample outliers in genomic data are generally characterized by data points that deviate significantly from the expected pattern or distribution of most of data points in the dataset. Outlier samples carry unusually low or high values compared to the majority of samples in the dataset. This results into markedly different distribution compared to other samples. Outliers could arise from experimental, technical errors in data collection as well as early data processing steps. They can hinder data analysis in several ways. For instance, they can skew statistical testing such that certain genes may appear falsely significant in differential expression studies, potentially leading to erroneous biological conclusions. Therefore, identifying outliers is an important step for maintaining data quality and ensuring comparability between samples for accurate analysis results. At Step 4 (QC/BC) of the data uploading process, the OmicsPlayground has a module fully dedicated to sample outliers -"Outliers Detection Module". We detect outlier samples based on 3 combined z-scores: (1) median-based z-score of pairwise sample correlaton; (2) median-based z-score of Euclidean distance; (3) median-based z-score of gene expression. These three measures are combined by average. A median-based z-score is based on median and median absolute deviation. It is more robust compared to standard Z-score, which instead uses mean and standard deviation. It is useful for identifying outliers in datasets that may not follow a normal distribution. Please see the corresponding R function detectOutlierSamples(), which is part of our playbase R package. The source code is accessible at https://github.com/bigomics/playbase/blob/main/R/pgx-outlier.R

Batch correction
-----------------
Measurements in datasets generated in multiple centers are typically affected by multiple sources of technical variation, collectively known as ‘Batch Effects’ (BEs). BEs may also arise within a single laboratory, due to distinct sequencing runs, depths, use of different sample donors, or when processing occurs in separate days. BEs are predominant, unwanted source of noise that impact mean and variance and may confound real biological signal, altering false positive and false negative rates. BE correction methods can be categorized into supervised, such as ComBat and Limma RemoveBatchEffects, and unsupervised methods such as SVA and RUV. Supervised methods use linear models to adjust known batch effects, while unsupervised methods measure potential sources of variation without requiring prior knowledge of the batch vector.

**ComBat**: ComBat employs empirical Bayesian method to adjust the data for the known batch vector. It assumes that BEs have similar impact on many genes. Information across features is gathered within each batch to estimate batch-specific mean and variance. These BEs parameters are then shrunk toward the global BEs average and used to adjust for the BEs on each gene. The output is a batch-corrected data matrix that can be used for downstream analyses.

**Limma RemoveBatchEffects**: RemoveBatchEffects employs linear modeling to adjust BEs and additional covariates if specified. In most  cases it is employed to adjust BEs only. Multiple numeric covariates, if specified, are assumed to have additive effects. The output is a batch-corrected data matrix that can be used for downstream analyses.

**Surrogate Variable Analysis (SVA)**: SVA aims to define surrogate variables (SVs) that consistently capture latent sources of variation in the data. It employs singular value decomposition (SVD) on the batch uncorrected data, without the need for prior information on latent variables affecting the data. To preserve the biological effects of interest, the SVs need to capture variation uncorrelated with the primary variable of interest. The SVs are then regressed out from the gene expression data to generate a batch-corrected data matrix suitable for downstream analyses.

**Remove Unwanted Variation (RUV)**: RUV estimates and removes known and unknown unwanted variation based on negative control variables and technical sample replicates that capture batch variation. It assumes the existence of negative control variables whose expression levels is robust to changes in the biological factors of interest. Factor analysis (e.g., SVD) on these controls is then used to estimate the factors representing unwanted variation, such as BEs. The expression of all features is then adjusted for the unwanted variation to get a batch-corrected dataset. 

**Nearest-Pair Matching (NPmatch)**: current methods for BE correction mostly rely on specific assumptions or complex models, and may not detect and adjust BEs adequately, impacting downstream analysis and discovery power. To address these challenges we (BigOmics Analytics) developed NPmatch `(Zito et al., Bioinformatics, 2025) <https://academic.oup.com/bioinformatics/article/41/3/btaf084/8042340>`_. NPmatch is a nearest-neighbor matching-based method that adjusts BEs satisfactorily and outperforms current methods in a wide range of datasets. Our method was inspired by principles of the statistical matching theory. It relies on distance-based matching to deterministically search for nearest neighbors with opposite labels, so-called “nearest-pair”, among samples. NPmatch requires knowledge of the phenotypes but not of the batch assignment. Differently to many other algorithms, NPmatch does not rely on specific models or underlying distribution. It does not require special experimental designs, randomized controlled experiments, control genes or batch information. NPmatch is based on the simple rationale that samples should empirically pair based on distance in biological profiles, such as transcriptomics profiles. The NPmatch algorithm initially selects the top variable features (genes). The features are feature-centered and then further centered per condition group. Inter-sample similarities are then determined by either computing the Pearson correlation matrix Dn x n (default) or Euclidean distance. The Pearson correlation matrix Dn x n is subsequently decomposed into the c phenotypic/condition groups. For each sample, a k nearest-neighbor like search is conducted to identify the closest k-nearest samples across each c phenotypic/condition group. The process results into a matrix Xn x (k x c) where for each sample, k-nearest samples are identified per each c condition. The Xn x (k x c) matrix is then used to derive a (i) vector of length L=n x k x c, storing all the computed pairs; (ii) a fully paired dataset Xp x L. As pairing may per-se imply duplication of correlated signals (which is a BE-like effect), Limma ‘RemoveBatchEffect’ is used to correct for the ‘pairing effects’ through linear regression. The batch-corrected X1 p x L matrix is finally condensed into its original p x n size by computing, per each feature, the average values across duplicated samples. Thus, the X1p x n matrix represents the batch-corrected dataset which can be used for further downstream analyses.

In OPG, batch effects, or contamination by unwanted variables, was identified by an F-test for the first three principal components. Continuous
variables were dichotomized into high/low before testing. Highly confounding variables would appear as having high relative contribution in the first or second principal component, often higher than the variable of interest. Batch effects were also visually assessed (before and after correction) using annotated heatmaps and t-SNE plots colored by variables.

Batch correction was performed for explicit batch variables or unwanted covariates. Parameters with a correlation r>0.3 with any of variables of interest (i.e. the model parameters) were omitted from the regression. Correction was performed by regressing out the covariate using the 'removeBatchEffect' function in the limma R/Bioconductor package.

Technical correction was performed for intrinsic technical parameters such as library size (i.e. total counts), mitochondrial and ribosomal proportions, cell cycle and gender. These parameters were estimated from the data. Cell cycle (CC) was estimated using the Seurat R/Bioconductor package using reference lists of genes that are known to be markers for S or G2M phase. You can read about it more `here <https://satijalab.org/seurat/archive/v3.1/cell_cycle_vignette.html>`_. In single-cell analysis, people sometimes regress out the CC effect. In bulk RNAseq it may give you some more information about your samples, 

Gender (if not given) was estimated by checking the absence/presence of expression of gender specific genes on the X/Y chromosome. Parameters with a correlation r>0.3 with any of the model parameters were omitted from the regression. Correction was performed by regressing out the covariate using the 'removeBatchEffect' function in the limma R/Bioconductor package.

Unsupervised batch correction was performed using SVA by estimating the latent surrogate variables and regressing out using the 'removeBatchEffect' function in the limma R/Bioconductor package.

Normalization 
---------------------
**Counts per million (CPM)**: CPM mapped reads are the number of raw reads mapped to a transcript, scaled by the number of sequencing reads in your sample, multiplied by a million. We employ a log2CPM: specifically, The data are then added a pseudocount of 1 to enable log2-transformation and avoid negative values, and also make data distribution closer to normal. Thus, log2CPM is a within sample normalization approach. It normalizes RNA-seq data for sequencing depth and so it also facilitates comparisons betweeen samples. However, a stronger cross-sample normalization method is often needed. That why in the OPG we have implemented log2CPM + Quantile normalization.

**Quantile normalization**: The quantile method aims to make the distribution of gene expression levels the same for each sample in a dataset (Bolstad et al., 2003). It assumes that the global differences in distributions between samples are all due to technical variation. Any remaining differences are likely actual biological effects. In quantile normalization, the genes are first ranked within each sample. An average value is calculated across all samples for genes of the same rank. This average value then replaces the original value of all genes in that rank. The genes are then placed in their original order. Therefore, quantile normalization makes the distribution of gene expression levels the same for each sample in a dataset, a pattern typically observed in boxplots. This makes quantile normalization a highly robust way to achieve cross-sample normalization.

**Max median normalization (MaxMedian)**: MaxMedian normalization is more often adopted in proteomics data. It aims to normalize the samples by the maximum median value. Specifically, it first calculates the median value in each sample. The maximum median value is identified. Each data point in each sample is then divided by the sample's median value and multiplied by the maximum median value. In OPG, we then perform log2 transformation.

**Max sum normalization (MaxSum)**: MaxSum normalization is also more often adopted in proteomics data. It aims to normalize the samples by the maximum value of total intensity. Specifically, it first calculates the total intensity in each sample. The maximum total intensity value is identified. Each data point in each sample is then divided by the sample's total intensity and multiplied by the maximum total intensity value. In OPG, we then perform log2 transformation.

**Reference normalization (reference)**: This type of normalization aims to normalize the data by a user-selected feature. Simply, it divides each data point in each sample by the value of the reference features in that sample. In OPG, we then perform log2 transformation.

Clustering
---------------------------
Heatmaps were generated using the ComplexHeatmap R/Bioconductor
package (Gu 2016) on scaled log-expression values (z-score) using
euclidean distance and Ward linkage. The standard deviation was used
to rank the genes for the reduced heatmaps.

**t-distributed stochastic neighbor embedding (t-SNE)**: t-SNE is a non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Unlike linear dimensionality reduction techniques like PCA, t-SNE may separate data that is not linearly separable. Furthermore, while PCA tends to preserve the global information in the data, t-SNE tends to preserve relative distances. t-SNE first calculates the distance between every pair of data points. Each data point is then placed within a Gaussian distribution while all other data points are distributed according to their distance. Points closer each other are more similar. Point more distanced are more diverse each other. A value, called 'Perplexity', is calculated to reflect the standard deviation of the data. The Perplexity value is the number of nearest neighbors considered in generating the probability of points being close each other. Smaller perplexity values may result in very localized outputs ignoring global information, while larger values may obscure smaller structures. For this reason, the Perplexity value is intended to be less than the size of data. Recommended values are in the range 5-50. To determine the representation of the data in the low dimensional space, a t-distribution is used with one degree of freedom. A gradient descent optimization involving an iterative process, is finally employed to determine the final low-dimensional data representation that reflects the high-dimension accurately. In OPG t-SNE is computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the t-SNE embedding. The perplexity heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation was performed using the `Rtsne` R package.

**Uniform Manifold Approximation and Projection (UMAP)**: UMAP is another non-linear dimensionality reduction method that enables visualization of high-dimensional data in a low-dimensional space, typically 2D or 3D. Similarly to t-SNE, UMAP can effectively separate data that is not linearly separable. When compared to t-SNE, UMAP tends to more clearly separate groups of similar categories from each other. Generally, UMAP can also preserve the global structure more than t-SNE. UMAP computation is also generally faster than t-SNE. To construct the initial high-dimensional graph, UMAP builds a weighted graph with edge weights representing the likelihood that two points are connected. Connectedness is inferred through radii outwards from each point. Smaller radii result to small, isolated clusters. Larger radii result to overconnection. To reduce these potential issues, each radius is chosen locally, based on the between each point and its nearest neighbor. UMAP then makes the graph "fuzzy" by decreasing the likelihood of connection as the radius grows. UMAP then projects the data into lower dimensions through a force-directed graph layout algorithm in a similar way than t-SNE. By ensuring that each point is connected to at least its closest neighbor, UMAP enables preservation of the local structure with respect to the global structure. In the OPG, UMAP was computed using the top 1000 most varying genes, then reduced to 50 PCA dimensions before computing the UMAP embedding. The number of neighbours was heuristically set to 25% of the sample size or 30 at maximum, and 2 at minimum. Calculation w as performed using the `uwot` R package.

**Principal Component Analysis (PCA)**: PCA is an unsupervised learning technique for dimensionality reduction. It is used to explain the variance–covariance structure of a set of variables through linear combinations of the variables. Principal components (PCs) are variables constructed as linear combinations of the initial variables. The PCs are uncorrelated and the greatest variation in the data is captured within the first PCs. The PCs represent the directions of the data that explain a maximal amount of variance. Though 10-dimensional data gives you 10 PCs, PCA put maximum possible information in the first component, followed by the second component, and so forth, under the constraint that each component is uncorrelated with the previous component. PCA can be performed through singular-value decomposition (SVD). [AZ: to-expand]. In OPG, PCA is performed using the `irlba` R package.


Differential gene expression testing
--------------------------------------------
Omics Playground is equipped with 9 distinct differential gene expression (DGE) testing methods, aiming to cover the most disparate experimental conditions. It‘s our priority to offer researchers of any background a vast range of choice to study in detail their data, in the fastest possible time, and without requiring any coding. Researchers may evaluate different methods to select the appropriate one based on their needs. Our DGE workflow is paralleled with extensive visualizations including volcano plots, box plots, bar plots, heatmaps, and functional enrichment testing of biological pathways. Here below we provide a description of the DGE algorithms available in the OPG:

**Student's t-test / Welch's t-test**: The t-test is the simplest statistics that can be used to compare two groups based on their average gene expression levels. While Student's t-test assumes that the two populations have equal variances, Welch's t-test does not rely on this assumption. When the assumption of the Student's t-test is known to be violated, the Welch's t-test should be employed as it performs better. 

**DESeq2 Likelihood / Wald test**: DESeq2 employs negative binomial generalized linear models to assess variability in gene expression profiles. Significant DGE changes between groups can be assessed using two methods: the Wald test and the likelihood ratio test (LRT). The Wald test is run by default: a negative binomial test is run for each gene to account for overdispersion in the data. A null hypothesis (Ho) of no DGE between the two sample groups (i.e., fold-change=1) is assumed. Then, a z-score is calculated from each gene's empirical LFC and compared to a standard normal distribution to compute a p-value. If the p-value is less than a pre-chosen alpha level (e.g., 0.05), the Ho is rejected and DGE is reported. In the LRT, DESeq2 fits both a full model and a reduced model for each gene and a Ho of no differences between the full and the reduced model is assumed. Parameters for both models are then estimated and the log-likelihoods of the two models are compared to obtain the likelihood ratio (LR) which would follow a ch-squared distribution. If the p-value is less than a pre-chosen alpha level (e.g., 0.05), the Ho is rejected and DGE is reported. Therefore, the Wald test differs from the LRT in that while the first is based on a single model per gene, the second is based on two models (full and reduced) per each gene.

**EdgeR likelihood ratio / quasi-likelihood F test**: EdgeR employs negative binomial models with estimation of dispersion parameters to model variability on the read counts. It also employs empirical Bayes methods to moderately estimate the gene-specific dispersions. DGE can be assessed in edgeR using and exact test, GLM likelihood ratio (LRT), or the quasi-likelihood F-test. In the exact test, EdgeR uses the negative binomial distribution and is useful for small to moderate sample size datasets. On the other hand, the GLM frameworks are particularly useful for the analysis of complex experimental designs with multiple variables to be accounted for. Compared to the GLM LRT test, the quasi-likelihood F-test may offer a better solution fot example when experiments results into small counts.

**Limma trend / voom**: It employs ordinary linear models with T and F test to measure gene expression differences between groups. These approaches aim to robustly estimate the mean-variance relationship non-parametrically. Using log-counts per million (log-cpm) normalized for sequencig depth, the mean-variance is fitted to the gene-wise standard deviations of the log-cpm as a function of average log-count. To incorporate the mean-variance relationship, limma-trend modifies limma’s empirical Bayes procedure to incorporate a mean-variance trend. A mean-variance trend across all genes aims to model the relationship between a gene's average expression and its variance. Limma-voom incorporates the mean-variance trend of the log-counts into a precision weight for each individual normalized observation. Limma-voom and limma-trend both fit non-parametric curves. They both estimate the relationship between abundance and variance by fitting a lowess/loess curve. Because parameters are estimated from the whole data set (not for individual genes), neither method results to over-fitting. Typically, limma-voom fits a slightly smoother curve than limma-trend. When sequencing depths are similar across samples, limma-trend and limma-voom perform very similarly. Limma-voom performs better than limma-trend when sequencing depths are highly variable across samples.


Timeseries (Longitudinal) data analysis
---------------------------------------
Time-series (longitudinal) data analysis refers to the application of statistical, computational, and machine learning methods to biological data collected at multiple time points. The primary goal is to uncover dynamic patterns, relationships, and mechanisms in biological systems by analyzing how variables-such as gene, protein or metabolite expression levels change over time. For instance, analysis of variation of transcriptomics across times has revealed crucial regulatory mechanisms underlying key biological processes, including cell cycle progression, immune response, disease development, and drug response. Analyzing gene and protein changes across times is uniquely powerful for studying molecular responses to therapeutics. By tracking molecular changes longitudinally, researchers can identify early biomarkers, monitor disease trajectories, and evaluate therapeutic effects. In OPG, the user can add a 'time' variable -in numerical or categorical format- in the metadata file (samples.csv) to trigger the OPG's timeseries-specific functionalities. We use advanced statistical analyses to assess the degree to which time affects biological signals. Specifically, we employ linear modeling in limma, DESeq2 and edgeR to assess the interaction of 'time' with a phenotype. When time is a continuous (numerical) variable, the 'phenotype:time' interaction is tested using a design formula containing natural cubic spline of the 'time' variable (i.e. ~ phenotype * spline(time)). A spline refers to a mathematical function -often a piecewise polynomial such as a cubic spline- used to flexibly model and smooth temporal data. Splines are valuable for representing noisy, irregular, or sparsely sampled gene expression profiles, allowing for the estimation of continuous curves from time-point measures. When time is a categorical variable (e.g., "pre_treatment", "post_treatment"), the 'phenotype:time' interaction is tested using a design formula without spline modeling. For tested features and phenotypes, complete statistical results (Log2 fold-change, p-values, q-values, meta p-values, meta q-values, these latter two corresponding to max p and max q among selected methods) of differential expression testing for the main effect and the interaction with time are reported. In the OPG's timeseries tab, features are grouped into modules defined through k-means clustering of expression data. Specifically, normalized and log2-transformed expression are first scaled and centered. Per each feature, the average expression across samples is then calculated per each time point. The top 1000 features with highest sd of the time point-specific average expression values are selected and singular value decomposition applied. K-means clustering is then applied on the singular vectors. The number of modules range from 2 to 10 and can be set from options menu on the timeseries tab.

Biomarker analysis
---------------------------
The Food and Drug Administration (FDA) defines a biomarker as ‘a defined characteristic that is measured as an indicator of normal biological processes, pathogenic processes, or responses to an exposure or intervention, including therapeutic interventions. A biomarker could be almost any objective and quantifiable functional, physiological, biochemical, or molecular measurement. Examples of molecular biomarkers include the presence of proteins in the blood, such as prostate-specific antigen (PSA) used in the diagnosis of prostate cancer, or the presence of mutations in tumor suppressor genes, like those in BRCA1 or BRCA2, predictive of breast cancer risk. Therefore, novel biomarker discovery is crucial to many areas, including clinical diagnostics and drug development.Bioinformatics has revolutionized biomarker discovery by integrating computational tools with high-throughput data analysis from genomics, proteomics, transcriptomics, and metabolomics. Researchers can now efficiently identify and analyze potential biomarkers, leading to cost-effective and accelerated research outcomes. On the Omics Playground, we have made available to all users state-of-the-art machine learning (ML) methods.

**Sparse Partial Least Squares (sPLS)**: sPLS is a ML technique that  extends  partial least square (PLS) regression. It is designed to analyze relationships between two datasets where it can handle multivariate high-dimensional data where the number of variables exceeds the number of observations -a common scenario in biological research- while employing dimensional reduction and variable selection. sPLS aims to identify patterns and relationships between continuous data within complex datasets by reducing the dimensionality of the data while maintaining its predictive power. This method combines the strengths of Partial Least Squares (PLS) regression with sparsity-inducing penalties. It seeks for linear combination between variables and, compared to PLS, it allows multiple response variable selection on both datasets. This is achieved through the use of LASSO penalization. Compared to CCA (Canonical Correlation Analysis), PLS relies on covariance rather than correlation coefficient. By incorporating sparsity constraints, sPLS can effectively identify a subset of variables that are most relevant for predicting the outcome of interest. sPLS is widely used in bioinformatic applications for biomarker discovery in biomedical research.

**Glmnet**:  The glmnet package in R provides extensive functionalities to identify putative biomarkers and construct predictive models for distinct biological outcome variables, such as prognosis, risk to disease, response to treatment. It supports binary (through logistic regression), continuous (through linear regression), as well as survival (through Cox-regression) variables. Glmnet offers procedures for fitting LASSO and/or elastic-net regularization in linear, logistic, and multinominal regression. Typically, and similarly to other ML techniques, Glmnet requires a response variable, a predictor variables and a regularization type with regularization strength. It employs L1 and L2 regularizations, which are LASSO and ridge penalties, respectively. While the ridge penalty shrinks the coefficients of correlated predictors towards each other, the lasso penalty picks one and discard the others. The elastic net penalty is a combination of LASSO and ridge penalty. Generally, these regularizations help preventing overfitting by adding a penalty term to the objective function. Importantly, Glmnet also provides approaches to perform cross-validation (CV) analyses. CV enables assessment of models performance and generability of the predicted features. Glmnet is also computational-efficient for large dataset. In summary, Glmnet provides tools for the implementation of regularized regression models, enabling building predictive models.

**Random Forest (RF)**: The RF algorithm is a powerful and versatile supervised ML method that combines multiple decision trees to make predictions. It is based on decision trees, which split the data based on features to classify observations. Each tree in a RF is built on a subset of the training data. Spefically, RF uses a bagging-like approach, where each tree is trained on a random data subset to hep reducing bias and variance. Another key aspect is feature randomness, where only a subset of features is considered for splitting at each node in a tree such that low correlations among trees are considered into the overall model's performance. As an ensemble learning method, RF combines outputs of multiple, distinct decision trees to improve accuracy and reduce overfitting. To make a prediction, RF aggregates (averages) the predictions of individual trees, therefore producing an accurate and stable prediction. Thus, by leveraging the collective wisdom of multiple decision trees trained on different subsets of data, the overall model accuracy and robustness is improved. All “hyperparameters” like node sizes, number of trees, as well as number of sampled features need to be set before training to optimize its performance. On the other hand, when used for classification purposes, RF selects the most common prediction among trees.

**Extreme Gradient Boosting (xgboost)**: The Extreme Gradient Boosting algorithm implemented in OPG is the one from Chen & Guestrin (2016). The R package xgboost includes functions for efficient linear model solver and tree learning. It supports various objective functions, including regression, classification and ranking for common machine learning tasks. Xgboost implememts regularization in the objective function to help preventing overfitting. In addition, two other techniques are used to further prevent overfitting: (i) shrinkage, which scales newly added weights after each step of tree boosting and so reduces the influence of each individual tree to leaves space for future trees needed to improve the model; (ii) feature subsampling, a technique also used in other algorithms, such as RandomForest. Subsampling features also prevents over-fitting to some extent. Xgboost is also efficient for sparse data and includes a sparsity-aware split finding algorithm. Finding the best tree split is a key issue in tree learning approaches. To achieve it, xgboost enumerates over all the possible splits on all the features using the exact greedy algorithm. The algorithm sorts the data based on normalized features. To identify and enumerate all possible splits for continuous features greedly, the exact greedy algorithm works on the sorted data. In this way a higher computational efficiency is achieved. However, in cases when the dataset does not entirely fit into memory, the exact greedy algorithm may be slow or not work properly. For this reason an approximate algorithm is used. The approximate algorithm has several steps: (i) identification of candidate splitting points based on percentiles of feature distribution; (ii) mapping features into buckets split by these points; (iii) aggregates the statistics; (iv) identify best solution. For a detailed description we refer to Chen and Guestrin, 2016.



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

**Kruskal-Wallis test**: The Kruskal-Wallis (KW) test is a non-parametric statistical test. It is generally used to assess significant differences between three (or more) groups of an independent variable. It is non-parametric because it does not assume an underlying normal distribution. It considered to be an extension of the non-parametric Mann-Whitney U-test / Wilcoxon Rank-Sum test to allow testing of more than two independent groups. Similarly to these tests, KW test is also based on rank place sums. The KW test is also considered as the non-parametric alternative of the one-way ANOVA test. The KW test relies on the assumptions that the groups are independent and have similar distribution. that The null hypothesis (Ho) of the KW test is that there are no differences between groups, specifically that the medians of the groups are equal. The KW test Ho is rejected if the median of at least 1 group differs from the other groups' median. 


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

Weighted Gene Co-expression Network Analysis
------------------------------------------
Weighted gene co-expression network analysis (WGCNA) is a powerful all-in-one analysis method that allows biologists to understand the transcriptome-wide relationships of all genes in a system rather than each gene in isolation. WGCNA enables the identification of clusters (modules) of features that exhibit correlated patterns and the assessment of the relationship between distinct clusters. Importantly, WGCNA also provides data on the association between modules and external traits, such as recorded sample phenotypes. Identification of gene correlation networks has high biological relevance as genes within the same module could share regulatory mechanisms and be functionally related within a molecular pathway at the cellular and inter-cellular level. WGCNA could inform on candidate biomarkers and druggable features for therapeutics. Although WGCNA has mostly been applied to transcriptomic data, its principles are suited to other omics, such as methylation data. WGCNA can be split into four main sequential analytical components: (1) construction of weighted gene correlation networks;  (2) identification of coexpression modules;  (3) association of genes with sample traits; (4) Inference of intramodular hub genes as candidate drivers of phenotypes. Outcomes are inferred by pairwise correlations between genes or modules in a guilty-by-association approach, where information about a gene is gained from its close neighbors in the network. 

**1. Construction of weighted correlation networks of genes:** typically, WGCNA starts with a matrix of data that features the gene expression of each sample. Pairwise correlations between genes across samples are measured. The correlation score of each gene pair indicates the similarity of their expression pattern and could suggest their potential functional relationship. The ‘weighted’ aspect aims to amplify the differences between strong and weak correlations by raising the correlation to a power defined by the user. A high correlation indicates the genes are strongly connected, whereas a low correlation suggests a weak connection.

**2. Identification of co-expression modules:** WGCNA uses the network’s weighted correlation coefficient information to place genes exhibiting significantly similar expression profiles into groups called modules. If genes have similar correlations with many shared neighbors in the network or have a large overlap of their network neighbors, the genes likely have similar expression patterns and can be grouped into the same module. 
To determine modules, hierarchical clustering is performed on the gene correlation network data. A dendrogram is generated where each branch identifies a specific module. Methods like dynamic tree cut can be employed to determine discrete modules containing genes with similar expression patterns. Each module is typically assigned a distinct ID and color.

**3. Correlate phenotypic traits with gene modules:** after defining modules using the dendrogram, the output must be simplified to one value per module, called the module eigengene. The eigengene is the first component from a principal component analysis and represents the overall module expression. As the module eigengene characterizes each module as a singular entity, it enables us to perform correlation analysis between modules to find those with similar expression behaviors or to determine how each module correlates with phenotypes. To determine whether these modules do have similar biological roles, the degree to which each module’s eigengene correlates to different patient traits, sample types, or disease outcomes can also be measure. These biological variables could include a patient’s age, gender, or weight, outcomes like remission or patient death, or whether samples originate from healthy or disease patients or from different organs or tumor locations.

**4. Identify potential driver genes:** from the identified modules of interest, genes that might be key factors for a particular trait or could influence other genes in that module could be identified. Each module may contain many genes; it is essential to identify so-called ‘hub genes’ that can be ideal candidates for further study. Hub genes are identified as the most highly connected genes within a module and, expectedly, the most strongly correlated with the phenotype of interest. The expression of a gene is also used to calculate the ‘module membership, which measures the degree to which a gene’s expression profile with a particular module within the expression network. Module membership is therefore a useful tool for prioritizing genes for further study. If the correlation is high, the gene is likely representative of the overall expression of the module as a whole and is well connected in the network. Similarly, the high correlation of this gene to the trait of interest further strengthens its likelihood as an important driver in that module.


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


Multi-omics data analysis
---------------------------
In Bioinformatics, multi-omics data analysis comprises integrative approaches aimed to leverage distinct molecular data types ('views') to unravel complex biological systems, discover biomarkers, and advance precision medicine. Its success relies on robust integration of multiple layers of biological data -such as genomics, transcriptomics, proteomics, metabolomics, and epigenomics- to translate big data into actionable biological insights. The rationale underlying multi-omics data analysis is that integration would uncover relationships and patterns that are not detectable when analyzing each omics layer in isolation. Importantly, emerging research works show that complex phenotypes, such as ageing and complex diseases, are driven by concomitant alteration in multiple biological layers, including the transcriptomes, the epigenome, and the proteome. Therefore, to achieve a deep understanding of the molecular processes underlying a certain condition, integrated analysis of multiple data types is essential. Multi-omics analysis is also powerful to aid development of precision medicine approaches as it may facilitate the association of distinct molecular patterns with patient-specific clinical outcomes. Bioinformatically, data integration -i.e., combining heterogeneous data types- presents important technical challenges. First, reconciling different data types is impacted by the distinct statistical distributions and noise profiles between data types, requiring preprocessing, including normalization and transformation, often tailored to the data type. Second, in most cases specific technologies and protocols are employed, in most cases unique to a datatype. This would inevitably triggers variable degree of intra- and inter-experimental variations (e.g., batch effects) across datatypes, which may need tailored adjustments.Third, certain data types, such as proteomics and metabolomics data measured by mass spectrometry, typically suffer of missing (undetected) values due to technical limitations in measuring the signal. While missing values may hinder data integration methods, imputing features (i.e., recovering a numerical entity from a missing value) without introducing bias is challenging but critical. Last but not least, each omics layer (e.g., genomics, proteomics) can involve thousands of features (genes, proteins), leading to the curse of dimensionality when combined. This increases computational costs, risks overfitting models, and necessitates dimension-reduction strategies. At present, no universal framework exists for multi-omics integration. Current methods and algorithms may perform differently depending on data types and data characteristics, with no one-size-fits-all solution. In OPG, we employ multiple, state-of-the-art methods for multi-omics data integration. We describe these methods below.

**SNF (Similarity Network Fusion)**:  SNF fuses multiple views (data types) together to construct an overall integrated matrix. Rather than merging raw measurements directly, SNF constructs a sample-similarity network for each omics dataset, where nodes represent samples (e.g., patients or biological specimens) and edges encode the similarity between samples which can be inferred by Euclidean or similar distance kernels. The SNF algorithm computes a matrix that quantifies pairwise similarities between samples within each data type. The datatype-specific matrices are then fused using a non-linear process to generate a unified similarity network emerges. This fused network captures complementary information from all omics layers. After fusion, spectral clustering can be applied to the integrated network to identify subgroups of samples, such as disease subtypes or phenotypic clusters. SNF is particularly valued for its ability to reveal robust sample groupings and potential biomarkers by capturing each omics' influence. Specifically, in OPG, prior to SNF, missing values (if any) are imputed using SVD2. For each data type, pairwise Pearson correlation distances are computed between all pairs of data points. Affinity matrices are then calculated from these distance matrices, using number of neighbors K=10-30 and hyperparameter alpha=0.5. Similarity Network Fusion then fuses the matrices together to construct an overall integrated matrix. OPG also performs clustering of SNF-integrated multi-omics data and generates an heatmap of normalized multi-omics data. In the heatmap, the SNF clusters capture multi-omic features exhibiting similar behavior, enabling assessment of samples' clustering driven by multiple data types/modalities.

**MOFA (Multi‐Omics Factor Analysis)**: MOFA is an unsupervided factorization-based framework for integrating and analyzing multi-omics datasets. MOFA generalizes principal component analysis (PCA) to the multi-omics context. It takes as input multiple data matrices -each representing a different omics modality (also referred to as 'views', e.g., genomics, transcriptomics, proteomics)- measured on the same sample set. The goal is to infer a set of hidden (latent) factors that capture the principal sources of variation across all data types. Each omics dataset is represented as a matrix (e.g., features as rows and samples in columns). MOFA decomposes each datatype-specific matrix into a shared factor matrix (representing the latent factors across all samples) and a set of weight matrices (one for each omics modality), plus a residual noise term. The model is formulated within a Bayesian probabilistic framework, assigning prior distributions to the latent factors, weights, and noise terms, ensuring that only relevant features and factors are emphasized. MOFA is trained to find the optimal set of latent factors and weights that best explain the observed multi-omics data. After training, MOFA quantifies how much variance each factor explains in each omics modality. Some factors may be shared across all data types, while others may be specific to a single modality.
The learned MOFA factors provide a low-dimensional representation of the data. A factor is a latent variable that captures a source of variation across the integrated data. Each factor captures a different source and dimension of heterogeneity in the integrated data, and thus represents an independent source of variation. Note that the interpretation of factors is analogous to the interpretation of the principal components in PCA. Factors with higher explained variance are typically considered more important for understanding the underlying structure and patterns in a multi-omics dataset. They may correspond to significant biological processes, cellular states, or experimental conditions that have a broader impact across multiple data modalities. As the inferred latent 'factors' represent the underlying principal axes of heterogeneity across the samples, these can be used for visualization, clustering, and subgroup discovery. After training, MOFA quantifies how much variance each factor explains in each omics modality. Some factors may be shared across all data types, while others may be specific to a single modality. In OPG, we show the amount of variance explained by each factor in each omic type from the trained MOFA analysis. We also show the total amount of variance explained by each view. Distinct omic types or data modalities often account for different variance observed in the data. This represents an expectation in multi-omics data analyses. A data type explaining more variance compared to another data type may capture either more biologically heterogenous signals, or be affected by technical noise. OPG also conducts analysis of magniture and direction of potential association between MOFA factors and available variables in the metadata file (samples.csv) by estimating Pearson's correlation coefficients. Factors with high (absolute) factor-trait correlation show large differences between phenotype conditions.

**DIABLO (Data Integration Analysis for Biomarker discovery using Latent cOmponents)**: DIABLO is a supervised multi-omics integration method. It uses known phenotype labels (e.g., disease vs. control) to guide the integration and feature selection process. The algorithm identifies latent components from each omics type. Latent componentas are variables constructed as linear combinations of the original features (e.g., genes, proteins). Shared latent components across all omics datasets that capture the common sources of variation relevant to the phenotype of interest are then searched. Feature selection identifies only subset of features from each omics dataset that are most informative for distinguishing between phenotypic groups. Feature selection is achieved using penalization techniques (e.g., Lasso-type penalties) to ensure only the most relevant features are kept. The aim is to maximize the ability to discriminate between phenotypic groups while ensuring that the selected features are correlated across datasets. In OPG, we implement RGCCA using the mixOmics R package.

**MCIA (Multiple Co-Inertia Analysis)**: MCIA is an exploratory multivariate statistical method designed for the integration and joint analysis of multiple high-dimensional, multi-omics datasets (such as transcriptomics, proteomics, metabolomics, etc.) measured on the same set of samples. MCIA extends the concept of Co-Inertia Analysis (CIA), which was originally limited to two datasets, to simultaneously handle three or more datasets and capture co-relationships and shared patterns of variation across several omics layers. Specifically, in OPG, MCIA is performed for a multi-block dataset using a modification to the Nonlinear Iterative Partial Least Squares method (NIPALS) proposed in (Hanafi et. al, 2010). MCIA seeks to simultaneously project all datasets into the same low-dimensional space. It does this by maximizing the sum of squared covariances between the projections of each dataset and a set of synthetic axes (latent variables). The core mathematical criterion is to find projections (axes) for each dataset such that the covariance between the projected datasets is maximized. In OPG, we implement MCIA using the nipalsMCIA R package.

**RGCCA (Regularized Generalized Canonical Correlation Analysis)**: RGCCA is an extension of canonical correlation analysis (CCA). It allows for the simultaneous analysis of more than 2 data blocks (often referred to as 'multi-block data'), making it suitable for multi-omics integration. It generalizes CCA by finding linear combinations (projections) of variables in each dataset that are maximally correlated with those in the other datasets, capturing shared structures. Regularization is incorporated to address the high-dimensionality and multicollinearity issue -typical of omics, biological data and potentially exacerbated in multi-omics data- where the number of features often exceeds the number of samples, making standard CCA inapplicable. RGCCA computes omics-specific latent variables (factors) by projecting each dataset onto a lower-dimensional space. These projections are chosen so that the resulting factors from different omics are as correlated as possible. By introducing regularization parameters, RGCCA can handle high-dimensional data and prevent overfitting, making it robust for omics applications compared to canonical CCA. In OPG, we implement RGCCA using the mixOmics R package.

**LASAGNA (Layered Approach to Simultaneous Analysis of Genomic and Network Associations)**: LASAGNA is a visualization, stacked layer model for multi-omics based on dimensional reducted. In the visualization, each layer corresponds to a data type. Specifically, each layer in the LASAGNA plot shows a data type-specific UMAP.

**Deep Learning with Multi-Omics Supervised Auto-Encoder**: Deep learning models, example of which are autoencoders (AE) and variational autoencoders (VAEs), learn compressed, meaningful latent representations from each omics layer, capturing both shared and unique biological signals. These latent spaces facilitate integration by aligning different data types into a common framework for downstream analysis. Deep learning has emerged as a powerful approach for integrating multi-omics data, addressing the challenges posed by high dimensionality, heterogeneity, and missing values across different omics layers. OPG offers deep learning via Semi-supervised auto-encoder (SAE) to integrate multi-omics data. SAE is performed using functionalities from the torch R package, including feature selection, SAE models, training/validation splitting, training with distinct optimizers, prediction and later feature extraction.
Specifically, the multi-omics, log2-transformed and normalized data matrix is first imputed if missing values are detected. Optionally, each data type can be 10x augmented. Data augmentation is conducted by (i) computing average feature standard deviation; (ii) expanding the matrix (by samples) 10 times the original size; (iii) adding to the expanded matrix random noise corresponding to the product between the original average feature standard deviation and random values drawn from a Gaussian distribution. To expand the breadth of features used in the SAE, genesets from gene set enrichment analysis can be optionally added. Noise can also be optionally added by checking the box. Adding noise triggers marginal increase in feature variations without altering the biological patterns in the data and its latent space. Noise is added as the product between average feature standard deviation and random values drawn from a Gaussian distribution. Multi-omics SAE is then performed using R6 class functionalities provided in the R torch R package. A GLU activation/gating mechanism can be optionally added. MultiBlockMultiTargetSAE ('MT') model is used to handle matrices of distinct features and predict multiple target variables at once. The SAE neural network is used to learn representations and make feature predictions. Internally, the model is organized into modules: (i) initialization, which converts data into torch sensors and split into training and validation; (ii) training, which sets the optimizer, defines the loss function, trains the model, and stores training and validation loss values; (iii) prediction, which runs the trained model to predict target probabilities; (iv) latent representation extraction, which returns the learned latent (encoded) representations for each view and the integrated multi-omics data; (v) feature importance by gradient, which computes feature importance for each input feature by analyzing how small changes (perturbations or gradients) may affect the output; (vi) model architecture dimensions, which returns the dimensions of encoder, decoder, and predictor layers in the model. To assess the performance of the classification SAE model, OPG also computes the confusion matrix by comparing the model’s predicted labels with the actual (ground truth) labels for a given phenotype.


Scripting and visualization
---------------------------
Data preprocessing was performed using bespoke scripts using R (R Core Team 2013) and packages from Bioconductor (Huber 2015). Statistical computation and visualization are all performed using latest playbase and Omics Playground version.


Supported species
---------------------------
Below is the list of species supported by OmicsPlayground. The list is in continuous update, and more species will be available soon.
Homo sapiens

Mus musculus


Rattus norvegicus  


Acanthochromis polyacanthus  


Acanthophacelus reticulata


Acyrthosiphon pisum


Aedes aegypti


Aedes albopictus
Ailuropoda melanoleuca
Aleurodes tabaci
Amborella trichopoda
Amphimedon queenslandica
Amphiprion ocellaris
Amphiprion testudineus
Amygdalus communis
Amygdalus persica
Ananas comosus
Anas boschas
Andropogon sorghum
Anolis carolinensis
Anopheles arabiensis
Anopheles funestus
Anopheles merus
Anopheles mysorensis
Anoplophora glabripennis
Anubis baboon
Aotus nancymaae
Aphanomyces astaci
Aphanomyces invadans
Aphritis gobio
Aplocheilus melastigmus
Aquila chrysaetos_chrysaetos
Arabidopsis lyrata_subsp._lyrata
Arabidopsis salsuginea
Arabidopsis thaliana
Ascidia intestinalis
Asparagus officinalis
Astatotilapia burtoni
Astatotilapia calliptera
Astyanax mexicanus
Aurata aurata
Australorbis glabratus
Balaena musculus
Barbus grahami
Beta vulgaris_subsp._vulgaris
Betta splendens
Bison bison_bison
Bombyx mori
Bos grunniens_mutus
Bos indicus_x_Bos_taurus
Bos taurus
Brachypodium distachyon
Brassica napus
Brassica rapa
Brienomyrus kingsleyae
Caenorhabditis briggsae
Caenorhabditis elegans
Caenorhabditis remanei
Calamoichthys calabaricus
Callithrix jacchus_jacchus
Callorhinchus milii
Camelina sativa
Camelus dromedarius
Camelus pacos
Canis dingo
Canis familiaris
Canis vulpes
Cannabis sativa
Capra aegagrus_hircus
Capsicum annuum
Caranx dumerili
Carassius auratus
Carlito syrichta
Cavia aperea_porcellus
Cebus capucinus_imitator
Cerasus avium
Cercocebus atys
Cercopithecus aethiops_sabaeus
Chaetochloa italica
Chelonoidis abingdonii
Chenopodium quinoa
Chinchilla lanigera
Chlamydomonas reinhardtii
Cistudo triunguis
Citellus parryii
Citellus tridecemlineatus
Citrus clementina
Clupea harengus_harengus
Cobitis heteroclita
Coelomys parahi
Corylus avellana
Coturnix coturnix_japanica
Crassostrea gigas
Cricetulus barabensis_griseus
Cricetus auratus
Crocodylus porosus
Cucumis melo
Cucumis sativus
Culex fatigans
Cyclopterus lumpus
Cynoglossus (Arelia)_semilaevis
Cyprinodon variegatus
Cyprinus carpio
Cyrtodiopsis dalmanii
Danio rerio
Daphnia magna
Daphnia pulex
Dasypus novemcinctus
Daucus carota_subsp._sativus
Delphinapterus leucas
Delphinus truncatus
Dendroctonus ponderosae
Denticeps clupeoides
Dicentrarchus labrax
Didelphis ursina
Didelphys domestica
Dioscorea cayenensis_subsp._rotundata
Dipodomys ordii
Drosophila ananassae
Drosophila erecta
Drosophila melanogaster
Drosophila mohavensis
Drosophila persimilis
Drosophila sechellia
Drosophila simulans
Drosophila virilis
Drosophila willistoni
Drosophila yakuba
Echinops telfairii
Electrophorus electricus
Elephas africanus
Emiliania huxleyi_CCMP1516
Equus caballus
Erinaceus europaeus
Euarctos americanus
Eucalyptus grandis
Felis catus
Ficedula albicollis
Folsomia candida
Fringilla canaria_Linnaeus,_1758
Fugu rubripes
Furina textilis
Fusarium oxysporum_f._sp._lycopersici_4287
Fusarium vanettenii_77-13-4
Fusarium verticillioides_7600
Gadus morhua
Gaeumannomyces tritici_R3-111a-1
Galago garnettii
Gallus gallus
Gasterosteus aculeatus
Geospiza fortis
Glycine max
Gopherus evgoodei
Gorilla gorilla_gorilla
Gossypium raimondii
Guillardia theta_CCMP2712
Haplochromis nyererei
Helianthus annuus
Helobdella robusta
Heterocephalus glaber
Hippocampus comes
Holocentrus calcarifer
Hordeum sativum
Hylobates concolor_leucogenys
Hypudaeus ochrogaster
Ictalurus punctatus
Ipomoea triloba
Ixodes dammini
Jaculus jaculus
Juglans regia
Kryptolebias marmoratus
Labrus bergylta
Lacerrta muralis
Lactuca sativa
Lamprologus brichardi
Larimichthys crocea
Latimeria chalumnae
Leo leo
Leo pardus
Lepeophtheirus salmonis
Lepisosteus oculatus
Lepus cuniculus
Limia formosa
Lingula anatina
Loa loa
Lottia gigantea
Lucilia cuprina
Lucioperca lucioperca
Lupinus angustifolius
Lycopersicon esculentum
Macaca cynomolgus
Macaca mulatta
Macaca nemestrina
Macrognathus armatus
Malus communis
Mandrillus leucophaeus
Manihot esculenta
Marmota marmota_marmota
Maylandia zebra
Medicago truncatula
Melampsora larici-populina_98AG31
Meleagris gallopavo
Melitaea cinxia
Microcebus murinus
Mollienesia latipinna
Monodon monoceros
Mus caroli
Mustela furo
Mustela vison
Myotis lucifugus
Myripristis murdjan
Naja scutata
Nannospalax ehrenbergi_galili
Nasonia vitripennis
Necator americanus
Nematostella vectensis
Nicotiana attenuata
Nothobranchius furzeri
Nymphaea colorata
Ochotona princeps
Octodon degus
Octopus bimaculoides
Olea europaea_subsp._europaea_var._sylvestris
Oncorhynchus kisutch
Oncorhynchus mykiss
Oncorhynchus tschawytscha
Opisthorchis viverrini
Oreochromis nilotica
Ornithorhynchus anatinus
Oryza brachyantha
Oryza glaberrima
Oryza sativa_(japonica_cultivar-group)
Oryzias latipes
Osteoglossum formosum
Ovis ammon_aries
Pan paniscus
Pan troglodytes
Panicum hallii
Papaver somniferum
Paramecium aurelia_syngen_4
Parastagonospora nodorum_SN15
Parus major
Pelodiscus sinensis
Peromyscus maniculatus_bairdii
Petromyzon marinus
Phascolarctos cinereus
Phascum patens
Phaseolus angularis
Phaseolus vulgaris
Phocoena sinus
Physeter catodon
Phytophthora infestans_strain_T30-4
Phytophthora sojae
Pistacia vera
Pisum sativum
Plasmodium falciparum
Platypoecilus maculatus
Pleuronectes maximus
Poephila guttata
Pomacentrus partitus
Pongo abelii
Populus balsamifera_subsp._trichocarpa
Propithecus coquereli
Pteropus vampyrus
Puccinia graminis_f._sp._tritici_CRL_75-36-700-3
Pygathrix bieti
Pygathrix roxellana
Pygocentrus nattereri
Quercus lobata
Rhinolophus ferrumequinum
Rosa chinensis
Saccharomyces cerevisiae
Salmo salar
Salmo trutta
Sarcophilus harrisii
Sclerotinia sclerotiorum_1980_UF-70
Selaginella moellendorffii
Seriola dorsalis
Sesamum indicum
Setaria viridis
Silurana tropicalis
Solanum tuberosum
Solenopsis invicta
Sorex araneus
Stomoxis calcitrans
Strigops habroptila
Strongylocentrotus purpuratus
Struthio australis
Sus scrofa
Tetrahymena thermophila_SB210
Thalarctos maritimus
Theobroma cacao
Trichinella spiralis
Trifolium pratense
Triticum aestivum
Triticum dicoccoides
Vitis vinifera
Zea mays
Zootermopsis nevadensis



REFERENCES 
---------------------------
Akhmedov M, Martinelli A, Geiger R and Kwee I (2020). "Omics Playground: A comprehensive self-service platform for visualization, analytics and exploration of Big Omics Data". NAR Genomics and Bioinformatics, Volume 2, Issue 1, March 2020; https://pubmed.ncbi.nlm.nih.gov/33575569/

Ashburner et al (2000). "Gene ontology: tool for the unification of biology." Nat Genet. May 2000;25(1):25-9; https://www.nature.com/articles/ng0500_25

Huber W, et al. (2015) Orchestrating high-throughput genomic analysis with Bioconductor. Nature Methods 12:115-121; https://www.nature.com/articles/nmeth.3252

Kanehisa, M. and Goto, S (2000). "KEGG: Kyoto Encyclopedia of Genes and Genomes." Nucleic Acids Res. 28, 27-30; https://www.genome.jp/kegg/

Leek J., Storey J. Capturing heterogeneity in gene expression studies by ‘surrogate variable analysis’ PLoS Genet. 2007; https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.0030161

Love MI, Huber W, Anders S (2014). “Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2.” Genome Biology, 15, 550; https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8

Zito A, Martinelli A, Masiero M, Akhmedov M, Kwee I. "NPM: latent batch effects correction of omics data by nearest-pair matching." Bioinformatics,  Volume 41, Issue 3, 2025; https://academic.oup.com/bioinformatics/article/41/3/btaf084/8042340

R Core Team (2013). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria; http://www.R-project.org/.

Ritchie ME, Phipson B, Wu D, Hu Y, Law CW, Shi W, Smyth GK (2015). “limma powers differential expression analyses for RNA-sequencing and microarray studies.” Nucleic Acids Research, 43(7); https://pmc.ncbi.nlm.nih.gov/articles/PMC4402510/

Robinson MD, McCarthy DJ, Smyth GK (2010). “edgeR: a Bioconductor package for differential expression analysis of digital gene expression data.” Bioinformatics, 26(1), 139-140; https://academic.oup.com/bioinformatics/article/26/1/139/182458

Wang B, Mezlini A, Demir F, Fiume M, Zu T, Brudno M, Haibe-Kains B, Goldenberg A (2014). “Similarity Network Fusion: a fast and effective method to aggregate multiple data types on a genome wide scale.” Nature Methods. https://www.nature.com/articles/nmeth.2810

Rohart F, Gautier B, Singh A, Lê Ca K (2017). "omixOmics: An R package for ‘omics feature selection and multiple data integration". https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005752

Argelaguet R, Velten B, Arnol D, Dietrich S, Zenz T, Marioni JC, Buettner F, Huber W, Stegle O (2018). "Multi‐Omics Factor Analysis—a framework for unsupervised integration of multi‐omics data sets". Mol Syst Biol(2018) 14: e8124; https://www.embopress.org/doi/full/10.15252/msb.20178124

Singh A, Shannon CP, Gautier B, Rohart F, Vacher M, Tebbutt SJ, Kim-Anh Lê Cao K (2019). "DIABLO: an integrative approach for identifying key molecular drivers from multi-omics assays". Bioinformatics, Sep 1;35(17):3055-3062; https://pubmed.ncbi.nlm.nih.gov/30657866/

Meng C, Kuster B, Culhane AC & Gholami AM  (2014). "A multivariate approach to the integration of multi-omics datasets". BMC Bioinformatics, 15:162; https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-15-162

Tenenhaus M, Tenenhaus A, Groenen PFJ (2017). "Regularized Generalized Canonical Correlation Analysis: A Framework for Sequential Multiblock Component Methods". Psychometrika; https://pubmed.ncbi.nlm.nih.gov/28536930/

