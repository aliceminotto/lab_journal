**“Using MACS to identify peaks from ChipSeq data” \[Feng etal.\]**

output file output\_peaks.xls:

chromosome start end length summit tags p\_value fold\_enrichment FDR%(not given if no control data available)

Parameters

-h --help show help message and exit

-t --treatment=tFile input

-c control file

-n output file

-f format/default AUTO

-g genome size

-s read size/default extime

-p p value/ default 1e-5

-m m fold, select regions with enrichment ratio within mfold interval/ default 10/30 (DO NOT set lower than 10)

-w more consuming (store on pileup)

Advanced parameters

--bw bandwidth/default 300. If nomodel 2X this value is used for model building

--version

--single-wig

--nolambda fixed background lambda for peak calling

--slocal small region size in bp to calculate dynamic lambda/default 1000

--llocal large..../default 10000

--verbose

**ChipSeq Parameters**

**FRIP (similar to SPOT, Signal Portion of Tags)**

it's the % that fall in hospots. To be good it should be &lt;=1%.

Get reads overlapping in peaks (at least 20%) using intersectbed from bedtools:

\* intersectbed -a \[bam or bed file from aligner\] -b \[peaks.bed from MACS\] -c -f 0.20 &gt; output.intersectBed

Now sum up reads mapped to peaks from output.intersectBed

\*pearl getCnt.pl \#downloaded from mel\_chipseq on Github

This script calculated the total number of readcount for each file; we get the total number of reads instead using grep -c command line option.

**Results**

\* wt\_vs\_empty ~0.27

\* mutant\_vs\_wt ~0.38

\* mutant\_vs\_empty ~1.08

The first two results appear to be good, but it's probably because of the low number of peaks. (the second condition listed is the one I used as a control condition)

**NCS (Normalized Strand Cross-correlation) & RSC (Relative Strand Cross-correlation)**

