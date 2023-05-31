.. _computepgx:

What if I have many datasets?
================================================================================

The first step in any OmicsPlayground analysis is to upload data which can be used to create a pgx object. 
The pgx object is basically the core data structure in the OmicsPlayground upon which most analysis and plotting functions operate.

If you have many datasets (tens to hundreds), it might make sense to create the pgx object with an R script.

We made it very easy to create a pgx object from your own data. With a few R functions, you can convert several datasets into pgx objects 
that can be uploaded in Omics Playground.

Here we create a pgx object that can be used in Omics Playground:

.. code-block:: R

            # step 0: install necessary packages
            install.packages("devtools")
            devtools::install_github("bigomics/playbase")
            
            # step 1: create a pgx object with your samples, counts and contrasts
            pgx <- playbase::pgx.createPGX(
              counts = playbase::COUNTS,
              samples = playbase::SAMPLES,
              contrasts = playbase::CONTRASTS
            )

            # step 2: compute the pgx object

            pgx <- playbase::pgx.computePGX(
              pgx = pgx
            )

            # save the pgx object to your computer
            save(pgx, file = "choose_a_name.pgx.")
            
All you have to do is substitute ``playbase::COUNTS``, ``playbase::SAMPLES``, and ``playbase::CONTRASTS`` with your own data. You can then import the pgx object into Omics Playground.

.. seealso::
    In reality, there is a lot more happening behing the `pgx.createPGX` and `pgx.computePGX`. If you are interested in learning more,
    please see our Github Wiki with more details on the statistics, normalization and filtering steps that are performed.
    Wiki. You can find it `here <https://github.com/bigomics/omicsplayground/wiki>`_.
