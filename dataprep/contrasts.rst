.. _contrasts:

Contrasts file (optional)
================================================================================

The contrasts are an optional input in Omics Playground. It contains 
the groups (treatment versus controls, mutant versus wild-type, etc..) 
that will be tested against each other. The contrasts are a list of 
comparisons between groups.

There are two ways to define the contrasts: the long contrast form and the short contrast form.

Long contrast form
--------------------------------------------------------------------------------

The long contrast form has the same number of rows of the samples file. That means the first column is the sample names (matching samples file), and the second column (onwards) contains the phenotypes.

The first row contains the name of the pairwise comparisons. All pairwise contrasts names must follow the format shown above with the groups joined together by  “_vs_” (e.g. piperaquine_vs_control).

For example, if you have 3 groups (A, B, C), you 
can test the following contrasts: A_vs_B, A_vs_C, B_vs_C.

The file ``contrasts.csv`` is optional because you can build 
the contrasts inside Omics Playground from the samples file. However, if you have a particularly complex datasets with multiple phenotypes and a large number of pairwise comparisons, you might want to generate this file through a script.

Here is a minimal example of how the  ``contrasts.csv`` should look like. In this case, the groups 
will be hair color (blond vs. black) and country (Japan vs. Switzerland), and derive from the samples file.

Here is a minimal example of contrasts, we can compare the countries (japan versus switzerland), or the hair color (blond versus black) as in the contrast table below.

The column names (black_vs_blond) will be used to name the comparisons. the first name (black) will be used as the numerator of the contrast, and the second name (blond) will be used as the denominator of the contrast.

+---------+----------------+----------------------+
|         | black_vs_blond | japan_vs_switzerland |
+=========+================+======================+
| sample1 |     blond      |        japan         |
+---------+----------------+----------------------+
| sample2 |     black      |     switzerland      |
+---------+----------------+----------------------+
| sample3 |     blond      |                      |
+---------+----------------+----------------------+
| sample4 |     black      |     switzerland      |
+---------+----------------+----------------------+

Inside the platform, we will transpare the contrasts table to the following table:

+---------+----------------+----------------------+
|         | black_vs_blond | japan_vs_switzerland |
+=========+================+======================+
| sample1 |       -1       |          1           |
+---------+----------------+----------------------+
| sample2 |       1        |          -1          |
+---------+----------------+----------------------+
| sample3 |       -1       |          0           |
+---------+----------------+----------------------+
| sample4 |       1        |          -1          |
+---------+----------------+----------------------+

Any of the tables above can be provided to the platform.

..
    There is one more input contrast, a short version with -1, 1, but I cannot find any example anywhere

.. seealso::
    If you are familiar with R, you can think of the contrasts file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::CONTRASTS``.
