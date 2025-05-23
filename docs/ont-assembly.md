# ONT Assembly

## Overview

In this session we will be performing a de novo assembly of a genome using ONT reads. We will be using the `flye` assembler, which is specifically designed for long-read sequencing data. You will contrast these methods and the output of the assembly with the output of a short-read assembly using `spades` that you generated earlier in the course.

## Software and Data Requirements

We will be using the following software and data in this activity:

1. Nanoplot - to perform read quality control
2. Flye - to perform de novo assembly of the genome
3. Quast - to perform assembly quality control
4. Prokka - to annotate the assembly

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

Where `<fastq>` is the path to the fastq file, `<output_dir>` is the path to the output directory and `--threads` is the number of threads to use. Flye will create a file called `assembly.fasta` in the output directory. This file contains the assembled genome, which is a collection of contigs.


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

    How to these metrics compare to the short-read assembly you generated earlier in the course?

## Annotation

We will be using `prokka` to annotate the assembly. The command is as follows:

```
prokka --outdir <output_dir>  <assembly.fasta> --cpus 2
```

Where `<output_dir>` is the path to the output directory, `<assembly.fasta>` is the path to the assembly file and `--cpus` is the number of threads to use. In the output directory there will be several files, including files that end in:

1. .fna - a fasta file with the nucleotide sequence of the genome
2. .ffn - a fasta file with the nucleotide sequence of the coding regions
3. .faa - a fasta file with the amino acid sequence of the coding regions
4. .gff - a text file with the location of genes 


# Comparing protein sequences

Open up the `.faa` file in a text editor (by double clicking on it in the file browser or running `open <filename>` on the terminal). You will see that the file contains the protein sequences of the coding regions. 

As we saw in the previous session, RpoB is a protein that is the target of the rifampicin antibiotic. We can use the protein sequence of RpoB to identify the presence of mutations that confer resistance to rifampicin. Look for the protein sequence of RpoB in the `.faa` file. You can search for it by using the command `ctrl + f` and typing `RNA polymerase subunit beta`. 

On the terminal run `aliview` to open the aliview program. Copy in the protein sequence of RpoB from the `.faa` file. You can do this by selecting the sequence in the text editor and using `ctrl + c` to copy it. Then in aliview, use `ctrl + v` to paste it.

Now copy the protein sequence from https://mycobrowser.epfl.ch/genes/Rv0667 and paste it into aliview.

!!! question
    The two sequences are exactly same length, so in this case we don't need to align them. What are the differences between the two sequences? Are any of the differences in the region that is known to confer resistance to rifampicin? (use the table from the TB genomics session to help you with this).
