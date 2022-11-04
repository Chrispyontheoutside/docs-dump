# NGS: Sequence QC

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Evaluation

### FastQC

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_fastqc_0.11.9_grace.sh)
[terra](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_fastqc_0.11.9_terra.sh)

` module spider FastQC`

After running FastQC via the command line, you can ssh to an HPRC
cluster enabling X11 forwarding by using the -X option and view the
images using the eog tool.

From your desktop:

` ssh -X username@grace.hprc.tamu.edu`

From your FastQC working directory on Grace unzip the .zip results file
then use eog to view the results in the Images directory:

` eog sample_fastqc/Images/per_sequence_gc_content.png`

You can also run FastQC interactively using the FastQC GUI by logging in
using X11 forwarding and running the command:

` fastqc`

### RNA-SeQC

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(w/bwa)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_rnaseqc_1.1.8_bwa_aln_2samples_se_ada.sh)
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_rnaseqc_1.1.8_bam_inputs_2samples_se_ada.sh)

RNA-SeQC
[homepage](http://archive.broadinstitute.org/cancer/cga/rna-seqc)

` module spider RNA-SeQC`

RNA-SeQC is a java program which computes a series of quality control
metrics for RNA-seq data.

To run RNA-SeQC after loading the module:

` java -jar $EBROOTRNASEQC/RNA-SeQC_v1.1.8.jar`

### KmerGenie

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_kmergenie_1.6982_ada.sh)

