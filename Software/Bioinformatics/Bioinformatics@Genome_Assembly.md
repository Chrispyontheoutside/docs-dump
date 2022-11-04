# Genome Assembly

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## NOTES

Effects of kmer size
[example](https://github.com/rrwick/Bandage/wiki/Effect-of-kmer-size)

## *de novo*

### ABySS

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(single-node
pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_abyss_1.9.0_pe_singlenode_grace.sh)
[grace (multi-node
pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_abyss_1.9.0_pe_multinode_grace.sh)

ABySS [homepage](http://www.bcgsc.ca/platform/bioinfo/software/abyss)

Use the 'module spider' command to see the available versions of ABySS

` module spider abyss`

ABySS is a de novo, parallel, paired-end sequence assembler that is
designed for short reads.

The single-processor version is useful for assembling genomes up to 100
Mbases in size.

The parallel version is implemented using MPI and is capable of
assembling larger genomes.

The other ABySS 1.9.0 modules are configured with a maxk of 128.

### WGS

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

WGS
[homepage](http://wgs-assembler.sourceforge.net/wiki/index.php?title=Main_Page)

` module load WGS/8.3rc2-Linux_amd64`

WGS (Celera Assembler) is a *de novo* whole-genome shotgun (WGS) DNA
sequence assembler.

### SPAdes

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_spades_3.14.1_pe_grace.sh)

SPAdes [homepage](http://bioinf.spbau.ru/spades)

` module spider SPAdes`

SPAdes was initially designed for small genomes.

The max k values is 128.

Add the following to your Grace job scripts when using all 48 cores of
the 384GB compute nodes since SPAdes supports OpenMP (use 80 for the
bigmem nodes):

`export OMP_NUM_THREADS=48`

The current version of SPAdes works with Illumina or IonTorrent reads
and is capable of providing hybrid assemblies using PacBio, Oxford
Nanopore and Sanger reads.

You can also provide additional contigs that will be used as long reads.

### Unicycler

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

[Unicycler](https://github.com/rrwick/Unicycler) is an assembly pipeline
for bacterial genomes.

It circularises replicons without the need for a separate tool like
Circlator.

It can assemble Illumina-only read sets where it functions as a
SPAdes-optimiser. It can also assembly long-read-only sets (PacBio or
Nanopore) where it runs a miniasm+Racon pipeline. For the best possible
assemblies, give it both Illumina reads and long reads, and it will
conduct a hybrid assembly.

    module load Unicycler/0.4.6-intel-2017A-Python-3.5.2

### MaSuRCA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_masurca_3.1.2_pe_ada.sh)
[ada
(pe+mp)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_masurca_3.1.2_pe_mp_ada.sh)

MaSuRCA [homepage](http://www.genome.umd.edu/masurca.html)

` module spider MaSuRCA`

MaSuRCA is whole genome assembly software.

MaSuRCA can assemble data sets containing only short reads from Illumina
sequencing or a mixture of short reads and long reads (Sanger, 454).

MaSuRCA version 3.2.1+ can utilize PacBio reads in the assembly.

IMPORTANT\! Do not pre‐process Illumina data before providing it to
MaSuRCA. Do not do any trimming, cleaning or error correction. This WILL
deteriorate the assembly.

### Velvet

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Velvet [homepage](https://www.ebi.ac.uk/~zerbino/velvet/)

` module spider Velvet`

Sequence assembler for very short reads

To see the configured max kmer length for a particular velvet module,
run the following command and look at the MAXKMERLENGTH output:

` velveth -h`

### SGA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(se+pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_sga_0.10.13_se_pe_ada.sh)
[ada
(pe+mp)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_sga_0.10.13_pe_mp_ada.sh)

SGA [homepage](https://github.com/jts/sga)

` module spider SGA`

SGA is a *de novo* assembler designed to assemble large genomes from
high coverage short read data.

SGA implements a set of assembly algorithms based on the FM-index.

As the FM-index is a compressed data structure, the algorithms are very
memory efficient.

### ALLPATHS-LG

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module spider ALLPATHS-LG`

ALLPATHS-LG is a short read assembler and it works on both small and
large (mammalian size) genomes.

To use it, you should first generate ~100 base Illumina reads from two
libraries: one from ~180 bp fragments, and one from ~3000 bp
fragments, both at about 45x coverage.

### DISCOVAR de novo

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_discovardenovo-52488_pe_ada.sh)

DISCOVAR de novo
[homepage](http://www.broadinstitute.org/software/discovar/blog/)

` module spider discovar/discovardenovo-52488`

DISCOVAR *de novo* is a large (and small) de novo genome assembler. It
quickly generates highly accurate and complete assemblies using the same
single library data as used by DISCOVAR.

It currently doesn’t support variant calling – for that, please use
DISCOVAR instead.

### SOAPdenovo & SOAPdenovo2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

SOAPdenovo [homepage](http://soap.genomics.org.cn/soapdenovo.html)

SOAPdenovo2 [homepage](https://github.com/aquaskyline/SOAPdenovo2)

` module spider SOAPdenovo`

or

` module spider SOAPdenovo2`

## Scaffolding

### SSPACE

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_sspace_3.0_mp_ada.sh)

SSPACE
[homepage](http://www.baseclear.com/genomics/bioinformatics/basetools/SSPACE)

` module spider SSPACE-STANDARD`

SSPACE standard is a stand-alone program for scaffolding pre-assembled
contigs using NGS paired-read data.

It is unique in offering the possibility to manually control the
scaffolding process.

### Opera

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(mp)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_opera_2.0.2_mp_ada.sh)
[ada
(pe+mp)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_opera_2.0.2_pe_mp_ada.sh)

Opera
[homepage](http://sourceforge.net/p/operasf/wiki/The%20Opera%20wiki/)

` module spider Opera`

Opera uses information from paired-end/mate-pair reads to order and
orient the intermediate contigs/scaffolds assembled in a genome
assembly.

### BESST

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

BESST [homepage](https://github.com/ksahlin/BESST)

` module spider BESST`

BESST is a package for scaffolding genomic assemblies.

It contains several modules for e.g. building a "contig graph" from
available information, obtaining scaffolds from this graph, and accurate
gap size information.

### L\_RNA\_scaffolder

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_l_rna_scaffolder_se_ada.sh)

L\_RNA\_scaffolder
[homepage](http://www.fishbrowser.org/software/L_RNA_scaffolder/index.php?action=isin&do=download)

` module spider L_RNA_scaffolder`

L\_RNA\_scaffolder is a genome scaffolding tool with long trancriptome
reads.

The long transcriptome reads could be generated by
454/Sanger/Ion\_Torrent sequencing, or *de novo* assembled with pair-end
Illumina sequencing.

## Gap Filling

### GapFiller

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_gapfiller_1.10_pe_ada.sh)

` module spider GapFiller`

GapFiller is a stand-alone program for closing gaps within pre-assembled
scaffolds.

## Merge Assemblies

### Metassembler

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_metassembler_1.5_ada.sh)

` module spider Metassembler`

Metassembler is a software package for reconciling assemblies produced
by *de novo* short-read assemblers such as SOAPdenovo and ALLPATHS-LG.

The goal of assembly reconciliation, or "metassembly," is to combine
multiple assemblies into a single genome that is superior to all of its
constituents.

## Improve Assemblies

### Arrow

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Arrow [homepage](https://github.com/PacificBiosciences/GenomicConsensus)

The GenomicConsensus package provides the variantCaller tool, which
allows you to apply the Quiver or Arrow algorithm to mapped PacBio reads
to get consensus and variant calls.

Arrow is useful if you only have PacBio sequence for genome polishing.

Arrow is installed in the pbbioconda Anaconda shared environment and can
be utilized by loading the following modules.

    module load Anaconda/2-5.0.1
    module load BamTools/2.5.1-GCCcore-7.3.0
    source activate pbbioconda

Running arrow on a single node may complete successfully for a bacterial
genome with 50x coverage.

Polishing large genomes with arrow can take weeks if run on a single
compute node.

It is recommended to use ArrowGrid to do genome polishing on large
genomes starting with your unaligned PacBio subreads.bam files that you
receive from the sequencing center.

#### ArrowGrid\_HPRC

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[Terra](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_arrowgrid_0.6.0_one_polish_terra.sh)

ArrowGrid\_HPRC is a modified version of the
[ArrowGrid](https://github.com/skoren/ArrowGrid) package.

ArrowGrid\_HPRC currently only runs on Terra (SLURM).

***It requires 65,000 SUs to submit a job that has 29 subreads.bam
files***

To estimate the number of required SUs to start an ArrowGrid\_HPRC job,
multiply the number of subreads.bam files \* 2000 and add 7000

`(number_of_subreads.bam_files * 2000) + 7000`

The default is to run each array job for 3 days. You can change this
using the -w option for arrow.sh (see below).

In this case you could estimate the number of required SUs as:

`(number_of_subreads.bam_files * 28 * hours) + 7000`

Example ArrowGrid\_HPRC Job Script:

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=arrow_polish     # set job name
    #SBATCH --time=1-00:00:00           # Set the wall clock limit to 1 day
    #SBATCH --nodes=1                   # uses 1 node
    #SBATCH --ntasks-per-node=1         # run 1 task (command) per node
    #SBATCH --cpus-per-task=28          # each task (command) uses 28 cores
    #SBATCH --mem=56G                   # total memory per node
    #SBATCH --output=stdout.%x.%j          # create a file for stdout
    #SBATCH --error=stderr.%x.%j 
    
    module load ArrowGrid_HPRC/0.6.0-iomkl-2017b
    source activate pbbioconda
    
    arrow.sh -g genome.fasta -p prefix

***You need a file named input.fofn in your working directory that
contains one .subreads.bam file per line.***

Helpful tips for polishing a large genome (polishing example below is
for a 29 PacBio .bam files at 50x coverage):

  - Start with the 29 unaligned PacBio bam files.
      - create a file named input.fofn which contains a list of the 29
        PacBio unaligned.bam files with paths (one per line)
  - Your initial job script is only for running arrow.sh which
    configures the ArrowGrid array jobs so you do not need to submit a
    job array.
  - There are two parallel stages, align and arrow, the array jobs will
    show up in job NAME of the command **squeue -l -u $USER** prefixed
    as align\_ and cns\_ respectively.
      - if the alignment stage completes and the arrow stage fails, then
        reconfigure the SLURM parameters as needed and submit the job
        script again and the second stage will start from where it left
        off.
  - When all 29 arrow array jobs are complete, there is a final merge
    step which results in a .fastq, .fasta and .gff file of your
    polished genome
  - A test run of arrow on 29 unaligned PadBio.bam files for 50x
    coverage of a genome sized 3Gb completed in 36 hours using ArrowGrid
    across 29 compute nodes.

<!-- end list -->

    ------------------------------------------------------------------------
                          Run Arrow in grid mode
    ------------------------------------------------------------------------
    
    Usage: arrow.sh -g <genome_assembly.fasta> -p <prefix>
        Required:
               -g genome.fasta      : GENOME: genome assembly fasta file (with .fai index file in same directory)
        Optional:
               -p prefix            : PREFIX: prefix for output files (default: arrow_polish)
               -r <text>            : ALGORITHM: arrow, quiver (default: arrow)
               -w <text>            : walltime for array jobs (default: SLURM: 3-00:00:00)
               -u <int>             : USEGRID: 0, 1 (default: 1)
          alignment step:           : alignment step values apply to variantCaller step if varantCaller step values are not used
               -a <text>            : additional alignment job submission parameters: Ex: -a '--mail-type=ALL --mail-user=user@email.edu'
               -c <int>             : CPUs for each alignment (blasr) array job (default: 28)
               -m <int>             : memory per node (default: 56G)
               -k <int>             : SLURM tasks per node (default: 1)
               -q <text>            : queue (paritition) for array jobs (default: SLURM: long)
          variantCaller step:       : values for variantCaller step will equal alignment step if the following are not used
               -A <text>            : additional variantCaller job submission parameters: Ex: -A '--mail-type=ALL --mail-user=user@email.edu'
               -C <int>             : CPUs for each variantCaller array job, each CPU needs about 5GB memory (default: 14)
               -M <int>             : memory per node (default: 56G)
               -K <int>             : SLURM tasks per node (default: 1)
               -Q <text>            : queue (paritition) for array jobs (default: SLURM: long)
    
               -h                   : print this help message.

If you use ArrowGrid, be sure to cite ArrowGrid:
<https://github.com/skoren/ArrowGrid>

### Pilon

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_pilon_1.20_ada.sh)
[ada (with
bwa)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_bwa_samtools_pilon_1.20_pe_ada.sh)

Pilon [homepage](https://github.com/broadinstitute/pilon/wiki)

` module spider Pilon`

Pilon is a software tool which can be used if you have Illumina reads
and PacBio to:

  - Automatically improve draft assemblies
  - Find variation among strains, including large event detection

### Redundans

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_redundans_0.13c_refbased_scaf_gapclose_pe_ada.sh)

Redundans [homepage](https://github.com/Gabaldonlab/redundans)

Redundans pipeline assists an assembly of heterozygous genomes. Program
takes as input assembled contigs, sequencing libraries and/or reference
sequence and returns scaffolded homozygous genome assembly. Final
assembly should be less fragmented and with total size smaller than the
input contigs. In addition, Redundans will automatically close the gaps
resulting from genome assembly or scaffolding.

`module load Redundans/0.13c-intel-2017b-Python-2.7.14`

## Gene Modeling

### Augustus

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_augustus_3.2.2_ada.sh)

Augustus [homepage](https://code.google.com/p/augustus/)

` module spider AUGUSTUS`

Augustus is an open source system for building and scoring statistical
models designed to work with data sets that are too large to fit into
memory.

A list of available augustus species can be found here:

` /software/easybuild/software/AUGUSTUS/3.1-intel-2015B-Python-3.4.3/config/species/`

You will need to rsync the Augustus config to one of your directories.
$SCRATCH/my\_augustus\_config is a good place. Make sure you load the
AUGUSTUS module first\!

`module load AUGUSTUS/3.3.1-intel-2017A`  
`mkdir $SCRATCH/my_augustus_config_3.3.1`  
`rsync -r $EBROOTAUGUSTUS/ $SCRATCH/my_augustus_config_3.3.1`

You will also need to add the following in your job script:

`export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config_3.3.1/config"`

### GeneMark-ES

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_genemark-es_4.3_ada.sh)

` module spider GeneMark-ES`

GeneMark-ES is for gene prediction in eukaryotic genomes

To use GeneMark-ES you need to download the GeneMark-ES licence key
file.

`  `<http://topaz.gatech.edu/GeneMark/license_download.cgi>

Select the following: GeneMark-ES and LINUX 64.

You do not need to download the program just the 64\_bit key file.

Save the gm\_key\_64.gz to your $HOME directory on Ada.

Then gunzip the key file and rename it from gm\_key\_64 to .gm\_key

### GeneMarkS

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_genemarks_4.3_ada.sh)

` module spider GeneMarkS`

GeneMarkS is for gene prediction in prokaryotes, intron-less eukaryotes,
eukaryotic viruses, phages and EST/cDNA sequences.

To use GeneMarkS you need to download the GeneMarkS licence key file.

`  `<http://topaz.gatech.edu/GeneMark/license_download.cgi>

Select the following: GeneMark-ES/ET v4.32 and LINUX 64.

You do not need to download the program just the 64\_bit key file.

Save the gm\_key\_64.gz to your $HOME directory on Ada.

Then gunzip the key file and rename it from gm\_key\_64 to .gm\_key

### geneid

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_geneid_1.4.4_ada.sh)

geneid [homepage](http://genome.crg.es/software/geneid/)

` module spider geneid`

geneid is a program to predict genes in anonymous genomic sequences
designed with a hierarchical structure.

### RNAmmer

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

RNAmmer [homepage](http://www.cbs.dtu.dk/cgi-bin/nph-sw_request?rnammer)

`module load RNAmmer/1.2-intel-2017A-Perl-5.24.1-HMMER2.3.2`

RNAmmer predicts ribosomal RNA genes in full genome sequences by
utilising two levels of Hidden Markov Models: An initial spotter model
searches both strands. The spotter model is constructed from highly
conserved loci within a structural alignment of known rRNA sequences.
Once the spotter model detects an approximate position of a gene,
flanking regions are extracted and parsed to the full model which
matches the entire gene. By enabling a two-level approach it is avoided
to run a full model through an entire genome sequence allowing faster
predictions.

### SNAP-HMM

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_snap-hmm_2013-11-29_ada.sh)

` module spider SNAP-HMM`

SNAP-HMM (Semi-HMM-based Nucleic Acid Parser) is a general purpose gene
finding program suitable for both eukaryotic and prokaryotic genomes.

## Genome Annotation

### MAKER

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace (using
$TMPDIR)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_maker_3.01.03_grace.sh)

MAKER [homepage](http://www.yandell-lab.org/software/maker.html)

` module spider MAKER`

MAKER is a portable and easily configurable genome annotation pipeline.

Its purpose is to allow smaller eukaryotic and prokaryotic genome
projects to independently annotate their genomes and to create genome
databases.

Here is a good
[paper](http://onlinelibrary.wiley.com/doi/10.1002/0471250953.bi0411s48/pdf)
to help you get started.

You need to do the following three steps prior to submitting a MAKER job
script on an HPRC cluster

  -   
    1\. Download the GeneMark license key

<!-- end list -->

  - 
    
      -   
        To use MAKER you need to download the GeneMark-ES licence key
        file since GeneMark-ES is part of the MAKER pipeline.

<!-- end list -->

  - 
    
      -   
        Download here:
        <http://topaz.gatech.edu/GeneMark/license_download.cgi>

<!-- end list -->

  - 
    
      -   
        Select the following: GeneMark-ES/ET v4.38 and LINUX 64.

<!-- end list -->

  - 
    
      -   
        You do not need to download the program just the 64\_bit key
        file

<!-- end list -->

  - 
    
      -   
        Save the gm\_key\_64.gz to your $HOME directory.

<!-- end list -->

  - 
    
      -   
        Then gunzip the key file and rename it from gm\_key\_64 to
        .gm\_key

<!-- end list -->

  -   
    2\. Create or copy the three required control files; you must edit
    maker\_opts.ctl

<!-- end list -->

  - 
    
      -   
        **MAKER 2.31.8** use the following commands to *create* the
        three maker control files in your current working directory:

` module load MAKER/2.31.8-intel-2015B-Perl-5.20.0`  
` cp $EBROOTMAKER/sample_ctl_files/* ./`

  - 
    
      -   
        **MAKER 2.31.10** use the following commands to *copy* the three
        maker control files to your current working directory

` module load MAKER/2.31.10-intel-2017A-Python-2.7.12`  
` cp /scratch/datasets/maker/2.31.10/*ctl ./`

  - 
    
      -   
        2a. **maker\_opts.ctl**
          -   
            You need to edit the maker\_opts.ctl file based on your
            project.
            Edit maker\_opts.ctl file to set cpus=20 when using
            *\#SBATCH --cpus-per-task=28* or specify cpus as a command
            option:

<!-- end list -->

    maker -cpus 20

  - 
    
      -   
        Recommended: Set TMP= to $TMPDIR by using the following maker
        option

<!-- end list -->

    maker -TMP $TMPDIR

  - 
    
      -   
        2b. **maker\_bopts.ctl**
          -   
            You do not need to edit the maker\_bopts.ctl file unless you
            want to adjust BLAST parameters.

<!-- end list -->

  - 
    
      -   
        2c. **maker\_exe.ctl**
          -   
            You do not need to edit the maker\_exe.ctl file since it is
            pre-configured with executable paths.

<!-- end list -->

  -   
    3\. Create a GeneMark HMM file

<!-- end list -->

  - 
    
      -   
        A GeneMark HMM file is needed if you want fasta sequences of
        predicted genes.

`module load GeneMarkS/4.32`  
`gmsn.pl -euk your_genome.fasta`  
`gm -m GeneMark.mat -R -lo -op your_genome.fasta`

  - 
    
      -   
        [GeneMark-ES](/kb3/Software/GeneMark-ES/SW@GeneMark-ES/) and
        [GeneMarkS](/kb3/Software/GeneMarkS/SW@GeneMarkS/) are
        installed which can generate the GeneMark HMM file.

<!-- end list -->

  - 
    
      -   
        Once your GeneMark\_hmm.mod file is generated, add it to the
        gmhmm value in the maker\_opts.ctl file.

<!-- end list -->

  -   
    4\. Add an AUGUSTUS species in your maker\_opts.ctl file at the
    line: augustus\_species=
      - 
        
          -   
            You can find a list of AUGUSTUS species by loading the Maker
            module then looking in the directory:

`ls $EBROOTAUGUSTUS/config/species`

#### MAKER 2.31.10

***Maker version 2.31.10 requires that you run two scripts after the
maker command is complete.***

    cd dpp_contig.maker.output
    
    fasta_merge -d dpp_contig_master_datastore_index.log
    gff3_merge -d dpp_contig_master_datastore_index.log

***Maker version 2.31.10 -help information:***

    MAKER version 2.31.10
    
    Usage:
    
         maker [options] <maker_opts> <maker_bopts> <maker_exe>
    
    
    Description:
    
         MAKER is a program that produces gene annotations in GFF3 format using
         evidence such as EST alignments and protein homology. MAKER can be used to
         produce gene annotations for new genomes as well as update annotations
         from existing genome databases.
    
         The three input arguments are control files that specify how MAKER should
         behave. All options for MAKER should be set in the control files, but a
         few can also be set on the command line. Command line options provide a
         convenient machanism to override commonly altered control file values.
         MAKER will automatically search for the control files in the current
         working directory if they are not specified on the command line.
    
         Input files listed in the control options files must be in fasta format
         unless otherwise specified. Please see MAKER documentation to learn more
         about control file  configuration.  MAKER will automatically try and
         locate the user control files in the current working directory if these
         arguments are not supplied when initializing MAKER.
    
         It is important to note that MAKER does not try and recalculated data that
         it has already calculated.  For example, if you run an analysis twice on
         the same dataset you will notice that MAKER does not rerun any of the
         BLAST analyses, but instead uses the blast analyses stored from the
         previous run. To force MAKER to rerun all analyses, use the -f flag.
    
         MAKER also supports parallelization via MPI on computer clusters. Just
         launch MAKER via mpiexec (i.e. mpiexec -n 40 maker). MPI support must be
         configured during the MAKER installation process for this to work though
         
    
    Options:
         -genome|g <file>    Overrides the genome file path in the control files
    
         -RM_off|R           Turns all repeat masking options off.
    
         -datastore/         Forcably turn on/off MAKER's two deep directory
          nodatastore        structure for output.  Always on by default.
    
         -old_struct         Use the old directory styles (MAKER 2.26 and lower)
    
         -base    <string>   Set the base name MAKER uses to save output files.
                             MAKER uses the input genome file name by default.
    
         -tries|t <integer>  Run contigs up to the specified number of tries.
    
         -cpus|c  <integer>  Tells how many cpus to use for BLAST analysis.
                             Note: this is for BLAST and not for MPI!
    
         -force|f            Forces MAKER to delete old files before running again.
                             This will require all blast analyses to be rerun.
    
         -again|a            recaculate all annotations and output files even if no
                             settings have changed. Does not delete old analyses.
    
         -quiet|q            Regular quiet. Only a handlful of status messages.
    
         -qq                 Even more quiet. There are no status messages.
    
         -dsindex            Quickly generate datastore index file. Note that this
                             will not check if run settings have changed on contigs
    
         -nolock             Turn off file locks. May be usful on some file systems,
                             but can cause race conditions if running in parallel.
    
         -TMP                Specify temporary directory to use.
    
         -CTL                Generate empty control files in the current directory.
    
         -OPTS               Generates just the maker_opts.ctl file.
    
         -BOPTS              Generates just the maker_bopts.ctl file.
    
         -EXE                Generates just the maker_exe.ctl file.
    
         -MWAS    <option>   Easy way to control mwas_server for web-based GUI
    
                                  options:  STOP
                                            START
                                            RESTART
    
         -version            Prints the MAKER version.
    
         -help|?             Prints this usage statement.

### BRAKER1

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

BRAKER1 [homepage](http://exon.gatech.edu/braker1.html)

`module spider BRAKER1`

BRAKER1: Unsupervised RNA-Seq-based genome annotation with GeneMark-ET
and AUGUSTUS

Since AUGUSTUS is used, you will need to rsync the Augustus config to
one of your directories. $SCRATCH/my\_augustus\_config is a good place.

    mkdir $SCRATCH/my_augustus_config
    rsync -r $EBROOTAUGUSTUS/ $SCRATCH/my_augustus_config

You will also need to add the following in your job script:

`export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config/config"`

### RepeatMasker

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_repeatmasker_4.1.2_grace.sh)
    [grace
(w/repeatscout)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_repeatmasker_4.1.2_trf_repeatscout_n_mask_grace.sh)

RepeatMasker [homepage](http://www.repeatmasker.org/)

` module spider RepeatMasker`

RepeatMasker is a program that screens DNA sequences for interspersed
repeats and low complexity DNA sequences.

Currently only RMBlast is the configured sequence search engine and is
also the default.

The RebBase database now charges a fee for a subscription to use their
repeat databases. Neither HPRC nor TAMU have a RebBase subscription.
RepeatMasker is available on HPRC clusters with the default repeat
databases provided by RepeatMasker and not the RebBase databases.

### TRF

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

TRF [homepage](https://tandem.bu.edu/trf/trf.html)

` module load trf/409-linux-x86_64`

trf (Tandem Repeats Finder) is a program to locate and display tandem
repeats in DNA sequences.

### RepeatScout

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_repeatmasker_repeatscout_ncbi_lc_mask_ada.sh)

RepeatScout [homepage](http://bix.ucsd.edu/repeatscout/)

` module load RepeatScout/1.0.5-GCCcore-6.3.0`

RepeatScout is a tool to discover repetitive substrings in DNA. The
purpose of the RepeatScout software is to identify repeat family
sequences from genomes where hand-curated repeat databases (a la RepBase
update) are not available. In fact, the output of this program can be
used as input to RepeatMasker as a way of automatically masking
newly-sequenced genomes.

### PASA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_pasa_2.3.3_pipeline_ada.sh)

PASA [homepage](http://pasapipeline.github.io/)

` module load PASA/2.3.3-foss-2018b-Perl-5.28.0`

PASA, acronym for Program to Assemble Spliced Alignments, is a
eukaryotic genome annotation tool that exploits spliced alignments of
expressed transcript sequences to automatically model gene structures,
and to maintain gene structure annotation consistent with the most
recently available experimental sequence data. PASA also identifies and
classifies all splicing variations supported by the transcript
alignments.

You can copy the PASA config files to your working directory and change
the permissions. They are found here:

` $PASAHOME/pasa_conf/`

## Genome Completeness

### BUSCO

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [terra
(busco 4.0.5)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_busco_4.0.5_genome_terra.sh)
    [grace
(busco 4.1.2)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_4.1.2_genome_grace.sh)
    [grace (busco 5.1.2
metaeuk)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_5.1.2_genome_metaeuk_grace.sh)
    [grace (busco 5.1.2
augustus)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_5.1.2_genome_augustus_grace.sh)

BUSCO [homepage](http://busco.ezlab.org/)

#### version 5.0.x

Version 5.0.0+ now uses Metaeuk as the default gene predictor instead of
Augustus so you don't need to rsync the AUGUSTUS directory unless you
want to use Augustus.

Databases for v5.0.0+ are found on Grace in the directory:

`/scratch/data/bio/busco5/lineages`

Contact the HPRC helpdesk if you need additional databases downloaded to
the shared busco5 lineages directory.

#### version 4.0.x

To use BUSCO you need to copy the augustus config files (about 1000
files) to your $SCRATCH directory (only need to do once). Make sure you
load the BUSCO module successfully by running 'module list' after the
module load command.

` module purge`  
` module load BUSCO/4.0.5-foss-2019b-Python-3.7.4`  
` module list`  
` mkdir $SCRATCH/my_augustus_config`  
` rsync -r /sw/eb/software/AUGUSTUS/3.3.3-foss-2019b/  $SCRATCH/my_augustus_config`  
` chmod -R 755 $SCRATCH/my_augustus_config`

You need to add the following in your job script:

` export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config/config"`

The lineages for version 4.0.x use odb10. Contact HPRC helpdesk if there
is not a lineage for your organism in the odb10 directory.

`Grace: /scratch/data/bio/busco4/lineages/`  
`Terra: /scratch/data/bio/BUSCO/odb10/lineages/`

#### version 3.0.2b

To use BUSCO you need to copy the augustus config files (about 1000
files) to your $SCRATCH directory (only need to do once). Make sure you
load the BUSCO module successfully by running 'module list' after the
module load command.

` module purge`  
` module load BUSCO/3.0.2b-intel-2015B-python-2.7.6-generic`  
` module list`  
` mkdir $SCRATCH/my_augustus_config`  
` rsync -r $EBROOTAUGUSTUS/ $SCRATCH/my_augustus_config`  
` chmod -R 755 $SCRATCH/my_augustus_config`

You need to add the following in your job script:

` export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config/config"`

A list of available augustus species can be found here:

` /software/easybuild/software/AUGUSTUS/3.3-intel-2015B/config/species/`

A list of available busco lineages for version 3.0.2b can be found here:

` /scratch/datasets/BUSCO/v3.0.2/`

Run BUSCO in transcriptome mode:

`python $EBROOTBUSCO/scripts/run_BUSCO.py --mode transcriptome`

If you are processing transcriptome data, use **--mode trans** instead
of **--mode Trans** for BUSCO version 1.2

### CEGMA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_cegma_2.5_ada.sh)

` module spider CEGMA`

CEGMA (Core Eukaryotic Genes Mapping Approach) is used for building a
highly reliable set of gene annotations in the absence of experimental
data.

### QUAST

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(w/ref)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_quast_3.2_w-ref_defaults_ada.sh)
[ada
(wo/ref)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_quast_3.2_wo-ref_defaults_ada.sh)

QUAST [homepage](http://bioinf.spbau.ru/quast)

` module load QUAST/5.0.2-intel-2018b-Python-3.6.6`

QUAST evaluates genome assemblies.

### REAPR

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_reapr_1.0.18_pe_mp_ada.sh)

REAPR [homepage](http://www.sanger.ac.uk/science/tools/reapr)

` module spider REAPR`

REAPR is a tool that evaluates the accuracy of a genome assembly using
mapped paired end reads, without the use of a reference genome for
comparison.

### Bandage

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Bandage [homepage](http://rrwick.github.io/Bandage/)

Bandage is a GUI program that allows users to interact with the assembly
graphs made by de novo assemblers such as Velvet, SPAdes, MEGAHIT and
others.

`module load Bandage/0.8.1_Centos`

Bandage is a GUI application that can run faster on the
portal.hprc.tamu.edu

Start a VNC job on the portal and type the following on the command
prompt once your portal job is launched:

`module load Bandage/0.8.1_Centos`  
`Bandage`
