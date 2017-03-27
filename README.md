## Pipeline to analyze variant SIV->HIV-2 variant datasets

This repository contains the scripts used to quantify and tabulate 
variants in SIV->HIV-2 sequencing datasets as described in:

** TODO: insert reference (DOI) here **


## to run the analysis pipeline on a dataset

This pipeline assumes paired-read fastq files as inputs, e.g. stock_virus_R1.fastq stock_virus_R2.fastq 

To run the pipeline, specify the sample name, for instance run:

`./identify_variants stock_virus`

see identify_variants script for additional detail on the pipeline's steps


### Usage / External dependencies

This pipeline was developed on a server running linux (Ubuntu 14.04) and ought to
work on most typical linux installations.  It requires perl as well as the following
tools:

* cutadapt			http://cutadapt.readthedocs.io/en/stable/guide.html
* cd-hit-est 		http://weizhongli-lab.org/cd-hit/
* bowtie2			http://bowtie-bio.sourceforge.net/bowtie2/index.shtml
* samtools			http://www.htslib.org/
* lofreq			http://csb5.github.io/lofreq/


## to obtain the datasets

To obtain the raw sequence datasets, run the fetch_and_process_datasets script

** TODO: create this script, once datasets in SRA **
