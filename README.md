## Pipeline to analyze variant SIV->HIV-2 variant datasets

This repository contains the scripts used to quantify and tabulate 
variants in SIV->HIV-2 sequencing datasets as described in [this paper](https://doi.org/10.1016/j.virol.2017.07.005) and [this paper](https://www.ncbi.nlm.nih.gov/pubmed/31576587)

The code used for the 2017 paper is in captured in [release v1.0](https://github.com/stenglein-lab/SIV_to_HIV-2/releases/tag/v1.0)

## to run the analysis pipeline on a dataset

This pipeline assumes paired-read fastq files as inputs that are named <dataset_id>_R1.fastq and <dataset_id>_R2.fastq.

e.g.: `SIVsm_stock_virus_R1.fastq SIVsm_stock_virus_R2.fastq`

This pipeline also assume the existence of a bowtie2 index made from the appropriate reference sequence.

The name of this bowtie index will match everything up to the first underscore in the dataset_id.  

So in the above example, the pipeline is expecting the existence of a bowtie2 index named `SIVsm (SIVsm*.bt2)`

See the [build_indexes script](./build_indexes) for an example of a script that creates these indexes.

To run the pipeline on a single dataset, use the [run_variant_pipeline](./run_variant_pipeline) script, passing the dataset name as the single command line argument.  For instance, run:

`./run_variant_pipeline SIVsm_stock_virus`

The final output of this script will be a file named `SIVsm_stock_virus_variant_alleles.lofreq.txt [or similar].`

This file will contain a table of the variants identified in that dataset relative to the virus reference sequence.  This is a tab delimited file that can be imported into R or Excel or other downstream analysis tools.  

A number of these variant table files can be merged into a matrix for all variants using the tabulate_variants script, e.g.:

`./tabluate_variants *_variant_alleles.lofreq.txt`

See [run_tabulate](./run_tabulate)


### Usage / External dependencies

This pipeline was developed on a server running linux (Ubuntu 14.04) and ought to
work on most typical linux installations.  It requires perl as well as the following
tools:

* cutadapt			http://cutadapt.readthedocs.io/en/stable/guide.html
* bowtie2			http://bowtie-bio.sourceforge.net/bowtie2/index.shtml
* samtools			http://www.htslib.org/
* lofreq			   http://csb5.github.io/lofreq/

## The SIV reference sequences used for the above papers

Can be found in the fasta format files in the [reference_sequences](./reference_sequences) directory in this repository.  These correspond to the consensus sequence of the
stock viruses used to infect mice at the beginning of the experiments.  The annotations for this file
are in the associated gff files.


## Scripts used to create variant frequency plots in Schmitt (2017)

These scripts were used to create plots of variant frequencies in the 2017 Schmitt et al paper.  They depend on the PostScript::Simple perl library:

http://search.cpan.org/~mcnewton/PostScript-Simple-0.09/lib/PostScript/Simple.pm

* create_variant_line_plot:     This script plots all variants as a line plot

* create_variant_line_plot_only_increasing:     This script plots only those variants with increasing frequencies


## Integration with viral_variant_explorer

I've developed a Shiny-based tool to visualize these variants, in [this repository](https://github.com/stenglein-lab/viral_variant_explorer)

## Limitations/TODO:

This pipeline could be improved in the following ways:

- This pipeline does not handle indel variants or other structural variants
- This pipeline does not by default handle codons changed by more than one variant, except to warn that multiple variants were detected for a particular codon.  The [analyze_variants script](./analyze_variants) does have a command line option (`-s`) that will output only codons impacted by multiple variants.  The issue is partly related to the next bullet point: the lofreq variant caller does not assess whether single nucleotide variants are linked, so even if 2 or more variants impinge on a single codon, there is no information in the lofreq vcf indicating whether these are linked. 
- This pipeline does not address variant linkage.
