.. _Installation:

Installation
================================================================================

The current version of Omics Playground software (0.99) is implemented in R 
using the Shiny web application framework. You can either install the platform 
from the source code, or download our Docker image.


Run from source code
--------------------------------------------------------------------------------
The source code of the platform is available on 
`GitHub <https://github.com/IRB-Bioinformatics/OmicsPlayground>`__. You can 
download the latest release of the software (includes more data files) by cloning
this repository. We explain the steps required to set up the platform below.

1. Download or clone the repository. 
2. Be sure you have installed all necessary R packges by running the files 
``requirements.R`` and ``requirements2.R``.
3. In the ``/scripts`` folder, run ``run-all.R`` to build the datasets. This can take 
a couple of hours.
4. Change the current directory into the ``/shiny`` folder and run::

    R -e "rmarkdown::run()"


Run using the Docker file
--------------------------------------------------------------------------------
Pull the docker image using the command `docker pull bigomics/playground`.
Then run the docker with  
`docker run --rm -p 80:3838 bigomics/playground`. Then open `localhost` in your browser.

.. warning::

    The docker image requires about 5GB hard disk space.
    
    