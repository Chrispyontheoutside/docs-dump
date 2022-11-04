# Sequence Alignments

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## BLAST & BLAST+

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(blastx)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_blastx_2.2.31_ada.sh)

` module spider BLAST`

or

` module spider BLAST+`

## mpiBLAST

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module spider mpiBLAST`

mpiBLAST [homepage](http://www.mpiblast.org/)

Make sure to add the following line in your job script

` export I_MPI_MPD_RSH=ssh`

Available formatted dbs are found here in either 38\_frag or 78\_frag

    /scratch/datasets/mpiblast/nt/38_frags
    /scratch/datasets/mpiblast/nr/38_frags
    /scratch/datasets/mpiblast/est_human/38_frags
    
    /scratch/datasets/mpiblast/nt/78_frags
    /scratch/datasets/mpiblast/nr/78_frags
    /scratch/datasets/mpiblast/est_human/78_frags

If you select 38 frags then run your job on 1 nodes using 40 cores per
node since 2 cores are required for mpiBLAST for management processes.

If you select 78 frags then run your job on 2 nodes using 48 cores per
node since 2 cores are required for mpiBLAST for management processes.

Since mpiBLAST uses a config file called ~/.ncbirc you should only run
one mpiBLAST job at a time.

Your ~/.ncbirc file should reflect the number of frags you are using:

Here is an example of the ~/.ncbirc file when using the 78 frag nt
database. First create a directory called
/scratch/user/Your\_NetID/tmp\_mpiblast

    [NCBI]
    Data=/scratch/datasets/mpiblast/data
    
    [BLAST]
    BLASTDB=/scratch/datasets/mpiblast/nt/78_frags
    BLASTMAT=/scratch/datasets/mpiblast/data
    
    [mpiBLAST]
    Shared=/scratch/datasets/mpiblast/nt/78_frags
    Local=/scratch/user/Your_NetID/tmp_mpiblast

If you want your mpiBLAST job to finish a lot faster, then add these
lines to your job script: (don't create the .ncbirc file, let the job
script create it for you since it will use the $TMPDIR variable at
runtime)

    echo "[NCBI]
    Data=/scratch/datasets/mpiblast/data
    
    [BLAST]
    BLASTDB=/scratch/datasets/mpiblast/nt/78_frags
    BLASTMAT=/scratch/datasets/mpiblast/data
    
    [mpiBLAST]
    Shared=/scratch/datasets/mpiblast/nt/78_frags
    Local=$TMPDIR" > ~/.ncbirc

An example of a command using the 78 frag nt database and the .ncbirc
file above would look like this:

` mpirun -np 78 mpiblast -p blastn -d nt -i my_seqs.fa -o my_output.tsv -m 9 --use-parallel-write --removedb`

And the BSUB parameters in your job script to accompany the above
example:

    #SBATCH --nodes=2
    #SBATCH --ntasks-per-node=48
    #SBATCH --cpus-per-task=1
    #SBATCH --mem=56G

If you format your own database, you can use a local copy of the blast
matricies which are found here:

` /scratch/datasets/mpiblast/data`

## BLAT

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module spider BLAT`

BLAT on DNA is designed to quickly find sequences of 95% and greater
similarity of length 25 bases or more.

## pblat-cluster

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_pblat-cluster_0.2_mpi_ada.sh)

` module spider pblat`  
` module spider OpenMPI/1.8.4-GCC-4.8.4`

This program is useful when you blat a big query file to a huge
reference like human whole genome sequence.

The program is based on the original blat program which was written by
Jim Kent.

BLAT alignments for small genomes will most likely be faster using
regular BLAT even for ~50,000 sequences.

