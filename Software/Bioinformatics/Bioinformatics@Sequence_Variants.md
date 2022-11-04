# Sequence Variants (SNPs, indels)

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Call Variants

### FreeBayes

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_freebayes_1.3.4_grace.sh)

` module spider FreeBayes`

FreeBayes is a Bayesian genetic variant detector designed to find small
polymorphisms, specifically SNPs (single-nucleotide polymorphisms),
indels (insertions and deletions), MNPs (multi-nucleotide
polymorphisms), and complex events (composite insertion and substitution
events) smaller than the length of a short-read sequencing alignment.

### Platypus

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[grace](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_platypus_0.1.9_callvariants_grace.sh)

` module spider Platypus`

Platypus
[homepage](https://www.rdm.ox.ac.uk/research/lunter-group/lunter-group/platypus-a-haplotype-based-variant-caller-for-next-generation-sequence-data)
[github page](https://github.com/andyrimmer/Platypus)

Platypus is a tool designed for efficient and accurate variant-detection
in high-throughput sequencing data. By using local realignment of reads
and local assembly it achieves both high sensitivity and high
specificity. Platypus can detect SNPs, MNPs, short indels, replacements
and (using the assembly option) deletions up to several kb.

### GATK

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

#### GATK 4.0

Use the following command to run GATK version 4.0+ instead of using the
.jar file

`gatk`

If whole genome processing for a large genome is taking a long time, you
can use
[intervals](https://software.broadinstitute.org/gatk/documentation/article?id=11009)
to parallelize the analysis and analyse sequential regions of a
chromosome or more specifically just coding regions.

Below is a step-by-step breakdown of the Best Practices workflow, with a
detailed explanation of why -L should or shouldn’t be used with each
tool.

| Tool                              | \-L | Why or why not?                                                                                                                                                                |
| :-------------------------------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| BaseRecalibrator                  | YES | This excludes off-target sequences and sequences that may be poorly mapped, which have a higher error rate. Including them could lead to a skewed model and bad recalibration. |
| PrintReads                        | NO  | Output is a bam file; using -L would lead to lost data.                                                                                                                        |
| UnifiedGenotyper/Haplotype Caller | YES | We’re only interested in making calls in exome regions; the rest is a waste of time & includes lots of false positives.                                                        |
| Next steps                        | NO  | No need since subsequent steps operate on the callset, which was restricted to the exome at the calling step.                                                                  |

#### GATK 3.0

Recommended workflows for variant discovery analysis with
[GATK](https://www.broadinstitute.org/gatk/guide/best-practices.php)

` module spider GATK`

To execute GATK run:

` java -jar $EBROOTGATK/GenomeAnalysisTK.jar`

The GATK is the industry standard for identifying SNPs and indels in
germline DNA and RNAseq data

The GATK tools are primarily designed to process exomes and whole
genomes generated with Illumina sequencing technology, but they can be
adapted to handle a variety of other technologies and experimental
designs.

### SAMtools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: yes (look at bwa
templates)

` module spider SAMtools`

SAM Tools provide various utilities for manipulating alignments in the
SAM format, including sorting, merging, indexing and generating
alignments in a per-position format.

Example of sorting and creating a bam file without creating an
intermediate sam file (reserving the entire compute node 20 cores).

Notice that using the $TMPDIR for temporary files is useful since files
in $TMPDIR do now count against your quota.

    bwa mem -M -t 20 -R "@RG\tID:my_readgroup\tLB:my_library\tSM:my_sample\tPL:ILLUMINA" \
     my_ref_genome.fasta paired_end_R1.fastq.gz paired_end_R2.fastq.gz | samtools view -h -Sb - | \
     samtools sort -m 2G --threads 10 - -T $TMPDIR/sorted -o my_output_bam

### IMSindel

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[terra](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_imsindel_1.0.1_terra.sh)

[IMSindel](https://github.com/NCGG-MGC/IMSindel) An accurate
intermediate-size indel detection tool incorporating de novo assembly
and gapped global-local alignment with split read analysis.

`module load IMSindel/1.0.1-foss-2019b-Ruby-2.7.1`

The output directory option --outd is required and the directory must
exist prior to running imsindel.

The memory usage is low and you can complete the analysis in a timely
manner by using half the cores on a compute node since the early step
uses multiple cores but the majority of the remaining processing uses
one core.

### Parsnp

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module load Parsnp/1.2-Linux64`

Parsnp is a command-line-tool for efficient microbial core genome
alignment and SNP detection. Parsnp was designed to work in tandem with
Gingr, a flexible platform for visualizing genome alignments and
phylogenetic trees; both Parsnp and Gingr form part of the Harvest
suite.

### kSNP

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module load kSNP/3.021-Linux_package`

kSNP identifies the pan-genome SNPs in a set of genome sequences, and
estimates phylogenetic trees based upon those SNPs. SNP discovery is
based on k-mer analysis, and requires no multiple sequence alignment or
the selection of a reference genome, so kSNP can take 100's of microbial
genomes as input.

### Delly

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_bwa_delly_0.8.1_pe_call_ada.sh)

Delly [homepage](https://github.com/dellytools/delly)

Delly is an integrated structural variant (SV) prediction method that
can discover, genotype and visualize deletions, tandem duplications,
inversions and translocations at single-nucleotide resolution in
short-read massively parallel sequencing data. It uses paired-ends,
split-reads and read-depth to sensitively and accurately delineate
genomic rearrangements throughout the genome. Structural variants can be
visualized using Delly-maze and Delly-suave.

`module spider Delly`

Delly primarily parallelizes on the sample level. Hence,
OMP\_NUM\_THREADS should be always smaller or equal to the number of
input samples.

If you have 5 samples, for example, you would use the following in your
job script along with the appropriate \#SBATCH values:

`export OMP_NUM_THREADS=5`

## Annotate Variants

### snpEff

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[terra](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_snpeff_4.3t_terra.sh)

snpEff [homepage](http://snpeff.sourceforge.net/)

` module spider snpEff`

Genetic variant annotation and effect prediction toolbox.

To see a list of available snpEff genome databases

` java -jar $EBROOTSNPEFF/snpEff.jar databases`

#### Download pre-built database

This must be done on a login node and not in a job script.

1\) First load the snpEff version of your choice

`module load snpEff/4.3t-foss-2018b-Python-3.6.6-Java-1.8.0`

2\) Copy the main snpEff.config file to your current directory

`cp $EBROOTSNPEFF/snpEff.config ./`

3\) See if the genome is available (save output to a file then search
the file):

`java -Xmx4g -jar $EBROOTSNPEFF/snpEff.jar databases > avail_dbs.txt`

4\) Download database using your snpEff.config file which will download
it to the current directory in a directory called data:

`java -Xmx4g -jar $EBROOTSNPEFF/snpEff.jar download -c snpEff.config Sporisorium_reilianum`

5\) Use the -config option when running snpEff commands in your job
script:

