.. _counts:

Counts file
================================================================================

The file counts contains the measurements (genes, proteins, etc..) for each sample listed in the samples file. Just
like the samples, the ``counts.csv`` file is in a tabular format (.csv), and each row describes the features (genes, proteins, etc..)
and each column describes the samples.

Below is a simple example of how a ``counts.csv`` file should look like.

+-------+---------+----------+----------+---------+
|       | sample1 | sample2  | sample3  | sample4 |
+=======+=========+==========+==========+=========+
| gene1 | 543.6   | 1556.1   | 413.0    | 887.9   |
+-------+---------+----------+----------+---------+
| gene2 | 6.5     | 14.7     | 2.3      | 42.4    |
+-------+---------+----------+----------+---------+
| gene3 | 10.4    | 763.5    | 0        | 0       |
+-------+---------+----------+----------+---------+
| gene4 | 3217.4  | 0        | 4983.2   | 7493.8  |
+-------+---------+----------+----------+---------+
| gene5 | 98770.5 | 113498.0 | 498351.6 | 88134.1 |
+-------+---------+----------+----------+---------+
| gene6 | 0       | 0        | 14.9     | 0       |
+-------+---------+----------+----------+---------+
| gene7 | 47648.8 | 0        | 32682.0  | 93873.2 |
+-------+---------+----------+----------+---------+

.. seealso::
    The formats accepted as features (genes, proteins are ENSEMB, ENSEMBLTRAN, UNIGENE, REFSEQ,ACCNUM and UNIPROT and gene SYMBOL).

Below is a slightly more complicated counts example from a real in-vitro human study. The columns (notact_004,  notact_007) are samples from T lymphocytes activated or not by an antigen, and each row is an actual measurement of a gene from the study.

+-------+------------+------------+------------+-------------+
|       | notact_004 | notact_007 | notact_008 | notact_009  |
+=======+============+============+============+=============+
| A1BG  | 37.54      | 100.8      | 47.78      | 132.62      |
+-------+------------+------------+------------+-------------+
| A2M   | 1457.92    | 1321.71    | 1422.19    | 1726.83     |
+-------+------------+------------+------------+-------------+
| AAAS  | 16.96      | 47.5       | 15.96      | 50.96       |
+-------+------------+------------+------------+-------------+
| AACS  | 3.3        | 6.78       | 3.82       | 8.87        |
+-------+------------+------------+------------+-------------+
| AAGAB | 0          | 0          | 0          | 0           |
+-------+------------+------------+------------+-------------+
| AAK1  | 574.67     | 859.61     | 627.89     | 763.84      |
+-------+------------+------------+------------+-------------+
| AAMDC | 5.86       | 24.88      | 11.56      | 11.13       |
+-------+------------+------------+------------+-------------+


.. seealso::
    If you are familiar with R, you can think of the counts file as a data.frame object. The samples file from the study above can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::SAMPLES``.
