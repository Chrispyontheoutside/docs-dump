[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

# Job Scripts

## Configuring

### Should I use one core or multiple cores?

`* Check with the software that you want to use and see if it supports multiple cores. If it supports multiple cores and there are no recommendations to use a max number of cores, then you should request all cores on a compute node and specify number of cores at the software command option.`  
`   * GeneMark has been reported to fail with >48 cores`  
`   * Trinity inchworm best with 6 cores: --inchworm_cpu 6`  
`* If you request all the cores on a compute node, then it is good practice to also request all the available memory since your job will be the only job running on the compute node and you may end up needing all the memory.`

### How do I request all the cores and all the memory on a single compute node?

The parameters are different for nodes with different amounts of total
available memory.

Generally you request the max available memory minus 10 GB to account
for the operating system image on the compute node.

#### Grace

##### For a 384 GB memory Grace compute node

Up to max 7 days runtime

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=my_job           # job name
    #SBATCH --time=7-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=48          # CPUs (threads) per command
    #SBATCH --mem=360G                  # total memory per node
    #SBATCH --output=stdout.%x.%j       # save stdout to file
    #SBATCH --error=stderr.%x.%j        # save stderr to file

Up to max 21 days runtime

`#!/bin/bash`  
`#SBATCH --export=NONE               # do not export current env to the job`  
`#SBATCH --job-name=my_job           # job name`  
`#SBATCH --time=21-00:00:00          # max job run time dd-hh:mm:ss`  
**`#SBATCH 
 --partition=xlong`**`           # partition used for jobs 7 to 21 days`  
`#SBATCH --ntasks-per-node=1         # tasks (commands) per compute node`  
`#SBATCH --cpus-per-task=48          # CPUs (threads) per command`  
`#SBATCH --mem=360G                  # total memory per node`  
`#SBATCH --output=stdout.%x.%j       # save stdout to file`  
`#SBATCH --error=stderr.%x.%j        # save stderr to file`

##### For a 3 TB memory Grace compute node

`#!/bin/bash`  
`#SBATCH --export=NONE               # do not export current env to the job`  
`#SBATCH --job-name=my_job           # job name`  
`#SBATCH --time=2-00:00:00           # max job run time dd-hh:mm:ss`  
**`#SBATCH 
 --partition=bigmem`**`          # use large (3TB) memory node       `  
`#SBATCH --ntasks-per-node=1         # tasks (commands) per compute node`  
`#SBATCH --cpus-per-task=80          # CPUs (threads) per command`  
`#SBATCH --mem=2929G                 # total memory per node`  
`#SBATCH --output=stdout.%x.%j       # save stdout to file`  
`#SBATCH --error=stderr.%x.%j        # save stderr to file`

##### For a A100 GPU 384 GB memory Grace compute node

**Request 1 GPU**

`#!/bin/bash`  
`#SBATCH --export=NONE               # do not export current env to the job`  
`#SBATCH --job-name=my_job           # job name`  
`#SBATCH --time=1-00:00:00           # max job run time dd-hh:mm:ss`  
`#SBATCH --ntasks-per-node=1         # tasks (commands) per compute node`  
`#SBATCH --cpus-per-task=24          # CPUs (threads) per command`  
`#SBATCH --mem=180G                  # total memory per node`  
**`#SBATCH   --gres=gpu:a100:1`**`           # request 1 GPU`  
`#SBATCH --output=stdout.%x.%j       # save stdout to file`  
`#SBATCH --error=stderr.%x.%j        # save stderr to file`

**Request 2 GPUs**

`#!/bin/bash`  
`#SBATCH --export=NONE               # do not export current env to the job`  
`#SBATCH --job-name=my_job           # job name`  
`#SBATCH --time=1-00:00:00           # max job run time dd-hh:mm:ss`  
`#SBATCH --ntasks-per-node=1         # tasks (commands) per compute node`  
`#SBATCH --cpus-per-task=48          # CPUs (threads) per command`  
`#SBATCH --mem=360G                  # total memory per node`  
**`#SBATCH   --gres=gpu:a100:2`**`           # request 2 GPUs`  
`#SBATCH --output=stdout.%x.%j       # save stdout to file`  
`#SBATCH --error=stderr.%x.%j        # save stderr to file`

#### Terra

##### For a 64 GB memory Terra compute node

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=job_name
    #SBATCH --time=7-00:00:00
    #SBATCH --ntasks-per-node=1
    #SBATCH --cpus-per-task=28
    #SBATCH --mem=56G
    #SBATCH --output=stdout.%x.%j
    #SBATCH --error=stderr.%x.%j

##### For a 96 GB memory KNL Terra compute node

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=job_name
    #SBATCH --time=7-00:00:00
    #SBATCH --ntasks-per-node=1
    #SBATCH --cpus-per-task=68
    #SBATCH --mem=80G
    #SBATCH --output=stdout.%x.%j
    #SBATCH --error=stderr.%x.%j
    #SBATCH --partition=knl

##### For a 128 GB memory Terra compute node

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=job_name
    #SBATCH --time=2-00:00:00
    #SBATCH --ntasks-per-node=1
    #SBATCH --cpus-per-task=28
    #SBATCH --mem=112G
    #SBATCH --output=stdout.%x.%j
    #SBATCH --error=stderr.%x.%j

### How do I find compatible software modules?

#### Grace

##### Example 1

`# first start with a new terminal session or run module purge`  
**`module   purge`**  
  
`# search for a software module for stacks`  
**`module   spider   stacks`**` `  
  
`# you will see that there are multiple versions`  
`    Versions:`  
`       Stacks/1.48`  
`       Stacks/2.3e`  
`       Stacks/2.41`  
`       Stacks/2.53`  
`       Stacks/2.55`  
  
`# run module spider on the latest version`  
**`module   spider   Stacks/2.55`**  
  
`# you will see that you have to load other modules prior to loading Stacks/2.55`  
` You will need to load all module(s) on any one of the lines below before the "Stacks/2.55" module is available to load.`  
  
`     GCC/9.3.0  OpenMPI/4.0.3`  
  
`# load the two prerequisite modules then the Stacks/2.55 module`  
**`module   load   GCC/9.3.0   OpenMPI/4.0.3 
 Stacks/2.55`**  
  
`# now search for available compatible samtools modules that are compatible with the Stacks/2.55 module you just loaded`  
**`module   avail   samtools`**  
  
`# you will notice that there is one version available since you already loaded the prerequisite modules`  
`----- /sw/eb/mods/all/Compiler/GCC/9.3.0 -----`  
`SAMtools/1.10`  
  
`# load the compatible samtools module`  
**`module   load   SAMtools/1.10`**

##### Example 2

`# first start with a new terminal session or run module purge`  
**`module   purge`**  
  
`# search for a software module for minimap2`  
**`module   spider   minimap2`**` `  
  
`# you will see that there are multiple versions`  
`   Versions:`  
`       minimap2/2.13`  
`       minimap2/2.17`  
`       minimap2/2.18`  
`       minimap2/2.23`  
  
`# select the version you want to use and run module spider`  
**`module   spider   minimap2/2.23`**  
  
`# you will see that you have to load another module prior to loading minimap2/2.23`  
`   You will need to load all module(s) on any one of the lines below before the "minimap2/2.23" module is available to load.`  
  
`     GCCcore/10.3.0`  
  
`# load the GCCcore/10.3.0 module then the minimap2/2.23 module`  
**`module   load   GCCcore/10.3.0   minimap2/2.23`**  
  
`# now search for available samtools modules that are compatible with the minimap2/2.23 module you just loaded`  
**`module   avail   samtools`**  
  
`# you will notice that there are not any compatible samtools modules`  
`No module(s) or extension(s) found!`  
  
`# load the parent module of GCCcore/10.3.0 which is GCC/10.3.0`  
**`module   load   GCC/10.3.0`**` `  
  
`# now search again for available compatible samtools modules`  
**`module   avail   samtools`**  
  
`# now there is a compatible samtools module available`  
`----- /sw/eb/mods/all/Compiler/GCC/10.3.0 -----`  
`  SAMtools/1.12`  
  
`# load the compatible samtools module`  
**`module   load   SAMtools/1.12`**

##### Example 3

`# first start with a new terminal session or run module purge`  
**`module   purge`**  
  
`# search for a software module for stacks`  
**`module   spider   samtools`**` `  
  
`# you will see that there are multiple versions`  
`     Versions:`  
`       SAMtools/0.1.16`  
`       SAMtools/0.1.20`  
`       SAMtools/1.9`  
`       SAMtools/1.10`  
`       SAMtools/1.11`  
`       SAMtools/1.12`  
  
`# select the version you want to use and run module spider`  
**`module   spider   SAMtools/1.12`**  
  
`# you will see that you have to load another module prior to loading SAMtools/1.12`  
`You will need to load all module(s) on any one of the lines below before the "SAMtools/1.12" module is available to load.`  
  
`     GCC/10.3.0`  
  
`# load the GCC/10.3.0 module then the SAMtools/1.12 module`  
**`module   load   GCC/10.3.0   SAMtools/1.12`**  
  
`# now search for available stacks modules that are compatible with the SAMtools/1.12 module you just loaded`  
**`module   avail   stacks`**  
  
`# you will notice that there are no compatible Stacks modules`  
`No module(s) or extension(s) found!`  
  
`# run module spider to see what Stacks modules are on the cluster`  
**`module   spider   stacks`**  
  
`# you will see that there are multiple versions`  
`    Versions:`  
`       Stacks/1.48`  
`       Stacks/2.3e`  
`       Stacks/2.41`  
`       Stacks/2.53`  
`       Stacks/2.55`  
  
`# see what needs to be loaded to use the latest version of Stacks`  
**`module   spider   Stacks/2.55`**  
  
`# you will see that you have to load a different module (9.3.0 instead of 10.3.0) prior to loading Stacks/2.55`  
`You will need to load all module(s) on any one of the lines below before the "Stacks/2.55" module is available to load.`  
  
`     GCC/9.3.0  OpenMPI/4.0.3`  
  
`# see what modules have already been loaded`  
**`module   list`**  
  
`# you will see what dependency modules have been automatically loaded in addition to the two you previously loaded`  
`Currently Loaded Modules:`  
` 1) GCCcore/10.3.0   3) binutils/2.36.1   5) ncurses/6.2   7) XZ/5.2.5      9) cURL/7.76.0`  
` 2) zlib/1.2.11      4) GCC/10.3.0        6) bzip2/1.0.8   8) OpenSSL/1.1  10) SAMtools/1.12`  
  
`# notice that we have `**`GCCcore`**`/10.3.0 loaded but not GCC/9.3.0. If Stacks/2.55 required `**`GCC`**`/10.3.0 we could load GCC/10.3.0 and OpenMPI/4.1.1 and do module avail again but since it is 9.3.0 you have a few options`  
`# 1. look to see if a newer version of Stacks is available and request the latest version installed to match the Samtools GCCcore/10.3.0 toolchain`  
`# 2. start by loading the Stacks module then repeat steps necessary for finding compatible Samtools modules.`  
**`module   purge`**  
**`module   load   GCC/9.3.0   OpenMPI/4.0.3 
 Stacks/2.55`**  
**`module   avail   samtools`**  
  
`# now there is a compatible samtools module available`  
`----- /sw/eb/mods/all/Compiler/GCC/9.3.0 -----`  
`  SAMtools/1.10`  
  
**`module   load   SAMtools/1.10`**

### Should I use one compute node or multiple compute nodes?

`This is highly dependent on the software. Most bioinformatics software will only require one node. `  
`Example of times when you could use multiple compute nodes:`  
`* The software has MPI support for running a command across multiple nodes (ABySS)`  
`* You have hundreds or thousands of individual commands to run. (`[`TAMULauncher`](/kb3/Software/tamulauncher/SW@tamulauncher/)`/)`  
`* You have multiple samples to run and can run one sample per compute node in a `[`job 
 array`](/kb3/Software/Bioinformatics/Bioinformatics@FAQ/#terra-job-array/)` using all cores and memory on each compute node.`

### Are the Terra KNL nodes as fast as the 64GB nodes?

    * Even though there are 72 cores on the KNL nodes, the speed of each core is 1.5GHz while the 64GB nodes are at 2.4GHz.
    
    * A test alignment of human sequences to GRCh38 took 5 days on a 64GB node using all 28 cores. The same job script did not complete before the KNL queue limit of 7 days using all 72 cores.

### Do I use a Job Array or TAMULauncher

TAMULauncher is good for commands that use one or a few cores. It is
also good if your job ends due to reaching the walltime limit because
TAMULauncher can start from the last uncompleted commands where you will
have to reconfigure a job array as to not redo already completed
commands. In most cases, TAMULauncher is recommended over a job array.

TAMULauncher can run one command per CPU core while a job array can only
run one command per compute node.

If each command uses an entire node, you can configure your job as a job
array.

If your commands use any redirection operators such as \< \> | \<\< \>\>
then use TAMULauncher instead of an job array.

The commands.txt file you generate is the same for a TAMULauncher job
and a job array.

#### How do I configure and run a TAMULauncher Job?

Here is an example script for TAMULauncher and a required commands file.
You need a file that has one command per line. Each line may have
multiple commands joined with a semicolon.

    blastn -query chunk0000.fa -db /scratch/datasets/blast/nt.bacteria -task megablast -out chunk0000.fa.out -outfmt 6
    blastn -query chunk0001.fa -db /scratch/datasets/blast/nt.bacteria -task megablast -out chunk0001.fa.out -outfmt 6
    blastn -query chunk0002.fa -db /scratch/datasets/blast/nt.bacteria -task megablast -out chunk0002.fa.out -outfmt 6
    blastn -query chunk0003.fa -db /scratch/datasets/blast/nt.bacteria -task megablast -out chunk0003.fa.out -outfmt 6

Here is the example job script for Terra. The default for tamulauncher
is to run one command per CPU core but you can use more cores per
process. In the following example, there are 5 nodes total each having 7
commands (tasks) with each command using 4 cores each.

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=blast        # job name
    #SBATCH --time=7-00:00:00       # max job run time
    #SBATCH --nodes=5               # use 5 nodes max
    #SBATCH --ntasks-per-node=7     # tasks (commands) per compute node
    #SBATCH --cpus-per-task=4       # CPUs (threads) per command
    #SBATCH --mem=56G               # total memory
    #SBATCH --output=stdout.%x.%j      # save stdout to file
    #SBATCH --error=stderr.%x.%j       # save stderr to file
    
    module load BLAST+/2.8.1-intel-2017A-Python-2.7.12
    
    tamulauncher commands.txt

Here is an example of using multiple commands on a single line.

  - In this example, each line will be run on one entire compute node
    using 20 cores per node.
  - You can specify more cores per process using the --commands-pernode
    option.
  - Only one of many lines is showed for better viewing but you would
    generally have many commands in the commands.txt file.
  - Each line in the example runs multiple commands per sample which are
    joined with a semicolon.
  - Notice with bwa and tamulauncher you need to use \\\\t instead of
    \\t for the read group value.
  - Also notice the use of the $TMPDIR for temporary files and in this
    example, the bam\_files directory needs to be created first.

<!-- end list -->

    bwa mem -R "@RG\\tID:ERR551981\\tSM:282set_CML220\\tLB:CML220_HADTMADXX\\tPL:ILLUMINA" -t 20 m_tuberculosis_uid185758.fna ERR551981_pe_1_trimmo.fastq.gz ERR551981_pe_2_trimmo.fastq.gz > $TMPDIR/ERR551981.sam; samtools sort -n -O bam -T $TMPDIR/nsorted $TMPDIR/ERR551981.sam -o $TMPDIR/nsorted_ERR551981.bam ; samtools fixmate -O bam $TMPDIR/nsorted_ERR551981.bam $TMPDIR/ncleaned_ERR551981.bam; samtools sort -O bam -T $TMPDIR/csorted $TMPDIR/ncleaned_ERR551981.bam -o bam_files/coord_sortedERR551981_1.bam

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=bwa          # job name
    #SBATCH --time=7-00:00:00       # max job run time
    #SBATCH --nodes=10              # use 10 nodes max
    #SBATCH --ntasks-per-node=1     # tasks (commands) per compute node
    #SBATCH --cpus-per-task=28      # CPUs (threads) per command
    #SBATCH --mem=56G               # total memory
    #SBATCH --output=stdout.%x.%j      # save stdout to file
    #SBATCH --error=stderr.%x.%j       # save stderr to file
    
    module load BLAST+/2.8.1-intel-2017A-Python-2.7.12
    
    tamulauncher --commands-pernode 1 commands.txt

#### How do I configure and run a Job Array?

##### Terra job array

Here is an example Slurm job script of running a job array using a
maximum of 10 compute nodes when you have a commands.txt file that
contains 10 or more lines where each line is a command or commands
joined with semicolons and each command uses all CPU cores on a compute
node.

The sed command uses the $SLURM\_ARRAY\_TASK\_ID to select the command
on a line number of the commands.txt file

    #!/bin/bash
    #SBATCH --export=NONE               # do not propagate environment; do not change
    #SBATCH --job-name=spades_job_array # job name
    #SBATCH --time=1:00:00              # set the wall clock limit to 1 hour
    #SBATCH --ntasks-per-node=1         # request 1 task (command) per node
    #SBATCH --cpus-per-task=28          # request 28 cpus (cores) per task
    #SBATCH --mem=56G                   # request 56GB of memory per node
    #SBATCH --array=1-10                # request a job array with a max of 10 compute nodes
    #SBATCH --output=stdout.%A_%a       # create file for stdout
    #SBATCH --error=stderr.%A_%a        # create file for stderr
    
    module load SPAdes/3.13.0-Linux
    
    # run one of the 10 commands on each job array node
    command=$(sed -n ${SLURM_ARRAY_TASK_ID}p commands.txt)
    $command

#### Create a file of commands for tamulauncher or parallel

If you have hundreds of commands to run and each requires paired end
files then you can use bash commands to create a file of commands to use
with tamulauncher or parallel.

The main advantages of tamulauncher over parallel is that if your job
runs out of walltime, you can restart from after the last completed
command and you can check the status of the number of commands
completed.

##### Outside the reads directory

If you have many files with the following names in a directory other
than your working directory:

    reads/SAMPLE_1_R1.fastq.gz
    reads/SAMPLE_1_R2.fastq.gz
    reads/SAMPLE_2_R1.fastq.gz
    reads/SAMPLE_2_R2.fastq.gz
    reads/SAMPLE_3_R1.fastq.gz
    reads/SAMPLE_3_R2.fastq.gz
    reads/SAMPLE_4_R1.fastq.gz
    reads/SAMPLE_4_R2.fastq.gz

Start by selecting only R1 files in order to get the sample names.

Type in the following lines and study the results in order to see how to
use the basename command and trim off parts of files in order to get
sample names from the file names:

    file='reads/SAMPLE_1_R1.fastq.gz'
    echo ${file/_R1.fastq.gz}                 # removes _R1.fastq.gz from the end of the value in the $file variable
    echo ${file/R1/R2}                        # replaces R1 with R2 in the $file variable
    echo $(basename ${file/_R1.fastq.gz})     # removes directory path and removes _R1.fastq.gz from the end of the $file variable 

You can capture each sample name in the directory from the first paired
file to create your commands to use for spades.py, trimmomatic or other
command.

    for sample in reads/*R1.fastq.gz; do echo $(basename ${sample/_R1.fastq.gz}); done

Then use the sample names to create a commands file

    for sample in reads/*R1.fastq.gz; do echo spades.py --threads 20 --tmp-dir \$TMPDIR --careful --memory 54 -o $(basename ${sample/_R1.fastq.gz}) --pe1-1 $sample --pe1-2 ${sample/R1/R2}; done > spades_commands.txt

(Notice how using \\$TMPDIR in the for loop will print $TMPDIR to the
output file)

The resulting spades\_command.txt file will look like this:

    spades.py --threads 20 --tmp-dir $TMPDIR --careful --memory 54 -o SAMPLE_1 --pe1-1 reads/SAMPLE_1_R1.fastq.gz --pe1-2 reads/SAMPLE_1_R2.fastq.gz
    spades.py --threads 20 --tmp-dir $TMPDIR --careful --memory 54 -o SAMPLE_2 --pe1-1 reads/SAMPLE_2_R1.fastq.gz --pe1-2 reads/SAMPLE_2_R2.fastq.gz
    spades.py --threads 20 --tmp-dir $TMPDIR --careful --memory 54 -o SAMPLE_3 --pe1-1 reads/SAMPLE_3_R1.fastq.gz --pe1-2 reads/SAMPLE_3_R2.fastq.gz
    spades.py --threads 20 --tmp-dir $TMPDIR --careful --memory 54 -o SAMPLE_4 --pe1-1 reads/SAMPLE_4_R1.fastq.gz --pe1-2 reads/SAMPLE_4_R2.fastq.gz

Since each spades command can use 20 cores, you can run these commands
as an array job instead of using TAMULauncher.

##### Within the reads directory

This example uses a different approach for parsing file names to capture
a sample name where the part of the file name to remove is different for
each sample. If you have many files with the following names in your
current working directory, for example, and you only want to use the
paired end reads (those with 1P and 2P)

    A45CEB2_S1_1P.fastq.gz
    A45CEB2_S1_1U.fastq.gz
    A45CEB2_S1_2P.fastq.gz
    A45CEB2_S1_2U.fastq.gz
    A49HEB1_S5_1P.fastq.gz
    A49HEB1_S5_1U.fastq.gz
    A49HEB1_S5_2P.fastq.gz
    A49HEB1_S5_2U.fastq.gz

Then you can capture the sample names from the first paired file and
create your command such as spades.py, trimmomatic or other command.

Here is a summary on using \#, \#\#, %, %%, \* to get a substring of a
bash variable

    ${var#*SubStr}     # will drop beginning of string up to first occurrence of 'SubStr'
    ${var##*SubStr}    # will drop beginning of string up to last occurrence of 'SubStr'
    ${var%SubStr*}     # will drop part of string from last occurrence of 'SubStr' to the end
    ${var%%SubStr*}    # will drop part of string from first occurrence of 'SubStr' to the end

Run the following UNIX commands in the same directory as the fastq.gz
files for this example.

Steps 1 and 2 are trial and error until you get the part of the filename
that is the sample name.

1\. get the names of pair one reads in order to obtain the sample name

    for sample in *1P.fastq.gz; do echo $sample; done
    
    OUTPUT:
    A45CEB2_S1_1P.fastq.gz
    A49HEB1_S5_1P.fastq.gz

2\. chop off the parts of the file name in order to get the sample name

    for sample in *1P.fastq.gz; do echo ${sample%_*}; done
    
    OUTPUT:
    A45CEB2_S1
    A49HEB1_S5

3\. test printing out the two sample names

    for sample in *1P.fastq.gz; do echo "${sample%_*}_1P.fastq.gz ${sample%_*}_2P.fastq.gz"; done
    
    OUTPUT:
    A45CEB2_S1_1P.fastq.gz A45CEB2_S1_2P.fastq.gz
    A49HEB1_S5_1P.fastq.gz A49HEB1_S5_2P.fastq.gz

4\. create the entire spades command for each sample using what you did
in step 3

    for sample in *1P.fastq.gz; do echo "spades.py --careful --memory 24 --threads 1 -1 \$SCRATCH/data/${sample%_*}_1P.fastq.gz -2 \$SCRATCH/data/${sample%_*}_2P.fastq.gz -o spades_${sample%_*}"; done > ../spades_commands.txt

The resulting spades\_command.txt file will look like this:

    spades.py --careful --memory 24 --threads 1 -1 $SCRATCH/data/A45CEB2_S1_1P.fastq.gz -2 $SCRATCH/data/A45CEB2_S1_2P.fastq.gz -o spades_A45CEB2_S1
    spades.py --careful --memory 24 --threads 1 -1 $SCRATCH/data/A49HEB1_S5_1P.fastq.gz -2 $SCRATCH/data/A49HEB1_S5_2P.fastq.gz -o spades_A49HEB1_S5

### Are there any example job scripts for bioinformatics tools?

`We have many example job scripts available for various bioinformatics tasks in the `[`GCATemplates`](/kb3/Software/useful-tools/SW@GCATemplates/)` module`

### How much walltime (\#SBATCH --time) should I use?

    If you are unsure about how much walltime to specify, you should specify the maximum allowed by the batch queues. Then when the job is complete, you can see how long it took to finish a job with your data using the 'seff jobid' command and you can adjust similar scripts accordingly. If a job that you had reserved 7 days (#SBATCH --time=7-00:00:00) finishes in 2 days then you can schedule similar jobs for 3 days just to allow more time if needed.

### How much memory did my job use and how long did it run?

Run the 'seff jobid' command and check memory efficiency and memory
utilized

    seff 3402830
    
    Job ID: 3402830
    Cluster: terra
    User/Group: netid/netid
    State: COMPLETED (exit code 0)
    Nodes: 1
    Cores per node: 28
    CPU Utilized: 05:15:41
    CPU Efficiency: 10.91% of 2-00:12:52 core-walltime
    Job Wall-clock time: 01:43:19
    Memory Utilized: 6.77 GB
    Memory Efficiency: 12.53% of 54.00 GB

Alternatively, you can look in the MaxRSS column in the batch row of the
following sacct command to see the max memory used by a job. Units are
Kb:

`sacct --format user,jobid,jobname,partition,nodelist,maxrss,maxdiskwrite,state%20,exitcode,alloctres%36 -j JOBID`

You can also see the total runtime and SUs charged per job with the
myproject command:

`myproject -j all`

## Running

#### Monitor resource usage for a running job

If you need to monitor the GPU or CPU utilization for a running job, you
can start a second job on the same compute node as the previously
running job in order to access the compute node and run job monitoring
tools like **top** for CPU usage and **nvidia-smi** for GPU usage.

Leave at least one core and 1GB available in your initial job in order
to launch a monitoring job on the same node.

Get the compute node name for the currently running job

`squeue -u $USER`

Look at the NODELIST column to see the compute node name.

Then start a second job from the login node command line requesting the
compute node name found in the NODELIST column (**c127** in the example
below) for the running job you want to monitor.

`srun --nodelist `**`c127`**` --time 01:00:00 --mem 1G --pty bash`

Once the interactive job starts, you will see the prompt change to
include the hostname as: **c127**

Run the following command to monitor CPU utilization (type **q** to stop
the top command)

`top -u $USER`

Run the following command to monitor GPU utilization (type CTRL+c to
exit)

`watch nvidia-smi`

Example output for nvidia-smi showing 31% GPU utilization for GPU 0 and
29% GPU utilization for GPU 1.

Also look at the Processes section to see what command is running on
which GPU to help identify your GPU if using only one GPU.

`Fri Sep  3 15:54:06 2021`  
`+-----------------------------------------------------------------------------+`  
`| NVIDIA-SMI 470.57.02    Driver Version: 470.57.02    CUDA Version: 11.4     |`  
`|-------------------------------+----------------------+----------------------+`  
`| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |`  
`| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |`  
`|                               |                      |               MIG M. |`  
`|===============================+======================+======================|`  
`|   `**`0`**`  Quadro RTX 6000     On   | 00000000:3B:00.0 Off |                  Off |`  
`| N/A   36C    P0    58W / 250W |   3607MiB / 24222MiB |     `**`31%`**`      Default |`  
`|                               |                      |                  N/A |`  
`+-------------------------------+----------------------+----------------------+`  
`|   `**`1`**`  Quadro RTX 6000     On   | 00000000:D8:00.0 Off |                  Off |`  
`| N/A   35C    P0    57W / 250W |   2142MiB / 24222MiB |     `**`29%`**`      Default |`  
`|                               |                      |                  N/A |`  
`+-------------------------------+----------------------+----------------------+  `  
  
`+-----------------------------------------------------------------------------+`  
`| Processes:                                                                  |`  
`|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |`  
`|        ID   ID                                                   Usage      |`  
`|=============================================================================|`  
`|    0   N/A  N/A     35322      G   /usr/bin/X                         38MiB |`  
`|    0   N/A  N/A    221139      C   julia                            3565MiB |`  
`|    1   N/A  N/A     35322      G   /usr/bin/X                         13MiB |`  
`|    1   N/A  N/A    222466      C   julia                            2125MiB |`  
`+-----------------------------------------------------------------------------+`

#### R code

Use the RScript command to run R code (mycommands.R in the following
example) in a job script. The job script and your R commands file should
be in the same directory.

    module load R_tamu/3.6.0-foss-2018b-recommended-mt
    
    Rscript mycommands.R

## Debugging

### How do I know if my job completed successfully?

#### Successfully completed

Look for the line in the 'seff jobid' command output that says 'State:
COMPLETED (exit code 0)'. However, this just means that the job script
finished without any errors but you should always check the format of
any output files.

#### Insufficent walltime

In the following example, the job ran out of walltime and used 32% of
the requested 180GB of memory:

    Job ID: 1234567
    Cluster: grace
    User/Group: netid/netid
    State: TIMEOUT (exit code 0)
    Nodes: 1
    Cores per node: 24
    CPU Utilized: 05:56:02
    CPU Efficiency: 2.06% of 12-00:09:12 core-walltime
    Job Wall-clock time: 12:00:23
    Memory Utilized: 57.85 GB
    Memory Efficiency: 32.14% of 180.00 GB

#### Insufficent memory

If your job failed and you see seff output like the following, then
increase the amount of requested memory in the \#SBATCH parameters and
run the job again.

    Memory Utilized: 179.85 GB
    Memory Efficiency: 99.91% of 180.00 GB

#### system terminated job

If you see the following line, then you may have reached your disk or
file quota.

`The cluster DRM system terminated this job`

Run the showquota command to see your quotas and send a request to the
HPRC helpdesk if you need to increase your quotas.

`showquota`

Remember to delete any unwanted or temporary files or tar.gz a project
when complete in order to free up disk space and file counts.

# Interactive Jobs

## srun

You can run an interactive job which will run on a compute node. You can
do this from the command line on a login node. The job will end once you
exit or close the terminal or when the walltime ends.

Use srun to start an interactive job. Once the job starts, the prompt
will change to the compute node name like **c697**

`srun --time=1-00:00:00 --mem=7G --ntasks=1 --cpus-per-task=1 --pty bash`

Increase the mem and cpus-per-task values as needed.

## VNC

The VNC portal app will run an interactive job that you can log out and
come back later to contine where you left off.

See the HPRC [video](https://www.youtube.com/watch?v=ORxFJVSZSyc) on how
to launch a VNC job.

# Singularity sandbox

You can build a sandbox directory from a .sif file. The sandbox
directory will allow you to install/rebuild software that doesn't
require root privileges. Create the sandbox somewhere in your $SCRATCH
directory where you have at least 60,000 files available in your scratch
file quota.

1). start a Slurm interactive session which will create a job and launch
a terminal on a compute node

**`srun   --time=1-00:00:00   --mem=60G   --ntasks=1 
 --cpus-per-task=8   --pty   bash`**

2). during the interactive session on the compute node, create a sandbox
directory from a .sif file.

**`cd   $SCRATCH`**  
`singularity build --sandbox my_gem5_sandbox_dir /sw/hprc/sw/containers/gem5-v21.2.1.0-04292022.sif `

 3). start a singularity interactive shell in order to edit files and
rebuild software

` singularity shell --writable my_gem5_sandbox_dir`

 Optional: you can mount a directory in your $SCRATCH to a directory
inside the image using the -B option

**`singularity   shell   -B   $SCRATCH/my_gem5_build:/mnt 
 --writable   my_gem5_sandbox_dir`**

4). once at the Singularity\> prompt, go to the directory where the
software is installed

` Singularity> `**`cd   /opt/gem5`**

5). edit files using the vi editor

` Singularity> `**`vi   src/SConscript`**

6). rebuild the software from the software directory (/opt/gem5) using
the number of cores you used when launching the job

` Singularity> scons build/X86/gem5.opt -j 8`

 7). exit the singularity prompt to get back to the compute node
command line

` Singularity> `**`exit`**

8\) build your new singularity image

` `**`singularity   build   my_gem5.sif 
 my_gem5_sandbox_dir`**

You can add the date to the singularity .sif file name

` `**`singularity   build   my_gem5-$(date   +%m%d%Y).sif 
 my_gem5_sandbox_dir`**

9). exit the Slurm interactive job to return to the login node

**`exit`**

# Bioinformatics Software

## Is this a good bio software to use?

### reliability

Software is not 100% reliable just because it is featured in a
publication and has a github.com repository.

Review the software github or webpage to see when the software was last
updated. If it hasn't been updated in 5 years, it probably has not kept
up with advances in genome sequencing and you should explore other
options.

Always review the output files for correct format including making sure
headers match the correct columns. Even after software has undergone
numerous bug fixes and years of support, you should still review output
files for correctness since features are continually added which can
introduce new bugs with existing features.

Review publications that have used the software in their analysis.

### licensing

Check the license to see if it is a commercial software or open source.

See a [list](/kb3/Software/Bioinformatics/Bioinformatics@Licenses/) of
academic license only tools on HPRC.

### support

Check google groups for software support groups to see how active the
bioinformatics community is with the software.

Check the github page issues tab to see how responsive the developers
are to user requests.

If you find a bug or suspect a bug, review it with your colleagues if
possible to help prevent an oversight on your part and submit a bug
report if it persists.

## Developing bio software

In addition to gnu coding
[standards](https://www.gnu.org/prep/standards/standards.html), useful
guidelines to follow when developing bio software for the sake of those
who will install and use your software.

Some of these are headaches for users and others are headaches for
installers:

1\. Provide an option to show help info (-h and --help) and version info
(-v and --version). Use --verbose instead of -v if you need a verbose
flag.

2\. Allow user to specify a temp directory if many temporary or
intermediate files are generated

3\. Provide a small sample input data set with expected output files to
test complex installations

4\. Provide an option to specify file prefix name to output file instead
of just writing to stdout

5\. Use - for single character option and -- for complete word option
such as -h and --help

`    headache example: blasr starting with -option and changing to --option in their newer versions`

6\. Spend a little extra time developing your code to allow compressed
files as input

7\. Provide released versions of your code instead of relying on latest
main git commit for installation or using a generic name without a
version. This helps when installing and updating software with automated
install tools.

8\. Set file permissions as executable by everyone for dependencies,
precompiled or scripts.
