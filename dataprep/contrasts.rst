.. _contrasts:

Contrasts file (optional)
================================================================================

The contrasts are an optional input in Omics Playground. It contains 
the groups (treatment versus controls, mutant versus wild-type, etc..) 
that will be tested against each other. The contrasts are a list of 
comparisons between groups.

There are two ways to define the contrasts: the long contrast form and the short contrast form. The contrast name rows need to be unique, both in short and long forms.

Sample-wise contrast (long form)
--------------------------------------------------------------------------------

The long contrast form has the same number of rows of the samples file. That means the first column is the sample names (matching samples file), and the second column (onwards) contains the phenotypes.

The first row contains the name of the pairwise comparisons. All pairwise contrasts names must follow the format shown below with the groups joined together by  “_vs_” (e.g. piperaquine_vs_control).

..note::
    1. All comparison names in the header **must** contain the separator “_vs_”
    2. Please use the exact condition names in the title as well as in their columns

For example, if you have 3 groups (A, B, C), you 
can test the following contrasts: A_vs_B, A_vs_C, B_vs_C.

Here is a minimal example of how the  ``contrasts.csv`` should look like. In this case, the groups 
will be hair color (blond vs. dark) and country (Japan vs. Switzerland), as derived from the samples file. Use NA (or empty field) to skip samples that do not belong to a contrast. 

+---------+----------------+----------------------+
|         | dark_vs_blond  | japan_vs_switzerland |
+=========+================+======================+
| sample1 |     blond      |        japan         |
+---------+----------------+----------------------+
| sample2 |     dark       |     switzerland      |
+---------+----------------+----------------------+
| sample3 |     blond      |        japan         |
+---------+----------------+----------------------+
| sample4 |     dark       |     switzerland      |
+---------+----------------+----------------------+
| sample5 |     dark       |         NA           |
+---------+----------------+----------------------+

The column names (dark_vs_blond) will be used to name the comparisons. The first name (dark) will be used as the numerator of the contrast, and the second name (blond) will be used as the denominator of the contrast. Alternatively, you can code the groups with -1 (reference group), 1 (main group) and 0 (not in comparison). This is shorter than writing the entire word but you have to be careful which group to assign +1 and -1 to. The -1 refers to the 'control' group that is the denominator or 'on-the-right' of the '_vs_' in the comparison name.

+---------+----------------+----------------------+
|         | dark_vs_blond  | japan_vs_switzerland |
+=========+================+======================+
| sample1 |      -1        |          1           |
+---------+----------------+----------------------+
| sample2 |       1        |         -1           |
+---------+----------------+----------------------+
| sample3 |      -1        |          1           |
+---------+----------------+----------------------+
| sample4 |       1        |         -1           |
+---------+----------------+----------------------+
| sample5 |       1        |          0           |
+---------+----------------+----------------------+

Any of the tables above can be provided to the platform. The zero means the sample5 will not be include in the comparison of japan_vs_switzerland.
    
Group-wise contrasts (short form)
--------------------------------------------------------------------------------

Sample-wise contrasts, as introduced in the previous paragraph, become tedious in datasets with large number of samples, as assigning the contrasts to each sample can be cumbersome. Instead, you can specify group-wise contrasts (or short form). However, this approach only works best if users are focusing on a single phenotype in their dataset.

Following the example above, if we would like to create a contrast between the two countries Japan and Switzerland, 
we will need to create a column called **group** in the sample file, which will contain the phenotypes (in this case country). To simplify, we could simply change the name of the column **country** to **group**.

Once we have the group column in the sample file, we can assign the contrasts as in the table below.

+-------------+----------------------+----------------------+----------------------+
|             | japan_vs_switzerland |   USA_vs_switzerland |   all_vs_switzerland |
+=============+======================+======================+======================+
|    japan    |          1           |          0           |         1            |
+-------------+----------------------+----------------------+----------------------+
|    USA      |          0           |          1           |         1            |
+-------------+----------------------+----------------------+----------------------+
| switzerland |          -1          |          -1          |        -1            |
+-------------+----------------------+----------------------+----------------------+

We will search for the group column in the samples file, and we will create the contrasts based on the groups. For the first comparison, samples with 'japan' in the group column will be the numerator, and samples with 'switzerland' in the group column will be the denominator. For the second comparison sample with 'USA' (as main group) will be compared to the samples with 'switzerland' (as reference group). The third comparison specifies both Japan and USA (together as one group) to be compared to Switzerland.

..note::
    1. The short contrast form requires a **group** column in the samples file. 
    2. The group column name must contain the word `group` (e.g. group, groups, group_name, etc..).
    3. If multiple group columns are found, only the first one will be matched. 

..seealso::
    If you are familiar with R, you can think of the contrasts file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::CONTRASTS``.
