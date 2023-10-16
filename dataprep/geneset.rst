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

.. tip::
    If you want to create your own genesets, the easiest way is to download our example GMT file and open it in excel as tab-separated values.
    The first column is the geneset name (EGFR_TARGET_GENES), followed by any description (can be left empty) or
    the geneset `source website <https://www.gsea-msigdb.org/gsea/msigdb/human/geneset/EGFR_TARGET_GENES>`_ in the second column.
    Then finally the genes should be listed on the third and following columns (ABCA7, ACTB, etc.).
    After editing, save the file as a tab-separated values file and change the extension to .gmt.

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

            filePath <- getwd() # path to gmt file
            
            custom.geneset <- list()

            custom.geneset$gmt <- playbase::read.gmt(filePath)
            
            # perform some basic checks
            gmt.length <- length(custom.geneset$gmt)
            gmt.is.list <- is.list(custom.geneset$gmt)

            # clean genesets

            custom.geneset$gmt <- list(CUSTOM = custom.geneset$gmt)

            # convert gmt to OPG standard
            custom.geneset$gmt <- playbase::clean_gmt(custom.geneset$gmt,"CUSTOM")

            # compute custom geneset stats
            custom.geneset$gmt <- custom.geneset$gmt[!duplicated(names(custom.geneset$gmt))]
            custom.geneset$info$GSET_SIZE <- sapply(custom.geneset$gmt,length)

            # pass the custom.geneset as argument to pgx.computePGX
            pgx <- playbase::pgx.computePGX(
                pgx = pgx,
                custom.geneset = custom.geneset
            )
    
    
    