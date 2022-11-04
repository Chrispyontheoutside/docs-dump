# Chromatin Structure

## Juicer
[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/) available: no

[Juicer homepage](https://github.com/aidenlab/juicer)

Juicer is a pipeline for generating Hi-C maps from fastq raw data files and command line tools for feature annotation on the Hi-C maps.

Hi-C is a genome-wide Chromatin Conformation Capture protocol using proximity ligation.

## Terra CPU version
The CPU version is for running on a single GPU compute node.

The first steps (bwa, dedup, merge, hic files) are run on the compute node's CPU and the postproc step is run on the GPU.

1. Load the CPU version of Juicer and set up your directories before submitting your job script


        module load Juicer/1.5.6-intel-2016b-Java-1.8.0-CUDA-8.0.44-CPU


2. Copy the Juicer scripts directory to your working directory.

        cp -r $EBROOTJUICER/CPU/scripts/ ./

3. Create a directory in your working directory named fastq that contains all your fastq files.

        mkdir fastq

4. Then you will need references and restriction_sites directories in your working directory.

    There are some references available which you can use by doing the following:

        ln -s /scratch/datasets/bio/Juicer/references
        ln -s /scratch/datasets/bio/Juicer/restriction_sites

5. You job script should be in the same directory as your scripts/ fastq/ references/ and restriction_sites/ directories

    By default, Juicer will use 28 threads for bwa so configure the #SBATCH parameters for 28 threads unless you want to specify fewer with the jucier.sh -t option

        #!/bin/bash
        #SBATCH --export=NONE                # do not export current env to the job
        #SBATCH --job-name=juicer_cpu        # set job name
        #SBATCH --time=1-00:00:00            # set the wall clock limit to 1 day
        #SBATCH --nodes=1                    # request one node
        #SBATCH --cpus-per-task=28           # Each task uses 28 cores
        #SBATCH --mem=112G                   # request 112GB total job memory
        #SBATCH --gres=gpu:1                 # request 1 GPU per node can be 1 or 2
        #SBATCH --partition=gpu              # request the GPU partition/queue
        #SBATCH --output=stdout.%x.%j
        #SBATCH --error=stderr.%x.%j


        module load Juicer/1.5.6-intel-2016b-Java-1.8.0-CUDA-8.0.44-CPU

        ./scripts/juicer.sh

