.. _contrasts:

Contrasts file (optional)
================================================================================

The contrasts are an optional input in Omics Playground. It contains 
the groups (treatment versus controls, mutant versus wild-type, etc..) 
that will be tested against each other. The contrasts are a list of 
comparisons between groups.

There are two ways to define the contrasts: the long contrast form and the short contrast form. The contrast name rows need to be unique, both in short and long forms.

Long contrast form
--------------------------------------------------------------------------------

The long contrast form has the same number of rows of the samples file. That means the first column is the sample names (matching samples file), and the second column (onwards) contains the phenotypes.

The first row contains the name of the pairwise comparisons. All pairwise contrasts names must follow the format shown below with the groups joined together by  “_vs_” (e.g. piperaquine_vs_control).

For example, if you have 3 groups (A, B, C), you 
can test the following contrasts: A_vs_B, A_vs_C, B_vs_C.

Here is a minimal example of how the  ``contrasts.csv`` should look like. In this case, the groups 
will be hair color (blond vs. black) and country (Japan vs. Switzerland), as derived from the samples file.

+---------+----------------+----------------------+
|         | black_vs_blond | japan_vs_switzerland |
+=========+================+======================+
| sample1 |     blond      |        japan         |
+---------+----------------+----------------------+
| sample2 |     black      |     switzerland      |
+---------+----------------+----------------------+
| sample3 |     blond      |        japan         |
+---------+----------------+----------------------+
| sample4 |     black      |     switzerland      |
+---------+----------------+----------------------+

The column names (black_vs_blond) will be used to name the comparisons. The first name (black) will be used as the numerator of the contrast, and the second name (blond) will be used as the denominator of the contrast.
Inside the platform, we will transform the contrasts table to the following table:

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
    
Group-based contrasts (short form)
--------------------------------------------------------------------------------

The group-based contrast is especially useful in datasets with large number of samples, as assigning the contrasts to each sample can be cumbersome. Hoever, this approach only works if users are focusing on a single phenotype in their dataset.

Following the example above, if we would like to create a contrast between the two countries Japan and Switzerland, 
we will need to create a column called **group** in the sample file, which 
will contain the phenotypes (in this case country). To simplify, we could simply 
change the name of the column **country** to **group**.

Once we have the group column in the sample file, we can assign the contrasts as in the table below.

+-------------+----------------------+
|             | japan_vs_switzerland |
+=============+======================+
|    japan    |          1           |
+-------------+----------------------+
| switzerland |          -1          |
+-------------+----------------------+

We will search for the group column in the samples file, and we will create the contrasts based on the groups. Samples with 'japan' in the group column will be the numerator, and samples with 'switzerland' in the group column will be the denominator.

..note::
    1. The short contrast form requires a group column in the samples file. 
    2. The group column can be any column in the samples file, and it will be used to connect to the short contrasts. 
    3. The group column name must contain the word `group` (e.g. group, groups, group_name, etc..).
    4. If multiple group columns are found, only the first one will be matched. 

.. seealso::
    If you are familiar with R, you can think of the contrasts file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::CONTRASTS``.
