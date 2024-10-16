# Eukaryotic Annotation

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/epaule/BGA24)

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

run BRAKER3 with proteins + RNASeq

```
cd /workspace/BGA24

# run BRAKER3
time braker.pl --workingdir=BRAKER3 --genome=input_data/odCraCram1_SUPER1.fa.masked --bam=input_data/odCraCram1_SUPER1_RNASeq.bam \
    --prot_seq=input_data/subsampled_porifera_proteins.fa --AUGUSTUS_BIN_PATH=/usr/bin/ \
    --AUGUSTUS_SCRIPTS_PATH=/usr/share/augustus/scripts/ --threads 8 \
    --busco_lineage=metazoa_odb10 \
    --gm_max_intergenic 10000 --skipOptimize # remember to remove both these options for real jobs!
```
it should take ~30mins with 8 cores. There are precalculated files in example_output/

# create an UCSC assembly hub
```
time make_hub.py -e my@email.com \
    --genome /workspace/BGA24/BRAKER/odCraCram1_SUPER1.fa.masked --long_label "Chromosome 1 of the Crambe crambe genome" \
    --short_label odCraCra1_1  --bam /workshop/BGA24/BRAKER/VARUS.bam --threads 8 \
    --latin_name "Crambe crambe" \
    --assembly_version "artifically split custom assembly" \
    --hints /workspace/BGA24/BRAKER3/hintsfile.gff \
    --gene_track /workspace/BGA24/BRAKER3/braker.gtf BRAKER3
```
... which currently breaks, due to an incompatible gitpod library. So we will use https://asg_hubs.cog.sanger.ac.uk/assembly_hubs/hub.txt instead.
