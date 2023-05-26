.. _samples:

Samples file
================================================================================

The samples file describe the samples in the dataset. It is a tabular (csv) file with the samples in the rows and the metadata in the columns.

Below is a simple example of sample file, where each row in the column should be a sample with a unique ID. If we have duplicate IDs (two rows with sample5), these will be merged as its considered a technical replicate.
From the second column onwards, we have the metadata (also called phenotypes, descriptors, annotation, etc..). 

If we are analyzing a human study (it can be applied to any study) as seen in the table below, the rows should be annonymized pacients, identifyied uniquely by the first column, and the other columns would be sample metadata (hair color, country, weight, age, etc.).

+---------+------------+-------------+--------+
|         | hair color |   country   | weight |
+=========+============+=============+========+
| sample1 |   blond    |    Japan    |   55   |
+---------+------------+-------------+--------+
| sample2 |   black    | Switzerland |   43   |
+---------+------------+-------------+--------+
| sample3 |   blond    |     USA     |   87   |
+---------+------------+-------------+--------+
| sample4 |   black    | Switzerland |   65   |
+---------+------------+-------------+--------+

Below is a slightly more complicated samples example from a real in-vitro human study. The rows (notact_004,  notact_007) are samples from T lymphocytes activated or not by an antigen.

+------------+---------------------+-----------+------+-----------+
|            |       sample        | condition | time | activated |
+============+=====================+===========+======+===========+
| notact_004 | q2_tcell_notact_004 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_007 | q2_tcell_notact_007 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_008 | q2_tcell_notact_008 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_009 | q2_tcell_notact_009 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_010 | q2_tcell_notact_010 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_011 | q2_tcell_notact_011 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| notact_014 | q2_tcell_notact_014 |  notact   |  0h  |  notact   |
+------------+---------------------+-----------+------+-----------+
| act12h_018 | q3_tcell_act12h_018 |  act12h   | 12h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act12h_019 | q3_tcell_act12h_019 |  act12h   | 12h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act12h_020 | q3_tcell_act12h_020 |  act12h   | 12h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act24h_023 | q3_tcell_act24h_023 |  act24h   | 24h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act48h_026 | q3_tcell_act48h_026 |  act48h   | 48h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act48h_027 | q3_tcell_act48h_027 |  act48h   | 48h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act72h_028 | q3_tcell_act72h_028 |  act72h   | 72h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act72h_029 | q3_tcell_act72h_029 |  act72h   | 72h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act72h_030 | q3_tcell_act72h_030 |  act72h   | 72h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act96h_032 | q3_tcell_act96h_032 |  act96h   | 96h  |    act    |
+------------+---------------------+-----------+------+-----------+
| act96h_034 | q3_tcell_act96h_034 |  act96h   | 96h  |    act    |
+------------+---------------------+-----------+------+-----------+

.. seealso::
    If you are familiar with R, you can think of the samples file as a data.frame object. The samples file from the study above can be accessed by installing playbase `devtools::install_github("bigomics/playbase")` and running `playbase::SAMPLES`.
