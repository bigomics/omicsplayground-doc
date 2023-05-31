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

.. seealso::
    If you want to create your own genesets, you can follow the tutorials in R
    `here <https://rdrr.io/cran/ActivePathways/man/GMT.html>`_ or
    more information about the GMT format `here <https://www.gsea-msigdb.org/gsea/doc/GSEAUserGuideTEXT.htm#_Gene_Sets_File_GMT>`_. 


In Omics playground, GMT files are the backbone of several modules, 
where we aim to identify enriched gene sets associated with specific 
biological processes, diseases, or experimental conditions.

You can find the geneset availables in omicsplayground with the R package playbase.
First, install playbase with ``devtools::install_github("omicsplayground/playdata")`` 
and then run the command ``playdata::GSET_INFO``.

If you have your own geneset, or you want to include a GMT file from a database,
you can upload directly in the Upload module under Options.

.. seealso::
    If you are working in R, you can add your gmt file to the ``playbase::pgx.computePGX`` by providing the ``custom.geneset`` argument.
    custom.geneset argument. That should be a list where the first argument ``gmt`` is the gmt file (see ``playbase::EXAMPLE_GMT``), and the second argument is the name of the gmt file.

    Building on what we learned in the section :ref:`Computing PGX <computepgx>`
    , we can add our own geneset to the analysis with the followign call:
    
    .. code-block:: R

            pgx <- playbase::pgx.computePGX(
            pgx = pgx,
            genesets = list(
                gmt = playbase::EXAMPLE_GMT,
                info = "MyGeneset"
                )
            )
    Currently, we are supporting only 1 gmt file in the list, but we may implement multiple gmt files in the future.

    
    
    