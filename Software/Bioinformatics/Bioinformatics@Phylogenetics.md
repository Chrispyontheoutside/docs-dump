# Phylogenetics

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## RAxML

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace hybrid-avx
(multinode+multicore)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_raxml_8.2.11_dna_phy_hybrid_avx_multi_node_grace.sh)
[grace mt-avx
(multicore)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_raxml_8.2.11_dna_phy_hybrid_avx_single_node_grace.sh)

RAxML [homepage](https://github.com/stamatak/standard-RAxML)

To see the available versions, type the following on the command line:

` module spider RAxML`

RAxML search algorithm for maximum likelihood based inference of
phylogenetic trees.

## AAF

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_aaf_20171001_grace.sh)

AAF [homepage](https://sourceforge.net/projects/aaf-phylogeny/)

Use the module spider command to see the available versions of AAF:

` module spider AAF`

AAF (alignment and assembly-free) is a free software package that
reconstructs phylogeny from next-generation sequencing data without
assembly and alignment.

It takes raw sequencing reads from each sample altogether and generates
a distance matrix based on the proportion of shared k-mers between each
sample and reconstruct a phylogeny based on the distance matrix.

If you are running aaf\_distance.py with \> 10 cores and the command is
failing with a message like ***IndexError: list index out of range***
then use fewer cores such as -t 5

## IQ-TREE

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

IQ-TREE [homepage](http://www.iqtree.org/)

Efficient phylogenomic software by maximum likelihood

When running using all 20 cores (\#BSUB -n 20) on a 64 GB or 256 GB
node, use the following in your job script:

    module load IQ-TREE/1.5.5-GCCcore-6.3.0
    OMP_NUM_THREADS=20

If you need to run on xlarge nodes (1 TB or 2 TB nodes) and you are
using \#BSUB -n 40 then use the following in your job script:

    module load Westmere
    module load IQ-TREE/1.5.5-GCCcore-6.3.0
    OMP_NUM_THREADS=40

Use the following command to run IQ-TREE

` iqtree-omp`

## BPGA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

BPGA [homepage](http://iicb.res.in/bpga/index.html)

BPGA is an ultra-fast software package that provides comprehensive pan
genome analysis of microorganisms. In addition to all types of routine
pan genomic analyses (Pan genome Profiles, Pan/Core Phylogeny etc.),
BPGA includes a number of novel downstream analysis features like
Exclusive Gene Family Analysis, Atypical GC Content Analysis, Subset
Analysis, MLST based on housekeeping genes and KEGG Distribution etc.

BPGA creates files in the installation directory so you will have to
open the .tar.gz package in your working directory for each project.

You can use the following commands to run BPGA from within your working
directory in your $SCRATCH space.

You can name your working directory anything you want, in this example
it is $SCRATCH/bpga\_project

    module purge
    module load USEARCH/10.0.240-i86linux32
    module load LibTIFF/4.0.7-GCCcore-6.3.0
    module load glibc/2.14
    module load gnuplot/4.6.6-GCCcore-6.3.0-Python-2.7.12-bare
    module load Ghostscript/9.21-GCCcore-6.3.0-Python-2.7.12-bare
    module load Python/2.7.12-intel-2017A
    
    mkdir $SCRATCH/bpga_project
    cd $SCRATCH/bpga_project
    cp /sw/eb/sources/b/BPGA/BPGA-1.3-linux-x86_64-0-0-0.tar.gz ./
    tar xzf BPGA-1.3-linux-x86_64-0-0-0.tar.gz
    cd BPGA-1.3-linux-x86_64-0-0-0/BPGA-Version-1.3/bin
    ln -s $EBROOTUSEARCH/bin/usearch
    chmod +x BPGA-Version-1.3
    ./BPGA-Version-1.3

When running BPGA, it will prompt you for the full path to the directory
that has your input files

## PhyloNetworks

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

PhyloNetworks [homepage](https://github.com/crsl4/PhyloNetworks.jl)

PhyloNetworks is a Julia package for the manipulation, visualization,
inference of phylogenetic networks, and their use for trait evolution.

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

PIECRUSt [homepage](https://github.com/picrust/picrust2/wiki)

PICRUSt2 (Phylogenetic Investigation of Communities by Reconstruction of
Unobserved States) is a software for predicting functional abundances
based only on marker gene sequences.

`# GRACE`  
`module load Anaconda3/2021.05`  
`source activate /sw/hprc/sw/Anaconda3/2021.05/envs/picrust2_2.4.1`

## PhyloSNP

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

PhyloSNP
[homepage](https://hive.biochemistry.gwu.edu/dna.cgi?cmd=phylosnp)

PhyloSNP is designed to take SNP data files (.csv and .vcf) and generate
phylogenetic trees from the provided data.

Additionally, PhyloSNP can either generate a shortened concatenated
genome from the SNPs or generate a concatenated genome from contigs
generated from the SNPs and a specified number of base pairs around each
SNP.

`module load PhyloSNP/20140203-GCC-9.3.0`

PhyloSNP works best with bacterial genomes. For larger genomes or
projects with many samples, use the shrunk-genomes.pl script in the
PhyloSNP module.

## SNPhylo

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

SNPhylo [homepage](https://github.com/thlee/SNPhylo)

SNPhylo, to construct phylogenetic tree based on SNP data. With this
pipeline, user can construct a phylogenetic tree from a file containing
huge SNP data.

`module load SNPhylo/2018.10.05-foss-2020a-Python-2.7.18`

SNPhylo works best with large genomes such as the human genome. Smaller
genomes such as bacterial and fungal genomes probably will not have
enough variants (5000 minimum) after the filtering step.
