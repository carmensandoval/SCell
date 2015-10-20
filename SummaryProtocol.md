# Summary Protocol

This document is intended to serve as a general outline of the steps to follow when analyzing single-cell RNA-seq libraries, from pre-processing and alignment, to clustering and estimating gene expression variation across cells and clusters.

## 1. Library Pre-processing

#####1a. Read Trimming

We recommend using the wrapper [**TrimGalore!**](http://www.bioinformatics.babraham.ac.uk/projects/trim_galore/), which employs [**cutadapt**](https://wiki.gacrc.uga.edu/wiki/Cutadapt) to trim leftover adapter sequences from reads after demultiplexing, as well as to trim low quality bases at the ends of reads.

To trim reads for leftover barcode sequences and low-quality bases, run the shell script [**sub_trim.sh**](https://dl.dropboxusercontent.com/u/9990581/SCell/PreProcessingScripts/sub_trim.sh), specifying the directory of single-cell libraries you want to trim. 


This script calls the PBS script [**trim.pbs**](https://dl.dropboxusercontent.com/u/9990581/SCell/PreProcessingScripts/trim.pbs).

This will create a new subdirectory called **trimmed**, which contains the trimmed versions of your raw single-cell data, in fastq format.

#####1b. Read Alignment
The scripts provided here employ [**TopHat 2**](https://ccb.jhu.edu/software/tophat/index.shtml), a splice junction short read aligner for RNA-Seq data.

Run the shell script **sub_align.sh**, which calls the PBS script **align.pbs**.
This will create a new directory called **tophat_out**, which contains the .bam files and alignment summary statistics for each single-cell library.

Summarize the mapping rates contained in the file **accepted_hits.stats** from each library using the script **comp_mapping_rates.m**

#####1c. Gene Expression Quantification
The [**FeatureCounts**](http://bioinformatics.oxfordjournals.org/content/30/7/923.full.pdf?keytype=ref&ijkey=ZzPz96t2lqzAH6F) program, from the [**SubRead**](http://subread.sourceforge.net/) package, assigns aligned reads/fragments to genomic features, such as genes. The output of this read summarization process is a count table, which contains the number of reads/fragments assigned to each feature in each of your single-cell libraries.

To obtain a count table from your aligned single-cell libraries, run the shell script 
**sub_featureCounts.sh**, which calls the PBS script **run_featureCounts.pbs**. 

You will need a GTF file containing the features you want to summarize aligned reads to. Refer to [this example](https://dl.dropboxusercontent.com/u/9990581/genes_ercc.gtf), or supply your own annotation file.

This will create a new directory named **featureCounts_out**, which contains a tab-delimited text file in which rows are genes, and columns are the single-cell libraries from your sample.
  
##2. Data Analysis using SCell

#####Quality Control

#####Library Normalization
By library size 

Cell-cycle state regression

ERCC spike-in molecules regression

#####Feature Selection
Gene panel for analysis.

- variation (index of dispersion)
- percentage of cells expressing
- zero-inflation power

#####PCA / Clustering
Varimax Rotation

Sample Scores

Gene Loadings

Clustering Algorithms

- k-means
- Gaussian mixture
- DBSCAN
- Minkowski weighted k-means

Viewing Gene Expression across samples
 - Regression methods
 
####Minimum-Spanning Trees and Lineage Progression

Viewing Gene Expression across tree
