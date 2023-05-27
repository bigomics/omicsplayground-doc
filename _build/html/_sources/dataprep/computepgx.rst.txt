.. computepgx:

What if I have many datasets?
================================================================================

The first step in any OmicsPlayground analysis is to upload data which can be used to create a pgx object. 
The pgx object is basically the core data structure in the OmicsPlayground upon which most analysis and plotting functions operate.

We made it very easy to create a pgx object from your own data. With a few R functions, you can convert several datasets into pgx objects 
that can be uploaded in Omics Playground.

In R, you can install the development version of playbase from GitHub with:

install.packages("devtools")
devtools::install_github("bigomics/playbase")

library(playbase)

# Here we create a pgx object that can be used in Omics Playground.

# Step 1. create a pgx object
pgx <- playbase::pgx.createPGX(
 counts = playbase::COUNTS,
 samples = playbase::SAMPLES,
 contrasts = playbase::CONTRASTS
)
# Step 2. Populate pgx object with results
pgx <- playbase::pgx.computePGX(
  pgx = pgx
)

All you have to do is substitute playbase::COUNTS, playbase::SAMPLES, and playbase::CONTRASTS with your own data.

.. seealso::
    In reality, there is a lot happening behing the `pgx.createPGX` and `pgx.computePGX`. If you are interested in learning more,
    please see our Github Wiki with more details on the statistics, normalization and filtering steps that are performed.
    Wiki. You can find it `here <https://github.com/bigomics/omicsplayground/wiki>`_.
