.. _samples:

Samples file
================================================================================

The samples file (`samples.csv`) contains the phenotypic information of each sample. The first column contains the sample name, which should be unique, and must match the name given in the read counts file. 

The samples file  is a tabular (csv) file with the samples in the rows and the phenotypic data (metadata) in the columns. Note that the platform will not accept purely numerical values as phenotypes.

Below is a simple example of sample file, where each row in the column should be a sample with a unique ID. If we have duplicate IDs (two rows with sample5), these will be merged as its considered a technical replicate.
From the second column onwards, we have the metadata (also called phenotypes, descriptors, annotation, etc..). 

.. note::
    All phenotypes must contain at least one alphabet letter. This is done to avoid continuous values (as in the case of weight), as the platform expects discrete ranges. Having excessive numbers of phenotypic groups may also result in errors.


If we are analyzing a human study (it can be applied to any study) as 
seen in the ``samples.csv`` table below, the rows should be annonymized patients, identifyied 
uniquely by the first column (sample1, sample2...), and the other columns would be sample metadata (hair color, country, weight, age, etc.).

+---------+------------+-------------+--------+
|         | hair_color |   country   |  age   |
+=========+============+=============+========+
| sample1 |   blond    |    Japan    |  old   |
+---------+------------+-------------+--------+
| sample2 |   black    | Switzerland | young  |
+---------+------------+-------------+--------+
| sample3 |   blond    |     USA     | young  |
+---------+------------+-------------+--------+
| sample4 |   black    | Switzerland |  old   |
+---------+------------+-------------+--------+

As mentioned above, the age was converted from numeric (12, 52, 87) to young and old, so we can have a discrete range acceted in the platform.


.. seealso::
    If you are familiar with R, you can think of the samples file as a data.frame object. We provide an example samples file that can be accessed by installing playbase ``devtools::install_github("bigomics/playbase")`` and running ``playbase::SAMPLES``.
