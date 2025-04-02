.. _counts:

Counts file
================================================================================

The file 'counts' contains the measurements (genes, proteins, etc..) for each sample listed in the samples file. Just
like the samples, the ``counts.csv`` file is tabular (.csv), where each row describes the features (genes, proteins, etc..)
and each column describes the samples.

The rows contains gene IDs, which can be in most common formats (such as HGCN or Ensembl), but not in the 
Entrez number format. If you are using Entrez numbers, please convert them to Ensembl IDs using tools such as `Syngo <https://www.syngoportal.org/convert>`_.

The values should always be numerical, with the exception of “NA” in case of a lack of data. Failure to do so will result in an error.

Below is a simple example of how a ``counts.csv`` file should look like.

+-------+---------+----------+----------+---------+---------+
|       | sample1 | sample2  | sample3  | sample4 | sample5 |
+=======+=========+==========+==========+=========+=========+
| gene1 | 543.6   | 1556.1   | 413.0    | 887.9   | 123.4   |
+-------+---------+----------+----------+---------+---------+
| gene2 | 6.5     | 14.7     | 2.3      | 42.4    | 56.7    |
+-------+---------+----------+----------+---------+---------+
| gene3 | 10.4    | 763.5    | NA       | 0       | 89.0    |
+-------+---------+----------+----------+---------+---------+
| gene4 | 3217.4  | 0        | 4983.2   | 7493.8  | 210.2   |
+-------+---------+----------+----------+---------+---------+
| gene5 | 98770.5 | 113498.0 | 498351.6 | 88134.1 | 345.6   |
+-------+---------+----------+----------+---------+---------+
| gene6 | 0       | NA       | 14.9     | 0       | 789.0   |
+-------+---------+----------+----------+---------+---------+
| gene7 | 47648.8 | 0        | 32682.0  | 93873.2 | 123.4   |
+-------+---------+----------+----------+---------+---------+

.. note::
    The formats accepted as features (genes, proteins are ENSEMBL, ENSEMBLTRAN, UNIGENE, REFSEQ, ACCNUM and UNIPROT and gene SYMBOL).
    Also note that the platform will not accept transcript IDs. You will need to convert them to Gene IDs. This will result in multiple gene entries that the platform will merge.

.. note::
    The minimum number of features (genes/proteins/etc) is 3. If you have less than 3 features, the platform will not accept the data.

.. seealso::
    If you are familiar with R, you can think of the counts file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::COUNTS``.
