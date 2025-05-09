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
mamba create -n ont-assembly flye quast prokka nanoplot
```

After it has finished you can activate the environment using:

```
mamba activate ont-assembly
```

We will also be using data from the [this study](https://journals.plos.org/globalpublichealth/article?id=10.1371/journal.pgph.0004099#sec013). 

We are going to be assembling the data for one of the samples from this study. You should download the fastq data from the ENA browser. The data is available under the accession `ERR12245902`. 

Create a folder called `ont-assembly` in your `data` directory. After you download the data, you can move it from your `Downloads` folder to the `ont-assembly` folder. 

## Read QC

Try to use nanoplot to summarise the quality of the reads. 

!!! question
    What is the average read length of the reads?


## Assembly

We will be using the `flye` assembler to perform the assembly. The a template of the command is as follows:

```
flye --nano-hq <fastq> --out-dir <output_dir> --threads 2 
```

Where `<fastq>` is the path to the fastq file, `<output_dir>` is the path to the output directory and `--threads` is the number of threads to use.


## Assembly QC

We will be using `quast` to perform the assembly quality control. The command is as follows:

```
quast.py <assembly.fasta> -o <output_dir> --threads 2
```

Where `<assembly.fasta>` is the path to the assembly file and `<output_dir>` is the path to the output directory.

Quast will generate a number of files in the output directory. Have a look at the `report.html` file by opening it via the file browser or using the command:

```
firefox <output_dir>/report.html
```

!!! question
    What is the N50 of the assembly?

    What is the number of contigs in the assembly?

    What is the total length of the assembly? How does this compare with the expected Mtb genome size?