.. _datachecks:


Checks before uploading
================================================================================

**Check #2**. Avoid regular expressions when naming your samples or phenotypes.
The platform is based on the R programming language, which makes heavy use of a feature called “regular expressions”. 

These are symbols that have a programming function beyond its common usage. Thus the full stop symbol ”.” usually indicates any alphanumeric character in a piece of code. Other regular expressions include “/”, “+”, “*”, etc…

As a good code of practice, never use any of these symbols when naming a sample or a phenotype. If you need to connect multiple elements, use underscore, “_” instead. Here’s an example:

.. figure:: ../dataprep/data_checks/p2.png
    :align: center
    :width: 65%



**Check #3**. Don't use spaces in your sample or phenotype names.
Empty spaces in the names of samples or phenotypes will cause the platform to throw an error message. If you need to create complex names, connect them via an underscore. Here’s an example:

.. figure:: ../dataprep/data_checks/p3.png
    :align: center
    :width: 65%


**Check #4**. Define intervals instead of using numeric phenotypes.
The platform does not cope with continuous numeric variables for phenotypes yet. To avoid that, our coders added a filter that flags phenotypes names “Time” or “Age” as unacceptable. The same applies for other continuous variables, such as height, weight, length, etc.

Instead, you should cluster the various numeric values into definite intervals and then name them accordingly (e.g. “Age_groups”, “Time_intervals”, etc…)

.. figure:: ../dataprep/data_checks/p4.png
    :align: center
    :width: 65%
