Hi-C data of embryonic stem cells
=================================

The following code and instructions were modified from a `HicExplorer tutorial <https://hicexplorer.readthedocs.io/en/latest/content/mES-HiC_analysis.html>`_ on aligning Hi-C data from female mouse, embryonic stem cells. It was adapted to generate a Hi-C contact map for chromosome 13 in ``.h5`` format. Additionally only data from the first replicate of `Marks <https://genomebiology.biomedcentral.com/articles/10.1186/s13059-015-0698-x>`_ *et al.* 2015 is used in this analysis. See the `main page <https://github.com/4DGB/hic-converter>`_ of the hic-converter repository for instruction on setting up a python computing environment and converting the ``.h5`` file to a ``.hic`` file.

Below are the needed bits of code for constructing a ``.h5`` contact map of chromosome 13 from paired-end ``.fastq.gz`` files

.. code-block::

    ## Set the working directory
    
    cd ./hic-converter/data

    ## Activate the python computing environment.

    conda activate hicexplorerenv

    ## Make directories for analysis.

    mkdir -p genome_mm10 fastq bam bwa

    ## Gather the mm10 reference, use wget and tar to unpack the data.
    wget http://hgdownload-test.cse.ucsc.edu/goldenPath/mm10/bigZips/chromFa.tar.gz -O genome_mm10/chromFa.tar.gz
    tar -xvzf genome_mm10/chromFa.tar.gz

    ## Index chromosome 13 via bwa index.
    bwa index -p bwa/chr13_index genome_mm10/chr13.fa

    ## Use the hicFindRestSite function from HicExplorer to find the SauIII restriction sites (GATC) across the mm10 genome. 
    hicFindRestSite --fasta ./genome_mm10/chr13.fa -o ./genome_mm10/chr13_SauIII_cut_sites.bed --searchPattern GATC

    ## Download data from Marks et al. for alignment.
    wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR195/007/SRR1956527/SRR1956527_1.fastq.gz -O ./fastq/SRR1956527_1.fastq.gz
    wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR195/007/SRR1956527/SRR1956527_2.fastq.gz -O ./fastq/SRR1956527_2.fastq.gz

    ## Align data seperately for each fastq file to chromosome 13 via bwa mem. Note we do not sort or filter the output bam files.
    bwa mem -A 1 -B 4 -E 50 -L 0 -t 14 bwa/chr13_index ./fastq/SRR1956527_1.fastq.gz | samtools view -Shb - > ./bam/SRR1956527_1_chr13.bam
    bwa mem -A 1 -B 4 -E 50 -L 0 -t 14 bwa/chr13_index ./fastq/SRR1956527_2.fastq.gz | samtools view -Shb - > ./bam/SRR1956527_2_chr13.bam

    ## Construct Hi-C contact matrix in .h5 format via the build matrix function from HicExplorer.
    hicBuildMatrix --samFiles ./bam/SRR1956527_1_chr13.bam ./bam/SRR1956527_2_chr13.bam \
        --restrictionSequence GATC --danglingSequence GATC --restrictionCutFile ./genome_mm10/chr13_SauIII_cut_sites.bed \
        --threads 5 --inputBufferSize 400000 \
        --QCfolder ./SRR1956527_chr13_QC --outFileName ./h5/SRR1956527_chr13.h5