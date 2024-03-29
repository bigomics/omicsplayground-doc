.. _samples:

Samples file
================================================================================

The samples file (`samples.csv`) contains the phenotypic information of each sample. The first column contains the sample name, which must be unique, and has to match the name given in the read counts file. 

The samples file  is a tabular (csv) file with the samples in the rows and the phenotypic data (metadata) in the columns. Note that the platform will not accept purely numerical values as phenotypes.


If we are analyzing a human study (it can be applied to any study) as 
seen in the ``samples.csv`` table below, the rows should be anonymized patients, identifyied 
uniquely by the first column (sample1, sample2...), and the other columns would be sample metadata or phenotypes (hair color, country, weight, age, etc.).

+---------+------------+-------------+--------+
|         | hair_color |   country   |  age   |
+=========+============+=============+========+
| sample1 |   blond    |    Japan    |  old   |
+---------+------------+-------------+--------+
| sample2 |   dark     | Switzerland | young  |
+---------+------------+-------------+--------+
| sample3 |   blond    |     USA     | young  |
+---------+------------+-------------+--------+
| sample4 |   dark     | Switzerland |  old   |
+---------+------------+-------------+--------+
| sample5 |   dark     |     USA     |  old   |
+---------+------------+-------------+--------+

As mentioned above, the age was converted from numeric (12, 52, 87) to young and old, since the platform currently does not support continuous values.

.. note::
    All phenotypes must contain at least one alphabet letter. This is done to avoid continuous values (as in the case of weight), since the platform expects discrete ranges. Having excessive numbers of phenotypic groups may also result in errors.

.. seealso::
    If you are familiar with R, you can think of the samples file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::SAMPLES``.
