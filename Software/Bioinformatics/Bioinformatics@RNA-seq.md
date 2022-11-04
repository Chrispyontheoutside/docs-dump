# RNA-seq

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## TUTORIALS

[VIDEO](https://www.youtube.com/watch?v=xh_wpWj0AzM) "How to analyze
RNA-Seq data? Find differentially expressed genes in your research"

[tutorials](https://github.com/griffithlab/rnaseq_tutorial) from
Griffithlab on RNA-seq analysis workflow

example [R
script](https://gist.github.com/stephenturner/f60c1934405c127f09a6) for
DESeq2

## Transcriptome Assembly

### Trinity

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_trinity_2.12.0_pe_tmpdir_grace.sh)

` module spider Trinity`

Trinity [homepage](https://github.com/trinityrnaseq/trinityrnaseq/wiki)

Trinity tutorial
[videos](https://www.broadinstitute.org/broade/trinity-screencast)

Trinity [memory](http://trinityrnaseq.github.io/performance/mem.html)
requirements summary

Trinity performs *de novo* or reference guided genome assemblies of
transcript sequences from Illumina RNA-Seq data.

R Bioconductor libraries, such as qvalue, required by some Trinity
analysis scripts are found in this R\_tamu module

` module load R_tamu/3.6.0-foss-2018b-recommended-mt`

Trinity will create 100,000+ temporary files during an analysis run. A
quota of 250,000 files (with about 225,000 available) should be enough
for one Trinity run at a time. If you want to run multiple Trinity jobs
at once, you can use run the analysis in $TMPDIR and copy the results
files to your $SCRATCH working directory.

You need to use a directory after $TMPDIR with 'trinity' in the name
which will get automatically created. Example: $TMPDIR/trinity\_out

Trinity does have checkpoints. If your job times out and you run the
same job script again, it should pick up where it left off unless you
are using $TMPDIR.

If you are using Galaxy then checkpoints will not work.

**NOTE:** Trinity 2.4.0+ utilizes seqtk for read normalization which
requires read headers to be in a specific format.

This version of Trinity requires either fastq headers in the new style:

`   @M01581:927:000000000-ARTAL:1:1101:19874:2078 1:N:0:1`

or that the fastq headers end with /1 or /2 such as:

`   @M01581:927:000000000-ARTAL:1:1101:19874:2078/1`

<!-- An example of adding /1 and /2 to headers can be found [
here](/All-Pages/Ada:NGS:File_Format_Tools/#add-.2f1-or-.2f2-at-end-of-fastq-headers "wikilink") -->

If your data come from SRA, be sure to dump the fastq file like so:

` fastq-dump --defline-seq '@$sn[_$rn]/$ri' --split-files file.sra`

#### Sample Trinity Paired End Assembly job Scripts

##### Terra: 54 GB compute nodes

using all 28 cores for 7 days

    #!/bin/bash
    #SBATCH --export=NONE
    #SBATCH --job-name=trinity
    #SBATCH --time=7-00:00:00
    #SBATCH --ntasks-per-node=1
    #SBATCH --cpus-per-task=28
    #SBATCH --mem=56G
    #SBATCH --output=stdout.%x.%j
    #SBATCH --error=stderr.%x.%j
    
    module load Trinity/2.11.0-foss-2018b-Python-3.6.6
    
    Trinity --workdir $TMPDIR/trinity_workdir --max_memory 52G --CPU 28 --inchworm_cpu 6 --no_version_check --seqType fq --left myreads_1.fastq.gz --right myreads_2.fastq.gz

The chrysalis step will generate thousands of small files in the $TMPDIR
when specifying --workdir $TMPDIR/trinity\_workdir which can help in
preventing the job from creating more files than are available in your
file quota.

Set the --max\_memory value to a few GB below the \#SBATCH --mem= to
prevent reaching the memory limit with Trinity sub-processes.

The --full\_cleanup option will remove all the thousands of intermediate
temporary files once Trinity has completed.

If you use the --full\_cleanup option (recommended), then the final
Trinity.fasta file will be copied to the working directory and the
outdir will be deleted.

If you do not see your Trinity.fasta file in the working directory then
just submit the job script again and let it finish the final step.

If you do not use the --full\_cleanup option, then the final
Trinity.fasta file will be in the outdir. If you do not see it there
then just submit the job script again and let it finish the final step.

##### using $TMPDIR

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_trinity_2.12.0_pe_tmpdir_grace.sh)

You can use the $TMPDIR to write all files to a local drive on the
compute node. All files written to $TMPDIR do not count against your
file quota so you don't have to request a file quota increase.

Example commands to use in your job script to run Trinity and copy the
result files to your working directory:

    Trinity --seqType fq --max_memory 52G --single myseqs.fastq.gz --CPU 28 --no_version_check --inchworm_cpu 6 --output $TMPDIR/trinity_out
    cp $TMPDIR/trinity_out/Trinity.fasta.gene_trans_map ./
    cp $TMPDIR/trinity_out/Trinity.fasta ./

When Trinity is complete, the two necessary results files are copied
from the $TMPDIR to the working directory. Rename the files with a
prefix if needed when copying the two result files.

If you use $TMPDIR no checkpoints are available. If the job fails due to
running out of walltime or memory, all files are deleted and you have to
start from the beginning.

You can't use $TMPDIR if using grid mode with tamulauncher.

#### Example Trinity Tutorials

[Trinity with
edgeR](https://github.com/trinityrnaseq/RNASeq_Trinity_Tuxedo_Workshop/wiki/Trinity-De-novo-Transcriptome-Assembly-Workshop)

If you need more than the 3TB memory Grace compute nodes, you can use
[external
HPCs](https://github.com/trinityrnaseq/trinityrnaseq/wiki/Accessing%20Trinity%20on%20Publicly%20Available%20Compute%20Resources)

### Scripture

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Scripture
[homepage](http://www.broadinstitute.org/software/scripture/home)

`module spider Scripture`

Scripture is a method for transcriptome reconstruction that relies
solely on RNA-Seq reads and an assembled genome to build a transcriptome
*ab initio*.

The statistical methods to estimate read coverage significance are also
applicable to other sequencing data.

Scripture also has modules for ChIP-Seq peak calling.

### StringTie

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

StringTie [homepage](https://ccb.jhu.edu/software/stringtie/)

` module spider StringTie`

StringTie is a fast and highly efficient assembler of RNA-Seq alignments
into potential transcripts.

To identify differentially expressed genes between experiments,
StringTie's output can be processed either by the Cuffdiff or Ballgown
programs.

### Trans-ABySS

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Trans-ABySS
[homepage](http://www.bcgsc.ca/platform/bioinfo/software/trans-abyss/)

` module spider Trans-ABySS`

de novo assembly of RNA-Seq data using ABySS

The current version of the Trans-ABySS package comes with 3 main
applications:

1\. transabyss - assemble RNAseq data

2\. transabyss-merge - merge multiple assemblies from (1)

3\. transabyss-analyze - analyze assemblies, either from (1) or (2), for
structural variants and splice variants. Requires reference genome and
annotations.

### SOAPdenovo-Trans

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

SOAPdenovo-Trans
[home](http://soap.genomics.org.cn/SOAPdenovo-Trans.html)

` module spider SOAPdenovo-Trans`

SOAPdenovo-Trans is a de novo transcriptome assembler basing on the
SOAPdenovo framework, adapt to alternative splicing and different
expression level among transcripts.The assembler provides a more
accurate, complete and faster way to construct the full-length
transcript sets.

For animal transcriptomes like mouse, about 30-35GB memory would be
required.

## Transcriptome Assembly Evaluation

### DETONATE

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(w/bam)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_detonate-1.10_w-bam_ada.sh)
[ada
(wo/bam)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_detonate-1.10_wo-bam_ada.sh)

DETONATE [homepage](http://deweylab.biostat.wisc.edu/detonate/)

` module spider DETONATE`

DETONATE (DE novo TranscriptOme rNa-seq Assembly with or without the
Truth Evaluation) consists of two component packages, RSEM-EVAL and
REF-EVAL. Both packages are mainly intended to be used to evaluate de
novo transcriptome assemblies, although REF-EVAL can be used to compare
sets of any kinds of genomic sequences.

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

## Transcriptome Assembly Annotation

### Trinotate

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_trinotate_3.1.1_ada.sh)

Trinotate [home](https://trinotate.github.io/)

` module load Trinotate/3.1.1-intel-2017A-Python-2.7.12`

Trinotate is a comprehensive annotation suite designed for automatic
functional annotation of transcriptomes, particularly de novo assembled
transcriptomes, from model or non-model organisms.

Trinotate has a pipeline script that can be used to run all annotation
steps at once.

Trinotate has checkpoints so if your job is stopped, you can restart the
job and it should start from the last checkpoint.

You will need to copy the Trinotate.sqlite database from the following
directory to your working directory. You should not have this line in
your job script if you are restarting a stopped job. The following UNIX
command will copy the necessary files to your current working directory.
Run this command on the UNIX command line prior to running your job:

    module load Trinotate/3.1.1-intel-2017A-Python-2.7.12
    cp $EBROOTTRINOTATE/resources/Trinotate.sqlite ./
    chmod 755 Trinotate.sqlite

Then in your job script, use the following two lines to create a gene to
transcript map and run the pipeline on your Trinity.fasta assembled
transcripts file:

` $TRINITY_HOME/util/support_scripts/get_Trinity_gene_to_trans_map.pl Trinity.fasta > Trinity.fasta.gene_to_trans_map`

` $TRINOTATE_HOME/auto/autoTrinotate.pl --transcripts Trinity.fasta --CPU 20 \`  
` --Trinotate_sqlite Trinotate.sqlite --gene_to_trans_map Trinity.fasta.gene_to_trans_map`

### TransDecoder

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_transdecoder_3.0.1_ada.sh)

TransDecoder [home](https://github.com/TransDecoder/TransDecoder)

` module spider TransDecoder`

TransDecoder identifies candidate coding regions within transcript
sequences, such as those generated by de novo RNA-Seq transcript
assembly using Trinity, or constructed based on RNA-Seq alignments to
the genome using Tophat and Cufflinks.

### miRNA

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

miRNA [home](https://github.com/bcgsc/mirna)

` module spider miRNA`

The BCGSC miRNA Profiling Pipeline produces expression profiles of known
miRNAs from BWA-aligned BAM files and generates summary reports and
graphs describing the results.

The miRNA application uses a local copy of the UCSC and miRBase
databases. The UCSC database is populated only with the organism being
analyzed.

First create a directory, go to that directory and run the startup
script

` mkdir $SCRATCH/mirna_setup`  
` cd $SCRATCH/mirna_setup`  
` /software/hprc/Bio/mirna/scripts/setup_mysql.sh`

You only need to run this once and it is run on the command line and not
within a job script. It takes about 10 minutes to populate the UCSC and
miRBase database files.

Once you successfully run this setup script, you do not need the script
any more.

You can run miRNA from any $SCRATCH directory you just need to rsync the
installation files to your working directory

` cd $SCRATCH/my_working_directory/`  
` rsync -arv $SCRATCH/mirna_setup/ ./`

Then you need to create a project directory inside your job script
directory and place your .sam and adapter.report file in that directory.
In this example the project directory is called project.

Notice that the names of the adapter.report and .sam file must be in
this format:

    project/my_sorted.sam
    project/my_sorted_adapter.report

Currently there is only support for the Dog genome. The UCSC database
and species codes are

``` 
ucsc_database='canFam3'
ucsc_species_code='cfa'   
```

The commands in your job script will look like this:

    # run the mysqld command to start the database
    ./mysqld start &
    
    sleep 120            # give mysqld_mirna time to initialize the database
    
    annotate.pl -m mirna_21a -u canFam3 -o cfa -p project
    
    # run the mysqld command to stop the database
    ./mysqld stop

The job script will launch a MySQL database on the compute node and run
the analysis and then stop the MySQL database.

## Differential Expression

### Bowtie & Bowtie2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [Grace
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_bowtie_2.3.3.1_pe_terra.sh)
    [Grace
(se)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_bowtie_2.3.3.1_se_terra.sh)

Bowtie [homepage](http://bowtie-bio.sourceforge.net/index.shtml)

` module spider Bowtie`

Genome indexes for bowtie can be found in the ucsc directory for each
organism:

` /scratch/datasets/genome_indexes/ucsc/organism_name/bowtie_index`

Bowtie2
[homepage](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)

` module spider Bowtie2`

Genome indexes for bowtie2 can be found in the ucsc directory for each
organism:

` /scratch/datasets/genome_indexes/ucsc/organism_name/bowtie2_index`

Bowtie indexes will not work with the Bowtie2 aligner.

Bowtie2 indexes will not work with the Bowtie aligner.

Please contact the HPRC helpdesk help@sc.tamu.edu if you need additional
genome indexes

### Cufflinks

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_tophat_cufflinks_cuffdiff_4samples_2groups_ada.sh)

Cufflinks [homepage](http://cole-trapnell-lab.github.io/cufflinks/)

` module spider Cufflinks`

Cufflinks assembles transcripts, estimates their abundances, and tests
for differential expression (cuffdiff) and regulation in RNA-Seq
samples.

Cufflinks includes a program, “cuffdiff”, that you can use to find
significant changes in transcript expression, splicing, and promoter
use.

### cummeRbund

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module load R_tamu/3.2.5-iomkl-2015B-default-mt`

CummeRbund takes the various output files from a cuffdiff run and
creates a SQLite database of the results describing appropriate
relationships betweeen genes, transcripts, transcription start sites,
and CDS regions.

` library(cummeRbund)`

### Salmon

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Salmon [manual](https://salmon.readthedocs.io/en/latest/)

Salmon is a wicked-fast program to produce a highly-accurate,
transcript-level quantification estimates from RNA-seq data.

`module load Salmon/0.14.1-linux_x86_64`

### Sailfish

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_sailfish_0.10.0_grace.sh)

Sailfish
[homepage](http://www.cs.cmu.edu/~ckingsf/software/sailfish/index.html)

` module spider Sailfish`

Sailfish: Rapid Alignment-free Quantification of Isoform Abundance

### edgeR

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

edgeR
[homepage](https://bioconductor.org/packages/release/bioc/html/edgeR.html)

` module spider R_tamu/3.2.0-iomkl-2015B-default-mt`

Empirical analysis of digital gene expression data in R

edgeR
[Tutorial](https://web.stanford.edu/class/bios221/labs/rnaseq/lab_4_rnaseq.html)

### DESeq

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

DESeq
[homepage](http://bioconductor.org/packages/release/bioc/html/DESeq.html)

DESeq2
[homepage](https://bioconductor.org/packages/release/bioc/html/DESeq2.html)

` module load R_tamu/3.2.0-intel-2015B-default-mt`

Differential gene expression analysis based on the negative binomial
distribution

Here are good tutorials

` `[`DESeq2 
 tutorial`](https://www.bioconductor.org/help/course-materials/2015/LearnBioconductorFeb2015/B02.1.1_RNASeqLab.html)  
` `[`DESeq2 
 tutorial`](https://bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html)` (use module load R_tamu/3.3.1-intel-2015B-default-mt)`

### Ballgown

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

ballgown
[homepage](https://www.bioconductor.org/packages/release/bioc/html/ballgown.html)

` module load R_tamu/3.5.2-intel-2018b-recommended-mt`

Tools for statistical analysis of assembled transcriptomes, including
flexible differential expression analysis, visualization of transcript
structures, and matching of assembled transcripts to annotation.

Ballgown\_input\_files(generated by StringTie for example): count files
(\*ctab files) for each sample

  - e\_data.ctab: exon-level expression measurements.

<!-- end list -->

  - i\_data.ctab: intron- (i.e., junction-) level expression
    measurements

<!-- end list -->

  - t\_data.ctab: transcript-level expression measurements

<!-- end list -->

  - e2t.ctab: table with two columns, e\_id and t\_id, denoting which
    exons belong to which transcripts

<!-- end list -->

  - i2t.ctab: table with two columns, i\_id and t\_id, denoting which
    introns belong to which transcripts

### kallisto

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

kallisto [homepage](https://pachterlab.github.io/kallisto/about.html)

kallisto is a program for quantifying abundances of transcripts from
RNA-Seq data, or more generally of target sequences using
high-throughput sequencing reads.

` module load kallisto/0.45.0-foss-2018b`

### Sleuth

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

sleuth [homepage](http://pachterlab.github.io/sleuth/about.html)
[usage](https://rawgit.com/pachterlab/sleuth/master/inst/doc/intro.html)

Sleuth is a program for analysis of RNA-Seq experiments for which
transcript abundances have been quantified with kallisto. sleuth
provides tools for exploratory data analysis utilizing Shiny by RStudio,
and implements statistical algorithms for differential analysis that
leverage the boostrap estimates of kallisto.

`module load sleuth/0.28.0-iomkl-2015B-R-3.2.5-default-mt`
