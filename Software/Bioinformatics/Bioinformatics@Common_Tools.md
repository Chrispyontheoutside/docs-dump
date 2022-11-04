# NGS: Common Tools

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

### Parallel

GCATemplates available: no

Gnu Parallel - build and execute shell command lines from standard input
in parallel

Gnu Parallel
[documentation](https://www.gnu.org/software/parallel/parallel.html)

Example Grace job script where many input .fasta files are in a
directory named inputs and an empty directory exists named outputs

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=my_parallel_job  # job name
    #SBATCH --time=7-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=48          # CPUs (threads) per command
    #SBATCH --mem=360G                  # total memory per node
    #SBATCH --output=stdout.%x.%j       # save stdout to file
    #SBATCH --error=stderr.%x.%j        # save stderr to file
    
    module load GCC/10.2.0  OpenMPI/4.0.5  MAFFT/7.490-with-extensions
    module load parallel/20210322
    
    parallel --joblog mafft.log "mafft {} > outputs/{/.}.aln.fasta" ::: inputs/*.fasta

When the job is complete, you can check the mafft.log file to see that
all commands completed successfully by looking at the Exitval column
where 0 = completed successfully and a non-zero value = failed.

`Seq Host    Starttime   JobRuntime  Send  Receive `**`Exitval`**` Signal  Command`  
`1   :      1638568687.578  0.506    0     0       `**`0`**`       0       mafft inputs/sample1.fasta > outputs/sample1.aln.fasta`

If any jobs failed due to running out of walltime or not enough memory,
you can restart the job by running the job script again using the
**--resume-failed** option which will figure out the failed jobs and run
those again. After that it will resume last unfinished job and continue
from there.

` parallel `**`--resume-failed`**` --joblog mafft.log "mafft {} > outputs/{/.}.aln.fasta" ::: inputs/*fasta`

| **command option** | **description**                          | **example output**   |
| ------------------ | ---------------------------------------- | -------------------- |
| {}                 | input line                               | inputs/sample1.fasta |
| {.}                | input line without extension             | inputs/sample1       |
| {/}                | basename of input line                   | sample1.fasta        |
| {/.}               | basename of input line without extension | sample1              |
|                    |                                          |                      |

\=== BamTools === [GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
no

BamTools provides both a programmer's API and an end-user's toolkit for
handling BAM files.

`module load BamTools/2.5.1-GCCcore-6.4.0`

### bgzip

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

bgzip compresses files in a similar manner to, and compatible with, gzip

bgzip can be found in the HTSlib modules

`module load HTSlib/1.9-intel-2018b`

## Picard tools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module spider picard`

The Picard tools use the /tmp directory which has limited space.

Use the automatically generated $TMPDIR directory for all the Picard
tools.

Here is an example of using the $TMPDIR in a job that reserves 54 GB of
memory for the job.

` java -Xmx48g -jar $EBROOTPICARD/SortSam.jar TMP_DIR=$TMPDIR I=myfile.sam O=myfile_sorted.bam SO=coordinate VALIDATION_STRINGENCY=LENIENT`

The java process is limited to 48GB and once picard tools uses all the
48GB of memory, then temporary files are written in the $TMPDIR.

## tabix

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Tabix indexes a TAB-delimited genome position file in.tab.bgz and
creates an index file (in.tab.bgz.tbi or in.tab.bgz.csi) when region is
absent from the command-line. The input data file must be position
sorted and compressed by bgzip which has a gzip(1) like interface.

`module load SAMtools/1.2-intel-2015B-HTSlib-1.2.1-r2`

## VCFtools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

VCFtools is a program package designed for working with VCF files, such
as those generated by the 1000 Genomes Project. The aim of VCFtools is
to provide easily accessible methods for working with complex genetic
variation data in the form of VCF files.

`module load VCFtools/0.1.16-GCCcore-6.3.0-Perl-5.24.0`

## BEDTools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

The BEDTools utilities allow one to address common genomics tasks such
as finding feature overlaps and computing coverage. The utilities are
largely based on four widely-used file formats: BED, GFF/GTF, VCF, and
SAM/BAM.

`module load BEDTools/2.27.1-GCCcore-6.4.0`

## pybedtools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

The BEDTools suite of programs is widely used for genomic interval
manipulation or “genome algebra”. pybedtools wraps and extends BEDTools
and offers feature-level manipulations from within Python.

` module load BEDTools/2.24.0-intel-2015B`  
` module load python/2.7.6-generic`  
` module load libpng/1.6.18-intel-2015B`  
` module load freetype/2.6-intel-2015B`

## seqtk

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_seqtk_1.3_subsample_pe_grace.sh)

Homepage: <https://github.com/lh3/seqtk>

` module spider Seqtk`

# SRA-toolkit

Used to download Sequence Read Archive files and extract into fasta
file(s).

` # on Grace`  
` module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9`

` # on Terra`  
` module load SRA-Toolkit/2.10.8-gompi-2020a`

SRA-toolkit will download files to your home directory be default and
since your home directory is limited to 10GB, you can redirect the
downloads to your scratch space by creating a directory in scratch and
making a symbolic link to that directory from your home directory.

For the newer versions of SRA-Toolkit, this is done using the vdb-config
command to configure the cache directory to a directory in your $SCRATCH
directory. You only need to run vdb-config once to set up the cache
directory. Do the following on the Grace login command prior to
submitting a job script.

    mkdir /scratch/user/YOUR_NETID/ncbi
    
    # on Grace
    module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9
    vdb-config --interactive
    
        # use letter and tab keys or mouse click to select menu items
    type c for CACHE
    type o for choose
    click [ Create Dir ] then hit enter and type /scratch/user/YOUR_NETID/ncbi
    then select OK and hit enter and hit y to select yes for the question to change the location
    then click s to save and x to exit
    
        # when you are done downloading and processing sra files, you will need to remove downloaded .sra files
        #   from the directory /scratch/user/your_netid/ncbi/sra/

The compute nodes are not connected to the internet so you will need to
add the proxy lines after loading the SRA-Toolkit module in your job
script.

</kb3/Software/Web-Proxy/SW@WebProxy/>

With the web proxy lines added to a job script, you can prefetch a .sra
file then use fastq-dump to process the .sra file. Downloading the .sra
file to $TMPDIR is a good approach since the $TMPDIR is deleted after
the job is complete. You just need to specify an output directory for
the processed fastq files.

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=fastq-dump       # job name
    #SBATCH --time=1-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=2           # CPUs (threads) per command
    #SBATCH --mem=10G                   # total memory per node
    #SBATCH --output=stdout.%x.%j          # save stdout to file
    #SBATCH --error=stderr.%x.%j           # save stderr to file
    
    # on Grace
    module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9
    
    # enable proxy to allow compute node connection to internet
    module load WebProxy
    
    prefetch --output-directory $TMPDIR SRR575500  && \
    fastq-dump --outdir seqs -F -I --gzip $TMPDIR/SRR575500/SRR575500.sra

  - add the --split-files option to the fastq-dump command for paired
    end reads

SRA-toolkit (fast-dump) is also available in Maroon Galaxy.

Browse SRA using [SRA Explorer](https://ewels.github.io/sra-explorer/)
where you can get URLs using the 'saved datasets' feature to directly
download fastq files using wget instead of having to use SRA-toolkit.

## Install Aspera

SRA-Toolkit will look to see if you have Aspera installed. The Aspera
ascp command will download SRA files quicker than wget. Run the
installation script from any directory. This will install configuration
files in your ~/.aspera

`/scratch/helpdesk/ngs/ibm-aspera-connect-3.9.8.176272-linux-g2.12-64.sh`

Example command: ascp -QT -l 300m -P33001 -i
$HOME/.aspera/connect/etc/asperaweb\_id\_dsa.openssh
era-fasp@fasp.sra.ebi.ac.uk:vol1/fastq/ERR315/009/ERR3155119/ERR3155119.fastq.gz
./