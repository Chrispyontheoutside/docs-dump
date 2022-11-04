# Genotyping

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## MSG

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

MSG [homepage](http://genomics.princeton.edu/AndolfattoLab/MSG.html)

Multiplexed shotgun genotyping (MSG).

A pipeline of scripts to assign ancestry to genomic segments using
next-gen sequence data. This method can identify recombination
breakpoints in a large number of individuals simultaneously at a
resolution sufficient for most mapping purposes, such as quantitative
trait locus (QTL) mapping and mapping of induced mutations.

First you will need to copy the MSG repository which has already been
downloaded on Ada. The msg latest release v0.4.9 has bugs so use our
copy.

In your working directory where your job script will be located, rsync
the already downloaded msg repo:

    rsync -r /software/hprc/Bio/MSG/f361369/ msg

You can copy the following sample files to your working directory to get
an idea of what input files are needed and their formats and also you
can run the sample job script without any making additional changes.

    cp /software/hprc/Bio/MSG/example_msg_files.tgz ./
    tar xzf example_msg_files.tgz

This is the sample Job Script **run\_msg\_test\_example.sh** from the
sample data (this is for the sample data set, adjust walltime as needed
for your larger data files and update msg.cfg and update.cfg as needed
for your project)

You can run the job script on the sample data without having to make any
additional adjustments

    sbatch run_msg_test_example.sh

This is the example job script run\_msg\_test\_example.sh taken from
running on Ada. If you plan to use MSG on Grace, please contact the HPRC
helpdesk to find the proper modules to load.

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=my_job           # job name
    #SBATCH --time=7-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=48          # CPUs (threads) per command
    #SBATCH --mem=360G                  # total memory per node
    #SBATCH --output=stdout.%x.%j          # save stdout to file
    #SBATCH --error=stderr.%x.%j           # save stderr to file
    
    module load Pyrex/0.9.9-intel-2015B-Python-2.7.10
    module load Stampy/1.0.28-intel-2015B-Python-2.7.10
    module load BWA/0.5.7-intel-2015B
    module load pysam/0.2-intel-2015B-Python-2.7.10-SAMtools-0.1.9
    module load Biopython/1.65-intel-2015B-Python-2.7.10
    module load XZ/5.2.1-intel-2015B
    module load libpng/1.6.21-intel-2015B
    module load libjpeg-turbo/1.4.1-intel-2015B
    module load PCRE/8.38-intel-2015B
    module load Java/1.8.0_92
    module load cURL/7.47.0-intel-2015B
    module load R_tamu/3.3.1-intel-2015B-default-mt
    
    perl msg/msgUpdateParentals.pl
    perl msg/msgCluster.pl
