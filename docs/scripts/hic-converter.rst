Hi-C File Converter
===================

Hi-C data can come in many formats including, for example, ``.hic``, ``.h5``, and ``.cool``. 
We are buliding a library of code to convert these formats to a ``.hic`` file compatable with the 4D-Genome Browser. 
The git repository, `hic-converter <https://github.com/4DGB/hic-converter>`_ is a collection of these tools and useful commands. 
This repository also holds Hi-C `data <https://github.com/4DGB/hic-converter/tree/main/data>`_ used in preprocessing and for setup of the 4D-Genome Browser Project.
In the following sections we highlight how to set up a python computing environment for running these scripts. 
We also walk through some example useage of our conversion tools. 

Installation and setup
-----------------------

Start by cloning the hic-converter git repository to a local directory. For example:

.. code-block::
    
    ## Clone the hic-converter git repo
    git clone git@github.com:4DGB/hic-converter.git

    ## Make scripts within the tools directory of the hic-converter repo executable
    chmod +x ./hic-converter/tools/*.sh ./hic-converter/tools/*.py


Generate a conda environment with an installation of `HiCExplorer <https://hicexplorer.readthedocs.io/en/latest/index.html>`_.
Other needed python libraries include:

* os 
* argparse 
* numpy 
* pandas 
* gzip
* subprocess

Below is an example ``conda create`` command for installing and setting up the needed python environment

.. code-block::

    conda create -n hicexplorerenv hicexplorer -c bioconda -c conda-forge

Dependencies
------------

The two largest dependencies for these conversion scripts are ``python`` and ``juicer`` tools:
Scripts here were developed using juicer version 1.22.01. The jar file of these tools are also stored `here <https://github.com/4DGB/hic-converter/tree/main/tools>`_.

* `Juicer tools jar file <https://github.com/aidenlab/juicer/wiki/Download>`_
* `Anaconda <https://www.anaconda.com/products/individual>`_

Example usage
-------------

Converting contact matrix from HiCExplorer as an ``.h5`` file to a ``.hic`` contact matrix
    
.. code-block::

    ## Activate hic-explorer environment
    conda activate hicexplorerenv

    ## Change directory to tools
    cd ./hic-converter/tools

    ## Convert the .h5 file to .hic formated file for Mus musculus chromosome 13
    ./h5.to.hic.sh -m ../data/h5/SRR1956527_chr13.h5 -g ../data/sizes/mm10.chr13.size.bed -o ../data/hic/SRR1956527_chr13.200kb.hic

Generating a ``.hic`` file from ``.summary.txt.gz`` file

.. code-block::

    ## Change directory to tools
    cd ./hic-converter/tools

    ## Convert a summary.txt.gz file to an .hic file for a single chromosome
    ./summary.to.chrom.hic.py -i ../data/summary/GSM2667262_WT1.HiC.rep1.mus.chr13.summary.txt.gz -g mm9 -c chr13 -O ../data/hic/GSM2667262_WT1.HiC.rep1.mus.chr13.200kb.hic

Convert juicer merged_nodups (long format) file for chromosome 22 to .hic

.. code-block::

    ## Activate hic-explorer environment
    conda activate hicexplorerenv

    ## Change directory to tools
    cd ./hic-converter/tools

    ## Envoke our long to chrom hic function
    ./long.to.chrom.hic.py -i ../data/long/merged_nodups.chr22.subsampled.txt.gz -g ../data/sizes/GRCh38.chr22.size.bed -c chr22 -O ../data/hic/chr22.10kb.hic -R 10000