Calculated with the phantompeakqualtools package (requires R packages -caTools and -show -this one is optional for parallel processing, can't run on old R versions-).

The first one should be &gt;=1.1 (or at least 1.05), the second one &gt;=1 (or at least 0.8).

**Results**

\*293FLP\_SETBP1\_WT\_hg19\_sorted.bam

NCS 1.015428

RCS 0.1779591

\* 293FLP\_SETBP1\_6870S\_hg19\_sorted.bam

NCS 1.015233

RCS 0.1968014

\* 293FLP\_SETBP1\_Empty\_hg19\_sorted.bam

NCS 1.010532

RCS 0.1841506

All these results do not meet by far the ENCODE standards, but this could be due to the fact that the TF doesn't bind the DNA in the common way, i.e. resulting in well defined narrow peaks, but in broad peaks.

**AT percentage in SETBP1 peaks**

There are an average of 325.66 bases per peak (5850 peaks with a total number of 1905119 bases).

The AT percentage in these regions is 65.6094%.

(The script I used to calculate the percentage is in my folder on the server and written in Python, it uses modular arithmetic to minimize RAM usage)

In the human genome there are 127592102000 bases, with a GC percentage of 41.31 (NCBI genomes, weighted average).

I checked the statistical significance of the percentages with R prop.test (chi square test with continuity correction), resulting in:

chi-squared: 27740.72

df (degree of freedom): 1

pvalue: &lt;2.2e-16

**STAR**

default parameters are optimized for mammalian genomes (for other species they need to be modified, especially min and max intron sizes).

It can be run utilizing annotated splice junctions loci to improve the sensitivity of the splice junctions detection (STAR incorporates annotated junction sequences in the suffix array and searches the seeds that cross the junctions simultaneously with the seeds that map contiguously to the genome).

If an alignment within one genomic window doesn't cover the entire read sequence, STAR will try to find two or more windows that cover the entire read, resulting in a chimeric alignment.

Note the inability to accurately detect splicing events that involve short (&lt;5-10 nt) sequence overhangs on the donor or acceptor site of a junction. This causes a significant underdetection of splicing events, and also increases significantly the misalignment rate, as such reads are likely to be mapped with few mismatches to a similar contiguous genomic region.

**Useful parameters for chimeric alignments**

chimScoreDropmax default 20

max difference of chimeric score from the read length

chimScoreSeparation default 10

min differences between the best chimeric score and the next one

**Whole genome sequencing**

**“Reducing INDEL calling error in whole genome and exome sequencing” \[Fang, Wu etal.\]**

Scalpel is a novel algorithm with a substantial improved accuracy over GATK-HaplotypeCaller, SOAP-indel and other six algorithms.

In the paper is suggested that PCR amplification induces a large number of error-prone INDELs to the library, and so INDEL calling quality could be effectively increased by reducing the rate of PCR amplification.

Ajay etal. \[“Accurate and comprehensive sequencing of personal genomes”\] reported that the number of SNVs detected exponentially increased until saturation at 40X to 45X average coverage. Moreover WGS at 60X mean coverage (after removing PCR duplicate) from HiSeq 2000 platform is needed to recover 95% of INDELs with Scalpel, which is much higher than the current sequencing practice.

The read depth requirement of INDELs detection in term of zigosity has not been well understood.

**“Comparison of insertion/deletion calling algorithms on human next generation sequencing data” \[Ghoneim, Myers etal.\]**

Here Pindel, GATK-UnifiedGenotyper and GATK-HaplotypeCaller are compared. It is suggested that researchers use concordance between HaplotypeCaller and Pindel with supporting reads adjustment to optimally call indels that validate.

The larger mean indel size called by Pindel is likely due to its identification of very large (about 2000 bp) deletions (neither of GATK tools can identify this kind of rearrangement).

Recommendation are:

\*HaplotypeCaller to detect small indels &lt;10bp

\*HaplotypeCaller in combination with Pindel for indels in the range of 10/100 bp

Note that Pindel default settings are optimal for WGS data or other sequencing data sets with relatively lower read depth.

Note: the coverage depth used in this paper was 24X, that is much lower than suggested in other papers, so the results have to be proven for higher coverages.

**Platypus**

**“Integrating mapping-, assembly- and haplotype- based approaches for calling variants in clinical sequencing applications” \[Rimmer, Phan etal.\]**

Platypus achieves high sensitivity and specificity for SNPs, indels and complex polymorphisms by using local de novo assembly to generate candidate variants. It is an order of magnitude faster than other existing tools.

It unites the usual approaches of mapping reads to a reference genome, of genome assembly and of borrowing information across related samples.

The assembler step consider small (default 1.5 kb) windows at a time. By contrast to most global assemblers, which typically identify relatively simple alternative paths (“bubbles”) to achieve high specificity, Platypus' candidate generation stage is designed to achieve high sensitivity.

Platypus' sensitivity for indels appears to be about 53%, a low value probably due to indels in homo-polymeric and tandem repetitive indel hotspots.

By the way local assembly allows Platypus to call variants considerably larger (up to 1kb) than those that can be identified within alignment. Note that, because of the algorithm nature, there is still a maximum length of insertion that can be called.

Using probabilistic escalating of empirical coverage data (human), it was found that Platypus achieves 95% sensitivity for de novo mutations with sequencing data with an average coverage of 35X (i.e. lower than suggested for other tools!).

When multiple mismatches appear within a specific distance (option minFlank), they are merged to form a sequence replacement polymorphism. Platypus identify:

\*SNPs

\*indels

\*replacement

\*complex variants

Note that Platypus assigns to each of these a generation frequency and assumes (for SNPs) that each of the 3 possible nucleotide is equally probable in the substitution, and this is not true.

Platypus also identifies regions where sequencing data provide positive support for the absence of variations (I couldn’t find any other tools with this feature listed).

Note that the maximum number of candidate variants considered per window (1.5 kb) is limited to 8 (this can be changed with the maxVariant option, but this increase the runtime!); for certain experiments designs, such as large number of samples or highly diverse regions, it will be beneficial to increase the threshold.

**Personal Notes**

The underlying logic of both Platypus and Scalpel \[“Accurate de novo and transmitted indel detection in exome-capture data using microassembly”, Narzisi, O'Rawe etal.\] re similar, in fact the last one performs localized micro-assembly, too. Scalpel requires that the read have been previously aligned with BWA using default parameters. Moreover Scalpel was written with exome data in mind.

**Pindel**

**“A pattern growth approach to dtect break points of large deletions ad medium sized insertions from paired end short reads” \[Ye, Shultz etal.\]**

It can't work in parallel, it's based on read alignment. Moreover it was written for 36bp Illumina reads, not sure if the default parameters and the algorithm itself were modified to meet modern standard. Mismatches are not allowed during alignment.

**BreakDancer**

**“BreakDancer: identification of genomic structural variation from paired-end read mapping” \[Fan, Abbott etal.\]**

It's based on two different algorithms: BreakDancerMax and BreakDancerMin. The first one provides genome wide detection of deletions, insertions, inversions and intrachromosomal and interchromosomal translocation (the last ones of the list are not investigated by previous softwares). On the other side BreakDancerMin focuses on detecting small indels (10-100 bp).

It's possible it could be useful for our applications to separate the two steps, utilizing just the first one, while relying on other more specific software for indel detections.

Insertion are still predicted with less accuracy than deletions. Note that the estimated FDR is high, about 10%, so it should be considered in case the researcher wants to minimize the error rate.

BreakDancer sensitively *and* accurately detects indels ranging from 10bp to 1Mb.

It can be run on RNAseq data too, to detect fusions and splicing.

**Installations and relate problems**

**BrakDancer**: doesn’t work from the download on its webpage, it is available on github with INSTALL.md instructions, but to install git is needed (and it has to be downloaded with you \[certificate expired\])

**Bioconductor**: it should be easily installed in R simply typing:

source(“http://bioconductor.org/biocLite.R”)

biocLite() this way all Bioconductor packages are installed, if only **DESeq** is needed, type DESeq in brackets

Couldn’t install it cause it requires R version 3.1.1 or later (2.10.1 now on server).

**Platypus**: easily downloaded (registration required) and installed following the instructions on the website and README file. Note that it has not been tested with Python 3 yet (what’s the version available on the new server?).

(error on line 922 when run on the demo files for pindel, no headers maybe? It works fine on other random trial files)

**Pindel**: if yum not available, it can be downloaded and installed from github without requiring any other package (but samtools), remember to set the right path for samtools (see instructions on README file). The tests performed ok once installed.

Requires:

-f reference fasta file

-o output file

-p pindel input text file OR/AND

-i bam input text file

-c (optional) chromosome name
