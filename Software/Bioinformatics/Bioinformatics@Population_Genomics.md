# Population Genomics

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Structure

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Structure
[homepage](https://web.stanford.edu/group/pritchardlab/structure.html)

` module spider Structure`

The program structure is a free software package for using multi-locus
genotype data to investigate population structure.

After loading the Structure module, copy the two params files to your
working directory and edit as needed:

    module load Structure/2.3.4-GCCcore-6.3.0
    cp $EBROOTSTRUCTURE/bin/*params ./

### StrAuto

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

StrAuto [manual](https://vc.popgen.org/software/strauto/strauto_doc.pdf)

Automation and Parallelization of STRUCTURE Analysis

StrAuto is the first tool to integrate STRUCTURE analysis with
post-processing using a pipeline approach in addition to implementing
parallel computation – a set up ideal for deployment on computing
clusters.

After loading the StrAuto module, copy the two Structure params files to
your working directory and edit each as needed:

`module spider StrAuto/1.0-GCCcore-8.3.0-Python-2.7.16`  
`cp $EBROOTSTRUCTURE/bin/*params ./`

## Stacks

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(ustacks)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_stacks_1.37_ustacks_ada.sh)

Stacks [homepage](http://catchenlab.life.illinois.edu/stacks/)

` module spider Stacks`

Stacks is a software pipeline for building loci from short-read
sequences, such as those generated on the Illumina platform. Stacks was
developed to work with restriction enzyme-based data, such as RAD-seq,
for the purpose of building genetic maps and conducting population
genomics and phylogeography.

When running Stacks on Ada, be sure to specify the number of threads by
adding the following UNIX environment variable to your job script

` OMP_NUM_THREADS=20`

## ipyrad

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

ipyrad is a toolbox for assembly and analysis of RAD-seq type genomic
data sets. Notably, it has four assembly methods by which to assemble
data: denovo, reference, reference addition, and reference subtraction.

ipyrad is available as an Anaconda environment on Ada:

    module load Anaconda/2-5.0.1
    module load glibc/2.14
    source activate ipyrad_0.7.29

ipyrad latest version on Ada:

    module load Anaconda/3-5.0.0.1
    source activate ipyrad-0.9.15

## PosiGene

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_posigene_0.1_nhsbr_ada.sh)

PosiGene [homepage](https://github.com/gengit/PosiGene)

PosiGene is a tool that (i) detects positively selected genes on
genome-scale, (ii) allows analysis of specific evolutionary branches,
(iii) can be used in arbitrary species contexts and (iv) offers
visualization of the candidates. As data input the program requires only
the coding sequences of your chosen species set in fasta or genbank
format.

`module load PosiGene/0.1-GCCcore-6.3.0-Perl-5.24.0`

## MavericK

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

MavericK is a program for inferring population structure on the basis of
genetic information.

`module load MavericK/1.0.5-GCCcore-6.3.0`

MavericK is a program for inferring population structure on the basis of
genetic information. The mixture modelling framework used by MavericK is
identical to that used in the program STRUCTURE by Pritchard et al.
(2000), which remains one of the most powerful and widely used programs
in population genetics.

You will need to create a parameters.txt and data.txt file as specified
in the MavericK
[manual](http://www.genetics.org/content/genetics/suppl/2016/06/10/genetics.115.180992.DC1/FileS2.pdf).

## OrthoMCL

## POTION

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

POTION [homepage](https://www.lmb.cnptia.embrapa.br/share/POTION/)

-----

***POTION BUG***

A user has identified that the columns for the final\_results.out file
do not match the columns in the positive.out file.

The POTION developer has been notified and the developer has
acknowledged that the columns in the final\_results.out file are out of
order.

    For Example:
       In the file final_results.out there may be 3 P's (in column 2) for model m78
       and 76 P's for m12 (in column 3). However, in the positive.out file it is reversed, there
       are 76 sequences listed for model 8 (m78) and only 3 for model 2 (m12)

-----

POTION (POsitive selecTION) is an open source, modular and end-to-end
software for genomic scale detection of positive Darwinian selection in
groups of homologous coding sequences through estimation of dN/dS
ratios.

`module spider POTION`

POTION requires multiple steps to be run on the command line prior to
running a job script:

    module load POTION/1.1.2-intel-2015B-Perl-5.20.0
    
    rsync -r $EBROOTPOTION/bin ./
    rsync -r $EBROOTPOTION/config_files ./
    
    ln -s $EBROOTPAML/bin/codeml bin/
    ln -s $EBROOTPHYLIP/bin/consense bin/
    ln -s $EBROOTMUSCLE/bin/muscle bin/
    ln -s $EBROOTPHIPACK/bin/Phi bin/
    ln -s $EBROOTPRANK/bin/prank bin/
    ln -s $EBROOTPHYLIP/bin/proml bin/
    ln -s $EBROOTPHYLIP/bin/dnaml bin/
    ln -s $EBROOTPHYLIP/bin/seqboot bin/
    ln -s $EBROOTTRIMAL/bin/trimal bin/
    ln -s $EBROOTMAFFT/bin/mafft bin/
    ln -s $EBROOTPAGAN/bin/pagan bin/
    ln -s $EBROOTPHYML/bin/phyml bin/
    
    cp ./config_files/dummy_potion_user_config_file_site_standard my_config_file

Edit the following variables in your my\_config\_file:

    CDS_dir_path = /path/to/CDS                         # path to folder containing CDS data; you create the CDS directory and put your data there
    homology_file_path = /path/to/all_orthomcl.out      # path to the ORTHOMCL 1.4 main output file
    project_dir_path = /path/to/potion_results_out      # path to the main directory where results will be created.Parent directory must exist.
    max_processors
    multiple_alignment
    phylogenetic_tree

Then edit only the **potion\_dir** variable in the
**./config\_files/potion\_config** file and set it to the full path of
your current working directory

    potion_dir = $EBROOTPOTION/           # change this to the full path of your working directory

OrthoMCL version 1.4 is required if generating the all\_orthomcl.out
input file for POTION.

Sample job script run from your working directory:

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=my_job           # job name
    #SBATCH --time=7-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=48          # CPUs (threads) per command
    #SBATCH --mem=360G                  # total memory per node
    #SBATCH --output=stdout.%j          # save stdout to file
    #SBATCH --error=stderr.%j           # save stderr to file
    
    module load POTION/1.1.2
    
    ./bin/potion.pl --conf_file_path /absolute/pato/to/working/directory/my_config_file
