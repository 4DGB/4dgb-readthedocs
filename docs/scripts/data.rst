
## A549 Cells From the ENCODE Project

The data listed here was generated for the ENCODE project by the Reddy lab at Duke University. It includes paired-end, Hi-C sequencing libraries on A549 cells, a cancer lung cell line treated with 100 nM dexamethasone. Specifically, the library of the first isogenic replicate ([ENCLB571GEP](https://www.encodeproject.org/experiments/ENCSR662QKG/)) with paired files [ENCFF039FYU](https://www.encodeproject.org/files/ENCFF039FYU/) and [ENCFF479RSE](https://www.encodeproject.org/files/ENCFF479RSE/) for the initial time point and the first isogenic replicate ([ENCLB870JCZ](https://www.encodeproject.org/experiments/ENCSR499RVD/)) with paired files [ENCFF668EDF](https://www.encodeproject.org/files/ENCFF668EDF/) and [ENCFF398SQH](https://www.encodeproject.org/files/ENCFF398SQH/) for the twelve hour time point (treated with 100 nM dexamethasone) were used to generate hic files via HiCExplorer. As an example, we have included the instructions for the construciton of the .h5 file of the twelve hour timepoint below.

### Building a contact map for chromosome 22

```
## Set the working directory
cd ./hic-converter/data

## Activate hic-explorer environment
conda activate hicexplorerenv

## Make directories for analysis.
mkdir -p GRCh38 fastq bam bwa

## Download the two paired fastq.gz files for the first replicate.
wget https://www.encodeproject.org/files/ENCFF668EDF/@@download/ENCFF668EDF.fastq.gz -O ./fastq/ENCFF668EDF_R1_001.fastq.gz
wget https://www.encodeproject.org/files/ENCFF398SQH/@@download/ENCFF398SQH.fastq.gz -O ./fastq/ENCFF398SQH_R2_001.fastq.gz

## Download the human reference genome from the ENCODE project.
wget https://www.encodeproject.org/files/GRCh38_no_alt_analysis_set_GCA_000001405.15/@@download/GRCh38_no_alt_analysis_set_GCA_000001405.15.fasta.gz -O ./GRCh38/GRCh38_no_alt_analysis_set_GCA_000001405.15.fasta.gz

## Unzip the genome.
gunzip ./GRCh38/GRCh38_no_alt_analysis_set_GCA_000001405.15.fasta.gz

## Find the MobI restriction sites (GATC) in the GRCh38, human reference genome.
hicFindRestSite --fasta ./GRCh38/GRCh38_no_alt_analysis_set_GCA_000001405.15.fasta -o ./GRCh38/GRCh38_MobI_cut_sites.bed --searchPattern GATC

## Index the human genome (this can take awhile but we only need to do it once)!
bwa index -p bwa/GRCh38_index ./GRCh38/GRCh38_no_alt_analysis_set_GCA_000001405.15.fasta 

## Align data to the human reference genome. 
bwa mem -A 1 -B 4 -E 50 -L 0 -t 14 bwa/GRCh38_index ./fastq/ENCFF668EDF_R1_001.fastq.gz | samtools view -SHb - > ./bam/ENCFF668EDF_R1_001.bam
bwa mem -A 1 -B 4 -E 50 -L 0 -t 14 bwa/GRCh38_index ./fastq/ENCFF398SQH_R2_001.fastq.gz | samtools view -SHb - > ./bam/ENCFF398SQH_R2_001.bam

## Build .h5 matrix for chromosome 22.
hicBuildMatrix --samFiles ./bam/ENCFF668EDF_R1_001.bam ./bam/ENCFF398SQH_R2_001.bam \
    --region chr22 --binSize 200000 \
    --threads 4 --inputBufferSize 200000 \
    --restrictionSequence GATC --danglingSequence GATC --restrictionCutFile ./GRCh38/GRCh38_MboI_cut_sites.bed \
    --QCfolder ENCLB870JCZ.chr22.12hr --outFileName ./h5/ENCLB870JCZ.chr22.200kb.12hr.h5
```

### Converting the chromosome 22 *.h5* contact map to *.hic*

```
## Activate hic-explorer environment
conda activate hicexplorerenv

## Change directory to tools
cd ./hic-converter/tools

## Convert a summary.txt.gz file to an .hic file for a single chromosome
./h5.to.hic.sh -m ../data/h5/ENCLB870JCZ.chr22.200kb.12hr.h5 -g ../data/sizes/GRCh38.chr22.size.bed -o ../data/hic/ENCLB870JCZ.chr22.200kb.12hr.hic
```