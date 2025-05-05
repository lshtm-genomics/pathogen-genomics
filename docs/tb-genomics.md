# TB Genomics

## Intended learning outcomes

The underlying theme of this practical is the use of genomics in understanding TB drug resistance and strain types. The practical is split into three sections. Each using different programs and with a different data type(s). For each section try to:

-	Be familiar with the programs presented and the types of analyses the can perform
-	Understand the format of the input/output data
-	Understand the conclusions you can draw from the analysis
-	Think about how you can apply these concepts to different organisms/scenarios

## 1. Whole genome phylogenetic analysis

In this section we will be generating phylogenetic trees from whole-genome polymorphisms. The dataset consists of 51 *M. tuberculosis* isolates, which underwent DNA sequencing using Illumina (Genome Analyser II, 76-bp paired-end) technology. Samples were isolated from 41 treatment-experienced TB patients attending a clinic in Kampala, Uganda, including longitudinal samples from five patients and cases of multi drug-resistant TB (MDR-TB). Raw reads were mapped to the H37Rv reference genome using BWA software and subsequently 6857 SNPs inferred employing SAMTOOLS and BCF/VCFTOOLS.  By concatenating the SNP locations for the 51 samples, a FASTA formatted dataset (uganda_gen.fasta) has been prepared to read into most phylogenetics software. Here we will be using seaview (Gouy, Guindon, & Gascuel, 2010), a graphical user interface for multiple sequence alignment and molecular phylogeny. 

Open up a new seaview window (by typing `seaview` on the terminal). Select File -> Open and choose "**uganda_gen.fasta**"

<figure markdown>
![seaview](img/img_1.jpg)
    <figcaption>Figure 1 Fasta-formatted sequence alignment of 51 Mtb isolates</figcaption>
</figure>


The alignment should appear in the seaview main window (Figure 1). The nucleotide bases are colour-coded to visually identify mismatches across sequences. The sequence identifiers on the left hand side of the window (e.g. A70659) consist of the patient ID, where multiple samples have been taken from the same patient the ID is suffixed with a number indicating which timepoint (e.g. A70136_1). A molecular typing method called spoligotyping has also been performed on most of the isolates. Box 1 explains the spoligotyping technique in _Mycobacterium tuberculosis_. The spoligotypes are in the `meta.csv` file.

To launch the phylogenetic analysis go to Trees -> Distance Methods. Select the Neighbor-joining method, Jukes-Cantor distance and Bootstrap with 100 replicates (see Figure 2)

<figure markdown>
![seaview](img/img_2.jpg)
    <figcaption>Figure 2 Distance analysis window</figcaption>
</figure>


<figure markdown>
![seaview](img/img_3.jpg)
    <figcaption>Figure 3 Neighbour-joining phylogenetic tree of 51 Mtb isolates</figcaption>
</figure>

Look at the resulting distance-based tree (Figure 3). Select Br lengths and Bootstrap tick boxes to display branch lengths and bootstrap values respectively.


!!! info 
    Box 1 - Spoligotyping
    The popular spoligotyping approach (Kamerbeek et al., 1997) exploits the polymorphism at the direct repeat (DR) locus of Mycobacterium tuberculosis. It is based on the PCR amplification of 43 short unique sequences (termed spacers) found between well-conserved 36-bp DRs and the subsequent hybridisation of the products onto a membrane with oligonucleotides complementary to each spacer. Since strains vary in the occurrence of particular spacers, each sample produces a distinctive spot pattern, which is then translated into a numerical code of 15 digits (known as octal code). Each code or group of related codes correspond to particular strain types such as Beijing, Central-Asian (CAS) or Latin-American (LAM) types.

    <figure markdown>
    ![seaview](img/img_4.jpg)
        <figcaption>Figure 4 Spoligotying scematic</figcaption>
    </figure>

!!! Question
    Compare whole-genome and spoligotype-based clustering. Which clustering method provides better resolution, i.e. enables a deeper isolate differentiation? In general, whole-genome SNP clustering provides greater resolution since isolates from the same spoligotype strain can be distinguished. How can these differences be explained?

Isolates sequenced at different time points from the same patient are closely related and cluster together with very short branch lengths among them. This is the case of A70136, A70763 and A70144 patients pointed with green arrows in Figure 3. On the contrary, isolates from patient A70067 and A70011 (red arrows) happen to be placed at distant positions in the tree and having different spoligotypes. **In which terms could this be explained? We will now explore this for patient A70067.**

