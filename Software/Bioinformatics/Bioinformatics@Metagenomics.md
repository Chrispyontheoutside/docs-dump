# Metagenomics

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Mothur

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Mothur [homepage](https://www.mothur.org/)

` module spider Mothur`

Open-source, platform-independent, community-supported software for
describing and comparing microbial communities

See syntax for commands when running in command line mode such as in a
batch file.

<https://mothur.org/wiki/Command_line_mode>

## QIIME

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[terra](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_qiime2_2020.2_demux_dada2_denoise_se_terra.sh)

QIIME is an open-source bioinformatics pipeline for performing
microbiome analysis from raw DNA sequencing data.

Qiime [homepage](http://qiime.org/)

## PICRUSt

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

PICRUSt [homepage](http://picrust.github.io/picrust/)

PICRUSt (pronounced “pie crust”) is a bioinformatics software package
designed to predict metagenome functional content from marker gene
(e.g., 16S rRNA) surveys and full genomes.

`module load PICRUSt/1.1.3-intel-2017A-Python-2.7.12`

If you need to use R with the ape package, you can load the following
R\_tamu version

`module load R_tamu/3.3.2-intel-2017A-Python-2.7.12-default-mt`

PICRUSt2 is available using Anaconda

`module load Anaconda/3-5.0.0.1`  
`source activate picrust2-2.3.0_b`

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

SortMeRNA [homepage](https://bioinfo.lifl.fr/RNA/sortmerna)

Fast filtering, mapping and OTU picking.

SortMeRNA is a program tool for filtering, mapping and OTU-picking NGS
reads in metatranscriptomic and metagenomic data.

    # for Grace
    module purge
    module load Anaconda3/2021.11
    source activate /sw/hprc/sw/Anaconda3/2021.11/envs/sortmerna-4.3.4

## MetaVelvet

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

MetaVelvet [homepage](https://metavelvet.dna.bio.keio.ac.jp/)

` module load MetaVelvet`

A short read assembler for metagenomics

## MetaPhlAn

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_metaphlan3_3.0.14_bowtie2_grace.sh)

MetaPhlAn [homepage](http://huttenhower.sph.harvard.edu/metaphlan),
[tutorial](https://github.com/biobakery/biobakery/wiki/metaphlan3),
[usage](https://github.com/biobakery/MetaPhlAn/wiki/MetaPhlAn-3.0)

` module spider MetaPhlAn/3.0.14-Python-3.8.6`

MetaPhlAn is a computational tool for profiling the composition of
microbial communities from metagenomic shotgun sequencing data.

The MetaPhlAn binaries are located in the following directory:

` ls $EBROOTMETAPHLAN/bin`

## MetaPhlAn2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no (see MetaPhlAn
template)

MetaPhlAn2 [homepage](http://huttenhower.sph.harvard.edu/metaphlan2)

` module load MetaPhlAn2/2.7.8-intel-2017A-Python-2.7.12`

MetaPhlAn2 is a computational tool for profiling the composition of
microbial communities (Bacteria, Archaea, Eukaryotes and Viruses) from
metagenomic shotgun sequencing data with species level resolution. From
version 2.0 MetaPhlAn2 is also able to identify specific strains (in the
not-so-frequent cases in which the sample contains a previously
sequenced strains) and to track strains across samples for all species.

The MetaPhlAn2 utilities are located in the following directory:

` ls $EBROOTMETAPHLAN2/utils`

This is how you use the MetaPhlAn2 provided bacterial profiles with
Bowtie2:

` metaphlan2.py --bowtie2db $EBROOTMETAPHLAN2/db_v20/mpa_v20_m200 --bowtie2_exe $EBROOTBOWTIE2/bin/bowtie2`

## SRST2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_srst2_0.2.0_ada.sh)

SRST2 [homepage](http://katholt.github.io/srst2/)

` module load SRST2`

Molecular Genotyping of Bacterial Pathogens

This program is designed to take Illumina sequence data, a MLST database
and/or a database of gene sequences (e.g. resistance genes, virulence
genes, etc) and report the presence of STs and/or reference genes.

List of MLST databases: [here](http://pubmlst.org/databases/)

You must download the appropriate MLST database prior to running SRST2
using the getmlst.py script provided by SRST2.

Here is an example of downloading the *Salmonella enterica* database on
the UNIX command line in your working directory prior to running SRST2.

**NOTE: you have to run these two commands on the login node command
line and not in a job script because the compute nodes do not have
access to the internet**

    module load SRST2/0.2.0-intel-2015B-Python-2.7.10
    getmlst.py --species "Salmonella enterica"

Read the output from the getmlst.py command to see any recommendations
on running srst2

``` 
  For SRST2, remember to check what separator is being used in this allele database

  Looks like --mlst_delimiter '_'

  >aroC_1  --> -->   ('aroC', '_', '1')

  Suggested srst2 command for use with this MLST database:

    srst2 --output test --input_pe *.fastq.gz --mlst_db Salmonella_enterica.fasta --mlst_definitions senterica.txt --mlst_delimiter '_'
```
