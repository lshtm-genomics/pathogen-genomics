# ONT Assembly

## Overview

In this session we will be performing a de novo assembly of a genome using ONT reads. We will be using the `flye` assembler, which is specifically designed for long-read sequencing data. You will contrast these methods and the output of the assembly with the output of a short-read assembly using `spades` that you generated earlier in the course.

## Software and Data Requirements

We will be using the following software and data in this activity:

1. Flye - to perform de novo assembly of the genome
2. quast - for quality assessment of the assembly
3. kraken2 - to identify the taxonomic classification of the reads
4. minimap2 - to map the reads to a reference genome
5. samtools - to manipulate the alignment files
6. freebayes - to call variants from the alignment files
7. bcftools - to manipulate the variant calling files
8. mafft - to align the genome sequences
9. iqtree - to infer the phylogenetic tree
10. figtree - to visualise the phylogenetic tree
11. igv - to visualise the alignment files
12. aliview - to visualise the alignment files
13. R - to generate plots

We will now use mamba to create an environment to install the required software. 

```
mamba create -n ont-assembly flye quast prokka 
```

We will also be using data from the [this study](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0313545). 