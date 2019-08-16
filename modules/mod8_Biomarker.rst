.. _Biomarker:

Biomarker analysis
================================================================================

This module performs the biomarker selection that can be used for classification or prediction purposes. To better understand which genes, mutations, or gene sets influence the final phenotype the most, Playground calculates a variable importance score for each feature using state-of-the-art machine learning algorithms, including LASSO \cite{Friedman2010Regularization}, elastic nets \cite{Candes2007TheDantzig}, random forests \cite{Breiman2007Random}, and extreme gradient boosting \cite{Chen2007Xgboost}, and provides the top 50 features according to cumulative ranking by the algorithms. By combining several methods, the platform aims to select the best possible biomarkers. The phenotype of interest can be multiple categories (classes) or patient survival data. Instead of choosing a phenotype, users can also specify a particular contrast from the analysis and perform biomarker selection (\textbf{Supp. Fig. 29}). 

The platform also provides a heatmap of samples based on identified top features. In addition, it generates a classification tree or survival tree using top features and provides expression boxplots by phenotype classes for features present in the tree (\textbf{Supp. Fig. 30}).