You have seen that genome alignments can be used to construct phylogenetic trees to understand the population structure of samples. They tend to cluster by strain-type In the Kampalan set, but this also holds across a global set of samples. Spoligotyping is one way of defining strain-type, but *M. tuberculosis* sensu stricto can be classified into seven lineages, including four that are predominant; 1 Indo-Oceanic, 2 East-Asian including Beijing, 3 East-African-Indian, 4 Euro-American. These lineages are postulated to have differential roles in pathogenesis, disease outcome and variation in vaccine efficacy. For example, modern lineages, such as Beijing and Euro-American Haarlem strains exhibit more virulent phenotypes compared to ancient lineages, such as East African Indian (Coll et al, 2014).

Before you close seaview, save the phylogenetic tree be selecting “File -> Save rooted tree” using `uganda_gen.nwk` as the file name.

## 2. In-silico strain typing
Whole genome sequencing is making its way into a clinical setting to assist with patient management. Recent reports of sequencing *M. tuberculosis* from sputum from suspected drug resistant patients (Whitney et al, 2015) suggests it has a role in the management of tuberculosis. An exhaustive library of 1325 drug resistance markers has been established and integrated into an online tool that rapidly analyses raw sequence data and predicts resistance (Coll et al, 2015; Phelan et al 2019). The online tool is called “TB-profiler” and can be accessed via https://tbdr.lshtm.ac.uk/

Click on upload and drag and drop in the A70067_1.fastq.gz file to the upload box, change the “pairing” option to “single” and press “Submit”. The output will take a few minutes to generate, as there are many millions of reads. Similarly, run it for the other sample from patient A70067 (A70067_2.fastq.gz). 

<figure markdown>
![tb-profiler](img/img_5.jpg)
    <figcaption>Figure 5 tb-profiler upload screen</figcaption>
</figure>

