.. _contrasts:

Contrasts file (optional)
================================================================================

The contrasts are an optional input in Omics Playground. It contains 
the groups (treatment versus controls, mutant versus wild-type, etc..) 
that will be tested against each other. The contrasts are a list of 
comparisons between groups. For example, if you have 3 groups (A, B, C), you 
can test the following contrasts: A vs B, A vs C, B vs C.

The file ``contrasts.csv`` is optional because you can build 
the contrasts inside Omics Playground from the samples file.

Here is a minimal example of how the  ``contrasts.csv`` should look like. In this case, the groups 
will be hair color (blond vs. black) and country (Japan vs. Switzerland).

+---------+------------+-------------+--------+
|         | hair color |   country   | weight |
+=========+============+=============+========+
| sample1 |   blond    |    Japan    |   55   |
+---------+------------+-------------+--------+
| sample2 |   black    | Switzerland |   43   |
+---------+------------+-------------+--------+
| sample3 |   blond    |     Japan   |   87   |
+---------+------------+-------------+--------+
| sample4 |   black    | Switzerland |   65   |
+---------+------------+-------------+--------+

Similarly, we can see the countrasts example from the dataset mentioned in the previous sections. The rows (notact_004,  notact_007) are samples from T lymphocytes activated or not by an antigen, and each column is ancontrast that will be compared.

+------------+--------+-----------+-------+
|            | group  | activated | time  |
+============+========+===========+=======+
| notact_004 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_007 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_008 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_009 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_010 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_011 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| notact_014 | notact |  notact   |  0h   |
+------------+--------+-----------+-------+
| act12h_018 | act12h |    act    | 12h   |
+------------+--------+-----------+-------+
| act12h_019 | act12h |    act    | 12h   |
+------------+--------+-----------+-------+


In the platform, we will convert that to the contrasts table. The number 
one representes the numerator of the contrast, and the number -1 represents the denominator.

For example, the contrast ``act12h_vs_notact`` will be represented by the following table:


+--------+------------------+------------------+------------------+------------------+-------------------+
|        | act12h_vs_notact | act24h_vs_notact | act48h_vs_notact | act72h_vs_notact | act96h_vs_notact  |
+========+==================+==================+==================+==================+===================+
| notact |        -1        |        -1        |        -1        |        -1        |        -1         |
+--------+------------------+------------------+------------------+------------------+-------------------+
| act12h |        1         |        0         |        0         |        0         |        0          |
+--------+------------------+------------------+------------------+------------------+-------------------+
| act24h |        0         |        1         |        0         |        0         |        0          |
+--------+------------------+------------------+------------------+------------------+-------------------+
| act48h |        0         |        0         |        1         |        0         |        0          |
+--------+------------------+------------------+------------------+------------------+-------------------+
| act72h |        0         |        0         |        0         |        1         |        0          |
+--------+------------------+------------------+------------------+------------------+-------------------+
| act96h |        0         |        0         |        0         |        0         |        1          |
+--------+------------------+------------------+------------------+------------------+-------------------+

The samples act12 will have 1 (numerator) and noact will have -1 (denominator). That means we are calculating fold changes in 1/-1 groups. 

The number zero is simply ignored, it can be left empty.

..
    There is one more input contrast, a short version with -1, 1, but I cannot find any example anywhere

.. seealso::
    If you are familiar with R, you can think of the contrasts file as a data.frame object. The samples file from the study above can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::CONTRASTS``.
