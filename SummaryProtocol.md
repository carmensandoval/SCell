# Single-Cell RNA-seq Analysis Protocol

This document is intended to serve as a general outline of the steps to follow when analyzing single-cell RNA-seq libraries, from pre-processing and alignment, to clustering and estimating gene expression variation across cells and clusters.

## 1. Library Pre-processing

#### 1a. Read Trimming and FastQC

We recommend using the wrapper [**TrimGalore!**](http://www.bioinformatics.babraham.ac.uk/projects/trim_galore/), which employs [**cutadapt**](https://wiki.gacrc.uga.edu/wiki/Cutadapt) to trim leftover adapter sequences from reads after demultiplexing, as well as to trim low quality bases at the ends of reads.

To trim reads for leftover barcode sequences and low-quality bases, run the shell script [`sub_trim.sh`](https://dl.dropboxusercontent.com/u/9990581/SCell/PreProcessingScripts/sub_trim.sh) from the terminal, specifying the directory of single-cell libraries you want to trim. This usually corresponds to a sequencing plate of single-cell libraries.

```shell
sh sub_trim.sh sequencingRunDir
```

This script calls and executes the PBS script [`trim.pbs`](https://dl.dropboxusercontent.com/u/9990581/SCell/PreProcessingScripts/trim.pbs), which will submit the trimming jobs for each of the libraries in the specified directory as a job array.

A new subdirectory called `/trimmed` will be created under each individual library's directory, which now contains the quality-and-barcode-trimmed reads in a `fastq` file.

The `/trimmed` subdirectory will also contain the output from [**FastQC**](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/) for each individual library in your sequencing run.

#### 1b. Read Alignment
The scripts provided here make use of [**TopHat 2**](https://ccb.jhu.edu/software/tophat/index.shtml), a splice junction short read aligner for RNA-Seq data.

To align your single-cell libraries, run the shell script [`sub_align.sh`]() from the terminal, specifying the directory of single-cell libraries you wish to align. This script calls and executes the PBS script [`align.pbs`](), which will submit the alignment jobs for each of the *trimmed* libraries in the specified directory as a job array.

```sh
sh sub_align.sh /path/to/sequencingRunDir
```

In the `sub_align.sh` script, you must specify:

 • The path to the Bowtie genome index directory containing the necessary `.bt2` files for alignment.

 • The path to the transcriptome index containing the necessary `.bt2` files to be used for the guided alignment.

 • The base name for the `.bt2` files in the Bowtie genome index directory to be used for alignment.

```sh
export bowtie_idx_path="/usr/refs/Homo_sapiens/NCBI/build37.2/Sequence/Bowtie2Index/"
```

```sh
export transcriptome_idx_path="/usr/refs/Homo_sapiens/NCBI/build37.2/Annotation/Genes/genes"
```
```sh
export genome_name="genome_name"
```

This will create a new directory called `/tophat_out`, which contains the `.bam` files and alignment summary statistics corresponding to each single-cell library.

Mapping rate statistics contained in the file `accepted_hits.stats` from each library can be summarized by running the script `comp_mapping_rates.m`

#### 1c. Gene Expression Quantification

[**FeatureCounts**](http://bioinformatics.oxfordjournals.org/content/30/7/923.full.pdf?keytype=ref&ijkey=ZzPz96t2lqzAH6F), part of the [**SubRead**](http://subread.sourceforge.net/) package, assigns aligned reads/fragments to genomic features, such as genes.

The output of this read summarization process is a counts matrix, which contains the number of reads/fragments assigned to each feature for each one of your single-cell libraries.

To obtain a matrix of gene counts from your aligned single-cell libraries, run the shell script
`sub_featureCounts.sh` from the terminal, specifying the name of the single-cell library directory to summarize.

```sh
sh sub_featureCounts.sh sequencingRunDir
```
This script calls the PBS script `run_featureCounts.pbs`.

You will need a GTF file containing the features you want to summarize aligned reads to. Refer to [this example](https://dl.dropboxusercontent.com/u/9990581/genes_ercc.gtf), or supply your own annotation file.

In the `run_featureCounts.pbs` file, you must specify the path to the GTF file to use for read summarization.

```sh
#human
annot="/usr/refs/Homo_sapiens/NCBI/build37.2/Annotation/genes_ercc.gtf"
```

This will create a new directory named `/featureCounts_out`, which contains a tab-delimited text file with genes as rows, and columns as single-cell libraries. This matrix is ready to be imported into SCell for quality control and analysis.

## 2. Data Analysis using SCell

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
