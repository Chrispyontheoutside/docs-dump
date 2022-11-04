# GCATemplates
GCATemplates (Genomic Computational Analysis Templates) is a tool developed by TAMU HPRC staff that allows you to copy a Bioinformatics job script template to your current working directory.

You no longer need to load the GCATemplates module, just run the command on one of the HPRC cluster login nodes: gcatemplates

However, if you want to use the assemblathon_stats.pl script, you have to load a new module named [GCATools](/kb3/Software/useful-tools/SW@GCATools/ "wikilink")

Run the following command then follow the menus to find a template script.
```php
 gcatemplates
```

![][image-1]

* The final menu will allow you to copy the template file to your current working directory.
* The template files have default settings for a tool.
* You need to edit the input files and read the manual for available options to use other than defaults.
* You will need to adjust the BSUB parameters as well as variables in the TODO section based on your project.

Below is an example of a template file: run_fastqc_0.11.9_terra.sh_

```php
#!/bin/bash
#SBATCH --export=NONE               # do not export current env to the job
#SBATCH --job-name=fastqc           # job name
#SBATCH --time=01:00:00             # max job run time dd-hh:mm:ss
#SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
#SBATCH --cpus-per-task=2           # CPUs (threads) per command
#SBATCH --mem=12G                   # total memory per node
#SBATCH --output=stdout.%j          # save stdout to file
#SBATCH --error=stderr.%j           # save stderr to file

module load FastQC/0.11.9-Java-11

<<README
    - FASTQC homepage: http://www.bioinformatics.babraham.ac.uk/projects/fastqc
    - FASTQC manual: http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help
README

################################### VARIABLES ##################################
# TODO Edit these variables as needed:

########## INPUTS ##########
pe1_1='/scratch/data/bio/GCATemplates/data/miseq/c_dubliniensis/DR34_R1.fastq.gz'
pe1_2='/scratch/data/bio/GCATemplates/data/miseq/c_dubliniensis/DR34_R2.fastq.gz'

######## PARAMETERS ########
threads=$SLURM_CPUS_PER_TASK

########## OUTPUTS #########
output_dir='./'

################################### COMMANDS ###################################
# use -o <directory> to save results to <directory> instead of directory where reads are located
#   <directory> must already exist before using -o <directory> option
# --nogroup will calculate average at each base instead of bins after the first 50 bp
# fastqc runs one thread per file; using 20 threads for 2 files does not speed up the processing

fastqc -t $threads -o $output_dir $pe1_1 $pe1_2

<<CITATION
    - Acknowledge TAMU HPRC: https://hprc.tamu.edu/research/citations.html

    - FastQC: http://www.bioinformatics.babraham.ac.uk/projects/fastqc
CITATION
```

[image-1]:	https://github.tamu.edu/emmanueljpreciado/HPRCWiki/blob/main/images/gcatemplates.png?raw=true