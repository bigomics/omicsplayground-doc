.. _datachecks:


Checks before uploading
================================================================================

**Check #1**. Avoid special characters and empty spaces when naming your samples or phenotypes.
The platform is based on the R programming language, so certain characters are reserved for programming purposes.

As a good code of practice, never use any of these symbols when naming a sample or a phenotype. If you need to connect multiple elements, use underscore, “_” instead. Here’s an example:

.. figure:: ../dataprep/data_checks/p2.png
    :align: center
    :width: 65%

We test regularly which characters are allowed or not, we will update this list accordingly. Here is the current list of characters that are not allowed:

+--------------+--------------+------------------------+---------------------------------------------------------------+
| Matrix       | Part         | Characters not allowed | Additional criteria                                           |
+==============+==============+========================+===============================================================+
| sample.csv   | columns      | @ , : empty spaces, +  | Always start the name with a letter from A to Z (recommended) |
+--------------+--------------+------------------------+---------------------------------------------------------------+
| sample.csv   | phenotypes   | @ , : empty spaces     | Always start the name with a letter from A to Z (recommended) |
+--------------+--------------+------------------------+---------------------------------------------------------------+
| sample.csv   | rows (names) | @ , : empty spaces     |                                                               |
+--------------+--------------+------------------------+---------------------------------------------------------------+
| contrast.csv | columns      | @ , : empty spaces +   | Always start the name with a letter from A to Z (recommended) |
+--------------+--------------+------------------------+---------------------------------------------------------------+
| contrast.csv | contrasts    | @ , : empty spaces     | Always start the name with a letter from A to Z (recommended) |
+--------------+--------------+------------------------+---------------------------------------------------------------+

**Check #3** Make sure you have samples, counts and contrasts in your filenames.  For example, we accept experiment23_samples.csv, samples_experiment23.csv, but not experiment23.csv as sample input.


**Check #4**. Define intervals instead of using numeric phenotypes.
The platform does not cope with continuous numeric variables for phenotypes yet. To avoid that, our coders added a filter that flags phenotypes names “Time” or “Age” as unacceptable. The same applies for other continuous variables, such as height, weight, length, etc.

Instead, you should cluster the various numeric values into definite intervals and then name them accordingly (e.g. “Age_groups”, “Time_intervals”, etc…)

.. figure:: ../dataprep/data_checks/p4.png
    :align: center
    :width: 65%
