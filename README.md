## Pipeline to analyze variant SIV->HIV-2 variant datasets

This repository contains the scripts used to quantify and tabulate 
variants in SIV->HIV-2 sequencing datasets as described in [this paper](https://doi.org/10.1016/j.virol.2017.07.005)


## to run the analysis pipeline on a dataset

This pipeline assumes paired-read fastq files as inputs, e.g. stock_virus_R1.fastq stock_virus_R2.fastq 

To run the pipeline on a single dataset, specify the sample name. For instance, run:

`./identify_variants stock_virus`

see identify_variants script for additional detail on the pipeline's steps

The 'final' output of this script will be a file named stock_virus_variant_alleles.lofreq.txt [or similar].

This file will contain a table of the variants identified in that dataset relative to the SIV reference sequence.

A number of these variant table files can be merged into a matrix for all variants using the tabulate_variants script, e.g.:

`./tabluate_variants *_variant_alleles.lofreq.txt`


### Usage / External dependencies

This pipeline was developed on a server running linux (Ubuntu 14.04) and ought to
work on most typical linux installations.  It requires perl as well as the following
tools:

* cutadapt			http://cutadapt.readthedocs.io/en/stable/guide.html
* cd-hit-est 		http://weizhongli-lab.org/cd-hit/
* bowtie2			http://bowtie-bio.sourceforge.net/bowtie2/index.shtml
* samtools			http://www.htslib.org/
* lofreq			http://csb5.github.io/lofreq/

## The SIV reference sequence

Can be found in the siv.fa fasta format file.  This corresponds to the consensus sequence of the
stock virus used to infect mice at the beginning of the experiment.  The annotations for this file
are in the Stock_virus_consensus_v1.gff file

## to obtain the datasets

To obtain the raw sequence datasets, run the fetch_and_process_datasets script

**TODO:** create this script, once datasets in SRA 


## Scripts used to create variant frequency plots

These scripts were used to create plots of variant frequencies.  They depend on the PostScript::Simple perl library:

http://search.cpan.org/~mcnewton/PostScript-Simple-0.09/lib/PostScript/Simple.pm

* create_variant_line_plot:     This script plots all variants as a line plot

* create_variant_line_plot_only_increasing:     This script plots only those variants with increasing frequencies


