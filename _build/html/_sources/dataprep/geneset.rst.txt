.. _geneset:

Loading custom geneset files
================================================================================

GMT (Gene Matrix Transposed) files are a format commonly used 
in bioinformatics and gene set enrichment analysis (GSEA). 

Gene sets are collections of genes that share certain biological 
characteristics, such as being involved in the same biological 
pathway or having similar functions. GSEA is a computational 
method used to determine whether a particular gene set is 
significantly enriched in a given dataset of gene expression.

In a GMT file, each line represents a gene set and consists
of a gene set name, and the list of genes 
belonging to that set. The gene names are typically represented 
using gene symbols or other identifiers. 
 
In Omics playground, GMT files are the backbone of several modules, 
where we aim to identify enriched gene sets associated with specific 
biological processes, diseases, or experimental conditions.

You can find the geneset availables in omicsplayground with the R package playbase.
First, install playbase with ``devtools::install_github("omicsplayground/playdata")`` 
and then run the command ``playdata::GSET_INFO``.

If you have your own geneset, or you want to include a GMT file from a database,
you can upload directly in the Upload module under Options.

.. seealso::
    If you want to create your own genesets, you can follow the tutorials in R
    `here <https://www.gsea-msigdb.org/gsea/doc/GSEAUserGuideTEXT.htm#_Gene_Sets_File_GMT>`_ or
    more information about the GMT format `here <https://www.gsea-msigdb.org/gsea/doc/GSEAUserGuideTEXT.htm#_Gene_Sets_File_GMT>`_. 
