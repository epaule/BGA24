# Eukaryotic Annotation

This session is part of [**Biodiversity Genomics Academy 2024**](https://thebgacademyBGA23.org/)

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/epaule/S2G-manual-curation)

## Session Leader(s)

- Michael Paulini
- Camilla Santos

## Description

This is a workshop on eukaryotic gene annotation using [BRAKER](https://github.com/Gaius-Augustus/BRAKER) developed by Katharina Hoff et.al. We will cover alternative tools and cases where manual intervention might be needed.

## Prerequesites

1. Understanding the terms genome assembly, reads, contigs
2. Understanding of linux command line basics

## Data

in input_data/
* The data chromosome 1 of the ASG Crambe crambe assembly published as [GCA_963924555.1](https://www.ncbi.nlm.nih.gov/datasets/genome/GCA_963924555.1/) - odCraCram1_SUPER1.fa.masked
* RNASeq is a subsample of mRNA SRA submissions created by [VARUS](https://github.com/Gaius-Augustus/VARUS) (Bruhn et al. 2019, BMC Bioinformatics, 20:558) - odCraCram1_SUPER1_RNASeq.bam
* a subsampled reference protein set - subsampled_porifera_proteins.fa

## Instructions

### BRAKER3



```
cd /workspace

# delete output from a possible previous run if it exists
if [ -d BRAKER3 ]
then
    rm -rf BRAKER3
fi

# run BRAKER3
time braker.pl --workingdir=BRAKER3 --genome=input_data/odCraCram1_SUPER1.fa.masked --bam=input_data/odCraCram1_SUPER1_RNASeq.bam \
    --prot_seq=subsampled_porifera_proteins.fa --AUGUSTUS_BIN_PATH=/usr/bin/ \
    --AUGUSTUS_SCRIPTS_PATH=/usr/share/augustus/scripts/ --threads ${8} \
    --busco_lineage=metazoa_odb10\
    --gm_max_intergenic 10000 --skipOptimize # remember to remove both these options for real jobs!
```
