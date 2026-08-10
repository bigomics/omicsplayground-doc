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


Single-cell RNA-seq counts
--------------------------------------------------------------------------------

.. _sc_counts:

When you select **scRNA-seq** as the data type, the counts file must be a
**genes x cells** matrix: one column per individual *cell*, not per sample.
Columns are cell barcodes, rows are gene symbols, and the values are **raw
integer UMI counts** — not normalized, not log-transformed, and not aggregated.

+--------+------------------+------------------+------------------+
|        | AAACATACAACCAC.1 | AAACATTGAGCTAC.1 | AAACATTGATCAGC.1 |
+========+==================+==================+==================+
| CD3E   | 0                | 0                | 3                |
+--------+------------------+------------------+------------------+
| MS4A1  | 0                | 12               | 0                |
+--------+------------------+------------------+------------------+
| LYZ    | 41               | 0                | 0                |
+--------+------------------+------------------+------------------+
| NKG7   | 0                | 0                | 0                |
+--------+------------------+------------------+------------------+

The ``samples.csv`` and ``contrasts.csv`` files must be keyed by the same cell
barcodes, so that each row describes one cell rather than one biological sample.
Your experimental grouping (treatment, condition, donor) becomes a column in
``samples.csv`` that is repeated across all cells belonging to that group.

Single-cell data has a characteristic profile, and the platform expects to see
it. As a reference, our example PBMC dataset of 14,053 genes x 1,000 cells has:

* between 783 and 6,628 UMIs per cell (median 1,636),
* between 501 and 1,687 detected genes per cell,
* about 95% zero values,
* clear marker gene separation (``MS4A1`` at 755 CPM in B cells versus 0 in T cells).

We recommend at least 1,000 cells. Cell type annotation uses Azimuth label
transfer, which needs enough distinct cells to find reference anchors; with only
a few hundred cells the annotation step will fail.

.. warning::
    A matrix whose columns are samples or sample-by-celltype groups (for example
    ``Sample001__NK_cells``, ``Sample001__Monocytes``, ...) is **pseudobulk**, not
    single-cell data, even if it was originally derived from a single-cell
    experiment. Such a matrix typically has only tens or hundreds of columns,
    uniform library sizes, 10,000+ detected genes per column and far fewer zeros.
    Upload it as **RNA-seq**, not scRNA-seq.

.. note::
    Use one gene ID format consistently for all rows. A file that mixes gene
    symbols with Ensembl IDs cannot be annotated reliably: the platform detects a
    single ID type from the majority of rows, and the remaining rows are
    mis-mapped or dropped.