`java -Xmx4g -jar $EBROOTSNPEFF/snpEff.jar -config snpEff.config Sporisorium_reilianum my_file.vcf > annotated.vcf`

#### Create your own database

You can create your own custom database with a sequences.fasta and
genome.gff3 file (or .gff).

This must be done on a login node and not in a job script.

The following example creates a database for AaegL5.0

1\) First load the snpEff version of your choice

`module load snpEff/4.3t-foss-2018b-Python-3.6.6-Java-1.8.0`

2\) Make a directory for your new config file and database files

`mkdir -p $SCRATCH/snpeff/4.3t`

3\) Copy the main snpEff.config file to your new directory

`cp $EBROOTSNPEFF/snpEff.config $SCRATCH/snpeff/4.3t/`

4\) Edit your snpEff.config file and change the data.dir to the
directory in your $SCRATCH (use your NETID in the full path)

`data.dir = /scratch/user/`**`NETID`**`/snpeff/4.3t`

5\) Add a unique line to your snpEff.config file with your custom genome
name using spaces:

`AaegL5.0.genome : AaegL5.0`

6\) Make a directory with the same name that you added to the
snpEff.config file and copy your unzipped reference genome and gff3
files to the new directory $SCRATCH/snpeff/4.3t/

    mkdir $SCRATCH/snpeff/4.3t/AaegL5.0
    cp my_reference_genome.fa $SCRATCH/snpeff/4.3t/AaegL5.0/
    cp my_reference_genome.gff $SCRATCH/snpeff/4.3t/AaegL5.0/

7\) Create symlinks in the new directory to your two files with names
sequence.fa and genes.gff

    cd $SCRATCH/snpeff/4.3t/AaegL5.0/
    ln -s my_reference_genome.fa sequences.fa
    ln -s my_reference_genome.gff genes.gff

8\) Make the database using the -config option to specify the new config
file.

`java -jar $EBROOTSNPEFF/snpEff.jar build -config $SCRATCH/snpeff/4.3t/snpEff.config -gff3 AaegL5.0`

This will create a snpEffectPredictor.bin file in the build.dir

9\) You can delete the reference and gff files from the directory after
you create the database

    cd $SCRATCH/snpeff/4.3t/AaegL5.0/
    unlink sequences.fa
    unlink genes.gff
    rm my_reference_genome.fa
    rm my_reference_genome.gff

10\) Use the -config option when running snpEff commands in your job
script:

`java -jar $EBROOTSNPEFF/snpEff.jar -config $SCRATCH/snpeff/4.3t/snpEff.config AaegL5.0  my_file.vcf > annotated.vcf`

## Variant Effect on Protein

### PROVEAN

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_provean_1.1.5_ada.sh)

PROVEAN [homepage](http://provean.jcvi.org/index.php)

` module spider PROVEAN`

PROVEAN (Protein Variation Effect Analyzer) is a software tool which
predicts whether an amino acid substitution or indel has an impact on
the biological function of a protein.

PROVEAN is useful for filtering sequence variants to identify
nonsynonymous or indel variants that are predicted to be functionally
important.

Since it uses BLAST and psiBLAST against the nr database, it is slow and
may take several minutes per query.

If you are working with human variants, you can download a file of
precomputed scores for every amino acid change at every position for all
human genes at: <http://provean.jcvi.org/downloads.php>
