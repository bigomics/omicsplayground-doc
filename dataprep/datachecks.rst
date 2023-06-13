.. _datachecks:


Checks before uploading
================================================================================

**Check #1**. Never use the special characters in the table below. The platform is based on the R programming language, so certain characters are reserved for programming purposes. As good practice, avoid using symbols when naming a sample or a phenotype. If you need to connect multiple elements, use underscore, “_” instead. Here’s an example:

We test regularly which characters are allowed or not, we will update this list accordingly. Here is the current list of characters that are not allowed:

+---------------+-----------------+------------------------+
| Input file    | Part            | Characters not allowed |
+===============+=================+========================+
| sample.csv    | column names    | @ , : empty spaces +   |
+---------------+-----------------+------------------------+
| sample.csv    | row names       | @ , : empty spaces     |
+---------------+-----------------+------------------------+
| sample.csv    | phenotype names | @ , : empty spaces     |
+---------------+-----------------+------------------------+
| contrasts.csv | column names    | @ , : empty spaces +   |
+---------------+-----------------+------------------------+
| contrasts.csv | contrast names  | @ , : empty spaces     |
+---------------+-----------------+------------------------+

**Check #2** Avoid starting your sample, phenotype or contrast names with special characters like (+, -, *, /, %, etc..). While the platform will accept these characters, they may be converted into a standard symbol like X. For example, if we label the sample.csv country column as `%country`, we will see X.country in some analysis in Omics Playground.

**Check #3** Make sure you have samples, counts and contrasts in your filenames. For example, we accept experiment23_samples.csv, samples_experiment23.csv, but not experiment23.csv as sample input.

**Check #4**. Define intervals instead of using numeric phenotypes.
The platform does not cope with continuous numeric variables for phenotypes yet. To avoid that, our coders added a filter that flags phenotypes names “Time” or “Age” as unacceptable. The same applies for other continuous variables, such as height, weight, length, etc.

Instead, you should cluster the various numeric values into definite intervals and then name them accordingly (e.g. “Age_groups”, “Time_intervals”, etc…)

.. figure:: ../dataprep/data_checks/p4.png
    :align: center
    :width: 65%