## Exonerate

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Exonerate
[homepage](http://www.ebi.ac.uk/about/vertebrate-genomics/software/exonerate)

` module spider Exonerate`

Exonerate is a generic tool for pairwise sequence comparison.

## mrfast

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

mrfast [homepage](http://mrfast.sourceforge.net/)

` module spider mrfast`

mrFAST is a read mapper that is designed to map short reads to reference
genome with a special emphasis on the discovery of structural variation
and segmental duplications.

mrFAST maps short reads with respect to user defined error threshold,
including indels up to 4+4 bp.

NOTE: mrFAST is developed for Illumina, thus requires all reads to be at
the same length.

For paired-end reads, lengths of mates may be different from each other,
but each "side" should have a uniform length.

## DNA-seq

### bwa

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_bwa_0.7.17_samtools_1.9_sort_pe_terra.sh)

bwa [homepage](http://bio-bwa.sourceforge.net/)

` module spider BWA`

Genome indexes for bwa can be found in the ucsc directory for each
organism:

` /scratch/datasets/genome_indexes/ucsc/hg19/bwa_0.7.12_index`

Indexes created with bwa version 0.7.12 will work for bwa tool version
0.7.12+

Please contact the HPRC helpdesk help@sc.tamu.edu if you need additional
genome indexes

### GSNAP

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_gsnap_2015-09-21_se_ada.sh)

GSNAP [homepage](http://research-pub.gene.com/gmap/)

` module spider GMAP-GSNAP`

GSNAP: Genomic Short-read Nucleotide Alignment Program

### SNAP

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [ada
(pe)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_snap_0.15.4_pe_ada.sh)
[ada
(se)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_snap_0.15.4_se_ada.sh)

SNAP [homepage](http://snap.cs.berkeley.edu/)

` module spider SNAP`

SNAP is a new sequence aligner that is 3-20x faster and just as accurate
as existing tools like BWA-mem, Bowtie2 and Novoalign.

### SpeedSeq

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_speedseq_0.1.2_align_pe_ada.sh)

SpeedSeq [homepage](https://github.com/hall-lab/speedseq)

`module load SpeedSeq/0.1.2-foss-2017A-Python-2.7.12`

A flexible framework for rapid genome analysis and interpretation.

Use the following command to download your own copy of VEP builds
(canis\_familiaris\_vep used as an example)

`mkdir $SCRATCH/vep_cache`  
`$EBROOTVEP/INSTALL.pl --AUTO c --CACHEDIR $SCRATCH/vep_cache --SPECIES canis_familiaris_vep`

If you do not want to use your file and disk quota to download genome
builds, there are some builds available at the following directory:

`/scratch/datasets/VEP/vep_cache/`

Send a message to the HPRC helpdesk if you would like additional genome
builds added to this shared location.

speedseq align uses a default of 20GB of memory for sambamba sorting.
There are other concurrent processes other than the sambamba sort which
also needs memory. If your job script is running out of memory on the
64GB memory nodes, select a 256GB node using [all available
memory](/kb3/Software/Bioinformatics/Bioinformatics@FAQ/#for-a-256-gb-compute-nodes/)
and set **speedseq -M 200** It also helps to use the $TMPDIR variable in
your job script as the temporary files directory: **speedseq -T
$TMPDIR**

### BFAST

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

BFAST [homepage](http://sourceforge.net/projects/bfast/)

` module spider BFAST`

BFAST facilitates the fast and accurate mapping of short reads to
reference sequences.

### Stampy

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Stampy [homepage](http://www.well.ox.ac.uk/project-stampy)

` module spider Stampy`

Stampy is a package for the mapping of short reads from illumina
sequencing machines onto a reference genome.

It's recommended for most workflows, including those for genomic
resequencing, RNA-Seq and Chip-seq.

### LAST

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

LAST [homepage](http://last.cbrc.jp/)

` module spider LAST`

LAST finds similar regions between sequences. LAST copes more
efficiently with repeat-rich sequences (e.g. genomes).

For example: it can align reads to genomes without repeat-masking,
without becoming overwhelmed by repetitive hits.

## RNA-seq

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

### Tophat & Tophat2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_tophat_2.1.1_se_ada.sh)

TopHat [homepage](https://ccb.jhu.edu/software/tophat/index.shtml)

` module spider TopHat`  
` module spider TopHat2`

TopHat is a fast splice junction mapper for RNA-Seq reads.

It aligns RNA-Seq reads to mammalian-sized genomes using the ultra
high-throughput short read aligner Bowtie, and then analyzes the mapping
results to identify splice junctions between exons.

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

### STAR

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

STAR [homepage](https://code.google.com/p/rna-star/)

` module spider STAR`

STAR is an ultrafast universal RNA-seq aligner

Optimizing STAR for PacBio long reads
[tutorial](https://github.com/PacificBiosciences/cDNA_primer/wiki/Bioinfx-study:-Optimizing-STAR-aligner-for-Iso-Seq-data)

### GMAP

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available:
[ada](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_gmap_2015-09-21_se_ada.sh)

GMAP [homepage](http://research-pub.gene.com/gmap/)

` module spider GMAP-GSNAP`

GMAP: A Genomic Mapping and Alignment Program for mRNA and EST
Sequences.

### HISAT2

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

HISAT2 [homepage](http://ccb.jhu.edu/software/hisat2/index.shtml)

` module load HISAT2/2.0.5-intel-2015B-Python-2.7.10`

HISAT2 is a fast and sensitive alignment program for mapping
next-generation sequencing reads (both DNA and RNA) against the general
human population (as well as against a single reference genome).

If you will be using cufflinks downstream, run hisat2 with the
--dta-cufflinks option

The hisat2 index for hg19 is found here:

` /scratch/datasets/genome_indexes/ucsc/hg19/hisat2_index/grch37/`

### Subread

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Subread [homepage](http://subread.sourceforge.net/)

` module spider Subread`

Subread: an accurate and efficient aligner for mapping both genomic
DNA-seq reads and RNA-seq reads (for the purpose of expression
analysis).
