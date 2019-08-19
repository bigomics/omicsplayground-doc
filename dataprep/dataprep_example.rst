.. _Dataprep_example:

Data cleaning examples
================================================================================

The data cleaning and preprocessing includes preparing the input data, filtering, 
normalising, and precomputing statistics for some analyses. The data cleaning and 
preprocessing is performed offline using scripts in order to support real-time 
interaction and minimize user interface latency. The platform comes with the 
necessary scripts under the ``/scripts`` folder for data cleaning and preprocessing.


Offline computation
--------------------------------------------------------------------------------
Statistics for the differentially expressed genes (DEG) and gene set enrichment (GSE) 
analyses are precomputed to accelerate the visualisation on the interface.