!!! info
    ![](https://media.tenor.com/rec5dlPBK2cAAAAd/mr-bean-waiting.gif)

    If you are feeling extra impatient today you can find pre-computed results here:

    - A70067_1 - [https://tbdr.lshtm.ac.uk/results/0ba50688-d874-44e7-93c0-f78ec7334730](https://tbdr.lshtm.ac.uk/results/0ba50688-d874-44e7-93c0-f78ec7334730)
    - A70067_2 - [https://tbdr.lshtm.ac.uk/results/1dcefc81-70c1-40e4-8aa5-6ce03ee746bf](https://tbdr.lshtm.ac.uk/results/1dcefc81-70c1-40e4-8aa5-6ce03ee746bf)

!!! question
    How do the profiles differ from each other? Is this what you expected, especially when comparing to the original phylogenetic tree visualised in seaview? Are there any situations where this profiling approach could lead to an inconclusive result? 



## 3. Genetic variation visualisation between different strains

Here we use the Broad Institute's IGV genomic visualisation tool to consider SNP and structural variation differences between Kampalan Mtb alignments. 

Launch the IGV tool (typing “igv” on the command-line)

The IGV application window is divided into several controls and panels (see figure below). If sample attributes are loaded, they will be colour-coded and displayed as columns on the left-hand side of its corresponding identifier.

<figure markdown>
![tb-profiler](img/img_6.jpg)
    <figcaption>Figure 6 IGV overview panels and features</figcaption>
</figure>

We need to load in the reference genome and annotation into IGV. As you have done in previous practicals load the reference genome (MTB.fa) and annotation files (MTB.gff). 

You should now see the genome sequence in the top panel and the annotation in the bottom panel. Remember, the annotation file contains information about the location of genes, their function and other features of interest.

<figure markdown>
![tb-profiler](img/img_7.jpg)
    <figcaption>Figure 7 IGV view of the reference genome and annotation</figcaption>
</figure>

We will be exploring the genomic data for samples A70067_1 (CAS2, lineage3, September 2003) and A70067_2 (T2, lineage 4, April 2004) which, as discussed in the previous exercise, were isolated from the same patient but are different strains being introduced at different times. We should now load in the BAM files (alignment files) from these two different strains in the previous loaded IGV environment

Click on File > Load from file... and select the corresponding BAM files (A70067_1.bam and A70067_2.bam). Go to the chromosome region harbouring the *Rv3738c* gene (coordinates 4,189,463 to 4,190,410 bp) using the Search Box. Type in ‘Rv3738c’ or ‘Chromosome:4,189,463-4,190,410’ in the search box. 

The IGV screen should now be focused on that gene, but try zooming out and in.

<figure markdown>
![tb-profiler](img/img_8.jpg)
    <figcaption>Figure 8 Figure 4 IGV view showing a deletion at the *Rv3738c* locus in A70067_1 isolate</figcaption>
</figure>

**Take a closer look at both the BAM and coverage tracks around _Rv3738c_ gene. A deletion with respect to the reference can be spotted in A70067_1, whilst is absent in A70067_2.** Several signatures are indicative of such event. The most obvious is the lack of read coverage at the region. Large deletions such as this one should also have paried reads that span the deletion junction. To view this, right click on the coverage track and select "View as pairs". This will show you the paired reads that are mapped to the reference genome. Can you see this evidence in the A70067_1 sample? What about in A70067_2?

Samples belonging to CAS2 strains (e.g. A70067_1) are reported to have a deletion covering this region while other strains types are not. These regions are often called Regions of Difference (RD), and some RDs and SNPs are associated with strain-types (Coll et al, 2014). 

As shown earlier, Isolates A70067_1 and A70067_2 exhibit different drug susceptibility profiles (see Table 1). Both isolates were tested for Isoniazid (INH) and Rifampicin (RIF) anti-TB drugs, with A70067_1 being susceptible and A70067_2 multidrug-resistant. 

|      Patient    |     Date      |     SIT     |      Spoligotype family (lineage)    |     Drug     INH RIF    |     Compared      to    |     SNPs      All                  |     DR        |
|-----------------|---------------|-------------|--------------------------------------|-------------------------|-------------------------|------------------------------------|---------------|
|     A70067_1    |     Sep-03    |     288     |     CAS2 (lineage 3)                 |     S  S                |     H37Rv               |     1060 (539)                     |     15 (9)    |
|     A70067_2    |     Apr-04    |     2867    |     T2 (lineage 4)                   |     R  R                |     H37Rv               |     475 (246)                      |     11 (9)    |

Drugs: INH = Isoniazid , RIF=  Rifampicin, R = resistant, S = susceptible; DR = drug resistant candidates. SNP (non-synonymous changes). 

The primary mechanism for acquiring resistance in *M. tuberculosis* is the accumulation of point mutations (SNPs) in genes coding for drug targets or converting enzymes, and drug resistant disease arises through selection of mutants during inadequate treatment (Zhang & Vilcheze, 2005) or new transmitted resistant strains. **We will investigate polymorphism differences between A70067_1 and A70067_2 isolates in katG (_Rv1908c_, coordinates: 2153896-2156118 bp) and rpoB (_Rv0667_, coordinates: 759810-763328 bp) genes**, known to be associated with INH and RIF resistance respectively.

**Make use of the Search Box functionality again to go to the genes of interest. Try to spot differences between the susceptible and resistant isolates in terms of presence/absence of SNPs** (Figure 9). Note that lineage-specific SNPs may also be present. Table 2 contains drug resistance and lineage-specific SNPs found in the rpoB and katG genes. Mismatches are colour-coded, while nucleotides matching the reference are not. Nevertheless, not all mismatches are to be considered SNPs since some differences are due to sequencing errors. On average, 1 in every 1000 bases in the reads is expected to be incorrect. However, the high depth of coverage achieved by current sequencing platforms means SNPs can be distinguished from sequencing errors. True SNPs are expected to be mismatches occurring consistently across multiple reads at the same reference position, whereas mismatches at spurious locations are likely to be caused by sequencing errors.

<figure markdown>
![tb-profiler](img/img_9.jpg)
    <figcaption>Figure 9 IGV view focused on rpoB gene (locus tag: _Rv0667_, coordinates: 759810-763328 bp)</figcaption>
</figure>

!!! question
    Can you identify the mutations in the katG and rpoB genes that are associated with INH and RIF resistance respectively? How do these mutations differ between the two isolates? (Use the table below to help you).

|     Gene    |     Locus Name    |     Chromosome position    |     Nucleotide change    |     Amino acid change and codon number    |     Annotation                       |
|-------------|-------------------|----------------------------|--------------------------|-------------------------------------------|--------------------------------------|
|     _katG_    |     _Rv1908c_       |     2155168                |     C/A                  |     S315I                                 |     INH resistance conferring SNP    |
|     _katG_    |     _Rv1908c_       |     2155168                |     C/T                  |     S315N                                 |     INH resistance conferring SNP    |
|     _katG_    |     _Rv1908c_       |     2155168                |     C/G                  |     S315T                                 |     INH resistance conferring SNP    |
|     _katG_    |     _Rv1908c_       |     2154724                |     C/A                  |     R463L                                 |     Non-lineage 4 specific SNP       |
|     _rpoB_    |     _Rv0667_        |     761155                 |     C/T                  |     S450L                                 |     RIF resistance conferring SNP    |
|     _rpoB_    |     _Rv0667_        |     761155                 |     C/G                  |     D450W                                 |     RIF resistance conferring SNP    |
|     _rpoB_    |     _Rv0667_        |     762434                 |     T/G                  |     G876G                                 |     CAS/lineage 3 specific SNP       |
|     _rpoB_    |     _Rv0667_        |     763031                 |     T/C                  |     A1075A                                |     Non-lineage 4 specific SNP       |

## 4. Investigating transmission

Using web-based tools is a great way to run software without the need for installation or knowledge of Linux or the command-line. However, these are often not convenient to use if you have many samples, or don’t have access to the internet. Many of the tools that we have used today are also available as command-line software (or have equivalents). To demonstrate this, we will run tb-profiler on our terminal. 

Before running tb-profiler we will need to activate the environment using the following command:

```
conda activate tb-profiler
```

After this we can run the profiling as we have done using tbdr.lshtm.ac.uk. The following commands will change directory to where the data is and profile the first sample:

```
cd ~/Data/tb
tb-profiler profile --read1 A70067_1.fastq.gz --prefix A70067_1 --txt
```

There are a few arguments that we have given:

 - `--read1` : This allows us to specify the input fastq file
 - `--prefix` : This specifies the prefix for the output files
 - `--txt` : This ensures a text output will be created 

!!! question
    Have a look at the output (~/Data/tb/results/A70067_1.results.txt). Does it look the same as the profile we got from tbdr.lshtm.ac.uk? 

**Try running the command for A70067_2 by changing the appropriate parameters.**

We can then combine several runs of tb-profiler into a single summary file with the collate function:

```
tb-profiler collate
```

!!! question
    Have a look at the output file ~/Data/tb/tbprofiler.txt using a text editor.  Do the profiles look different?

Now we’ll run tb-profiler on all samples. Running it from fastq files can take some time as it must go through all processing steps including trimming, mapping and variant calling. As a result it can take a while to run. Tb-profiler also can take input from vcf files which just contain variants. To run the pipeline using the provided vcfs the command should look like:

```
tb-profiler profile --vcf A70067_1.vcf.gz --prefix A70067_1 --txt
```

Here we have just switched the `--read1` argument for the `--vcf` argument. 

To establish if transmission has occurred, we frequently calculate snp-distance between pairs of samples and pairs with a distance less than a pre-defined cutoff (e.g. 10 snps) can be linked. We can investigate this by telling tb-profiler to calculate snp-distances and save the results of any pairs below a threshold. To do we can add `--snp_dist 20` to the command. We have used a relaxed value of 20 here as we can always make this more stringent after.

Finally, it can be a bit repetitive to run the same command for many isolates. Ideally, we would like to harness the power of automation that is possible on the command-line so that we can profile all samples with just one command. Tb-profiler contains a batch mode that enables you set up your commands using a csv file that tells the pipeline where to look for the input files. To do this we’ll create a csv file using some command-line tools:

```
ls *.vcf.gz | awk 'BEGIN {print "id,vcf"} {print $1","$1}' | sed 's/.vcf.gz//' > vcf_files.csv
```

This will create a csv file with two columns: id and vcf. Have a look at the format by running `head vcf_files.csv`. Now you can tell tb-profiler to run the pipeline for all samples in the csv file by running:

```
tb-profiler batch --csv vcf_files.csv --args "--snp_dist 20"
```

You’ll notice we didn’t give the `--vcf` and `--prefix` arguments as these are read from the csv file. We do have to specify any additional arguments with `--args` followed by the arguments as you would type them for a single sample command.

After it has finished running we can again combine the output files into a single report by running:

```
tb-profiler collate --itol
```

This will produce in addition to the **tbprofiler.txt** output file it will also create a file called **tbprofiler.transmission_graph.json**. We will visualise this in a web-based tool that you can open in your web browser at [https://jodyphelan.github.io/tgv](https://jodyphelan.github.io/tgv)

After the page loads click on the upload box and select the .json file. This represents the samples as nodes and where pairs of samples have a snp-distance less or equal to the cutoff an edge will be drawn between them (Figure 10). 

!!! question
    Does this agree with the phylogenetic tree? What happens if you alter the snp-distance cutoff to be more conservative (e.g. 10 SNPs)? What do you think is the best cutoff to use?

<figure markdown>
![tb-profiler](img/img_10.jpg)
    <figcaption>Figure 10 A transmission network generated by tb-profiler</figcaption>
</figure>

Finally, the collate command also produces annotation config files that can be used with iTOL which is a web-based phylogenetic tree viewer. To do this open [https://itol.embl.de/](https://itol.embl.de/) and select “upload” on the top navbar. Click browse and select the .nwk  file that you saved at the beginning of the practical, followed by “upload”. You should now see the tree as you have seen before in seaview. To load the annotations simple drag and drop the following files onto the tree view:
-	Tbprofiler.lineage.itol.txt – a strip with the main lineage annotated.
-	Tbprofiler.dr.itol.txt – a strip indicating the drug resistance type.
-	Tbprofiler.dr.individ.itol.txt – circles for each individual drug where a solid filled circle indicates resistance.

<figure markdown>
![tb-profiler](img/img_11.jpg)
    <figcaption>Figure 11 Annotations profuced by tb-profiler visualised with iTOL</figcaption>
</figure>