KmerGenie [homepage](http://kmergenie.bx.psu.edu/)

` module spider KmerGenie`

KmerGenie estimates the best k-mer length for genome de novo assembly.

### Qualimap

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Qualimap [homepage](http://qualimap.bioinfo.cipf.es/doc_html/intro.html)

  - fast analysis across the reference genome of mapping coverage and
    nucleotide distribution;
  - easy-to-interpret summary of the main properties of the alignment
    data;
  - analysis of the reads mapped inside/outside of the regions defined
    in an annotation reference;
  - computation and analysis of read counts obtained from intersting of
    read alignments with genomic features;
  - analysis of the adequacy of the sequencing depth in RNA-seq
    experiments;
  - support for multi-sample comparison for alignment data and counts
    data;
  - clustering of epigenomic profiles.

`module spider Qualimap`

Enter the following command to see the command line options

`qualimap -h`

Qualimap will use more than one core so you will need to specify the
number of cores using the qualimap -nt option.

You can capture the number of cores you specify in the Slurm parameters
with the environment variable $SLURM\_CPUS\_PER\_TASK

For example if you have these Slurm parameters:

`#SBATCH --ntasks-per-node=1`  
`#SBATCH --cpus-per-task=28`

Then you can use the -n value with the environment variable
$SLURM\_CPUS\_PER\_TASK to specify the number of cores for qualimap to
use

`qualimap -nt $SLURM_CPUS_PER_TASK`

If you run qualimap without options, it will start the GUI version. The
GUI version works best with the HPRC Portal.

If you would like to use the GUI version, you can login to the OnDemand
portal at [portal.hprc.tamu.edu](https://portal.hprc.tamu.edu) and
select VNC in the 'Interactive Apps' tab. You might start with all cores
and all memory initially until you get an idea of how much memory is
required for Qualimap.

When the VNC loads after clicking the blue launch button, you will reach
a terminal where you can start the GUI version of Qualimap with the
following commands

    module purge
    module spider Qualimap
    # load the latest version using the appropriate module load command then run qualimap
    qualimap

## Screen Reads

### FastQScreen

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

[homepage](http://www.bioinformatics.babraham.ac.uk/projects/fastq_screen/)

FastQ Screen allows you to screen a library of sequences in FastQ format
against a set of sequence databases so you can see if the composition of
the library matches with what you expect.

`module load FastQScreen/0.11.4-intel-2015B-Perl-5.20.0`

Version 0.11.4 requires the full path to the alignment binary. Use any
of the following in your config file

    BOWTIE   /software/easybuild/software/Bowtie/1.1.2-intel-2015B/bin/bowtie
    BOWTIE2  /software/easybuild/software/Bowtie2/2.2.9-intel-2015B/bin/bowtie2
    BWA      /software/easybuild/software/BWA/0.7.15-intel-2015B/bin/bwa
    BISMARK  /software/easybuild/software/Bismark/0.17.0-intel-2015B/bismark

There are some databases already available on Ada. Your config file will
look like the following for screening the PhiX and UniVec databases
using Bowtie2.

    BOWTIE2  /software/easybuild/software/Bowtie2/2.2.9-intel-2015B/bin/bowtie2
    
    DATABASE  PhiX   /scratch/datasets/genome_indexes/ncbi/PhiX/bowtie2/NC_001422.1
    DATABASE  UniVec /scratch/datasets/genome_indexes/univec/UniVec_Core/bowtie2/UniVec_Core.fa

## Trim

### Trimmomatic

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_trimmomatic_0.39_pe_grace.sh)

Trimmomatic [homepage](http://www.usadellab.org/cms/?page=trimmomatic)

Trimmomatic
[manual](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf)

` module spider Trimmomatic`

Trimmomatic performs a variety of useful trimming tasks for illumina
paired-end and single ended data

Sample command for version 0.39

` java -jar $EBROOTTRIMMOMATIC/trimmomatic-0.39.jar [SE|PE] `<options>` `<files>` ... ILLUMINACLIP:$EBROOTTRIMMOMATIC/adapters/TruSeq3-PE.fa:2:30:10`

### Cutadapt

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Cutadapt
[homepage](http://cutadapt.readthedocs.org/en/stable/index.html)

` module spider cutadapt`

Cutadapt finds and removes adapter sequences, primers, poly-A tails and
other types of unwanted sequence from your high-throughput sequencing
reads.

#### Galaxy

To keep all reads that do not align to any database and also reads that
align to all databases (conserved reads) you need to do three steps for
paired end files:

1\) use FastQScreen with the following options: Filter results into new
fastq file? =\> Align and graph results without filtering fastq file
Select how many reads to screen =\> Use all reads Create tagged file?
=\> Yes Then select the aligner and check the checkboxes for the
databases you want. This will produce a TAGGED file which you will use
as input for the "Select FastQ Screen reads"

2\) In the "Select FastQ Screen reads" tool, select the following
options: that =\> match tags Tag type =\> preconfigured Tags =\> All
db's are 0's or all db's are non-0's

3\) Then if these are paired reads, you can use the Re-pair tool.

## Sequencing Error Correction

### Quake

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Quake [homepage](http://www.cbcb.umd.edu/software/quake/index.html)

` module spider Quake`

Quake is a package to correct substitution sequencing errors in
experiments with deep coverage (e.g. \>15X), specifically intended for
Illumina sequencing reads.

### Lighter

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Lighter [homepage](https://github.com/mourisl/Lighter)

` module spider Lighter`

Lighter is a kmer-based error correction method for whole genome
sequencing data.

Lighter uses sampling (rather than counting) to obtain a set of kmers
that are likely from the genome.

Using this information, Lighter can correct the reads containing
sequence errors.

## Merge overlapping reads

### FLASH

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_flash_2.2.00_pe_grace.sh)

FLASH [homepage](https://ccb.jhu.edu/software/FLASH/)

` module spider FLASH`

FLASH (Fast Length Adjustment of SHort reads) is a very fast and
accurate software tool to merge paired-end reads from next-generation
sequencing experiments.

FLASH is designed to merge pairs of reads when the original DNA
fragments are shorter than twice the length of reads.

The resulting longer reads can significantly improve genome assemblies.

They can also improve transcriptome assembly when FLASH is used to merge
RNA-seq data.

### Pear

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Pear [homepage](http://sco.h-its.org/exelixis/web/software/pear/)

` module spider Pear`

PEAR is an ultrafast, memory-efficient and highly accurate pair-end read
merger. It is fully parallelized and can run with as low as just a few
kilobytes of memory.

PEAR evaluates all possible paired-end read overlaps and without
requiring the target fragment size as input. In addition, it implements
a statistical test for minimizing false-positive results.

### Coperead

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Coperead [homepage](https://sourceforge.net/projects/coperead/)

` module spider Coperead`

COPE (Connecting Overlapped Pair-End reads) is a method to align and
connect the illumina sequenced Pair-End reads of which the insert size
is smaller than the sum of the two read length.
