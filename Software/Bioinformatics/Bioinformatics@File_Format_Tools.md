# NGS: File Format Tools

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Get Chromosome Lengths

Connect to UCSC database and get lengths from their file:

    module load UCSCtools/2021.08.21
    fetchChromSizes hg19 > hg19.len

Alternately, you can get sizes without having to download a UCSC genome
build:

    module load UCSCtools/2021.08.21
    faSize -detailed -tab genome.fasta > genome.len

## Split fasta file into multiple files

Example of splitting a fasta file named myseqs.fa into 100 files

    module load UCSCtools/2021.08.21
    faSplit sequence myseqs.fa 100 prefix 

## Create gtf file from UCSC table

Create a ~/.hg.conf file in your home directory with the following
contents:

    db.host=genome-mysql.cse.ucsc.edu
    db.user=genomep
    db.password=password
    central.db=hgcentral

Then load the UCSC tools module

` module load UCSCtools`

Run the genePredToGtf command on the gene prediction set you want. Here
are some sample commands for gene sets refGene and knownGene:

` genePredToGtf mm10 refGene mm10_ucsc_refGene.gtf`  
` genePredToGtf mm10 knownGene mm10_ucsc_knownGene.gtf`

## Validate gff file

on Grace

`module load GCC/9.3.0  GenomeTools/1.6.2`  
`gff3validator  my_file.gff3`

## Change sequence file format

### gff3 to gtf

Grace:

    module load GCC/8.3.0 OpenMPI/3.1.4 Cufflinks/2.2.1
    gffread my.gff3 -T -o my.gtf

See [GFF utilities](http://ccb.jhu.edu/software/stringtie/gff.shtml)

### gtf to gff3

Grace:

    module load GCC/8.3.0 OpenMPI/3.1.4 Cufflinks/2.2.1
    gffread my.gtf -E -o my.gff3

### bam to fastq or fasta

For single end fastq file output, use BamTools (Grace):

` module load GCC/9.3.0  BamTools/2.5.1`  
` bamtools convert -in in.bam -format `**`fastq`**` | gzip > out.fastq.gz`  
  
` bamtools convert -in in.bam -format `**`fasta`**` | gzip > out.fasta.gz`

For paired end fastq files output, use picard
[SamToFastq](https://broadinstitute.github.io/picard/command-line-overview.html#SamToFastq)

` module spider picard`

### re-pair paired end reads in two file

This can be used after trimming if the resulting trimmed files are not
properly paired and do not have the same number of reads in each file.

Grace:

`module load iccifort/2020.1.217  BBMap/38.87`  
`repair.sh in=input_R1.fastq in2=input_R2.fastq out=repaired_R1.fastq out2=repaired_R2.fastq outs=unpaired_sings.fastq`

### interleave two paired end files

This works with either fastq or fasta formatted files

`module load Seqtk/1.2-intel-2015B`  
`seqtk mergepe reads_P1.fastq reads_P2.fastq > interleaved_reads.fastq`

### de-interleave a paired end file

This works with either fastq or fasta formatted files

Grace:

`module load iccifort/2020.1.217  BBMap/38.87`  
`reformat.sh in=interleaved_reads.fastq out1=reads_R1.fastq out2=reads_R2.fastq`

### Fastq to Fasta

Seqtk accepts .fastq.gz or .fastq file input format

Grace:

` module load GCC/9.3.0  seqtk/1.3`  
` seqtk seq -A in.fastq.gz > out.fasta`

Or for saving in .fasta.gz format

` seqtk seq -A in.fastq.gz | gzip > out.fasta.gz`

### Fastq to Fasta with filter min length

Input fastq file and keep only reads longer than 10000 saved to a fasta
file

    awk 'BEGIN {OFS = "\n"} {header = $0 ; getline seq ; getline qheader ; getline qseq ; \
    if (length(seq) >= 10000) {print ">"header, seq}}' < input_reads.fastq > filtered_gt10kb.fasta

## Reformat & Filter using sed & awk

#### Delete the first line of a file

    sed -i '1d' file_name

### FASTQ

#### Add /1 or /2 at end of Fastq headers

Change the original file using "sed -i" instead of making a copy

    sed -i '1~4 s/$/\/1/g' my_file_R1.fastq
    
    sed -i '1~4 s/$/\/2/g' my_file_R2.fastq

If your fastq files are gzipped then create a new gzipped file for each
read file with \\1 or \\2 in the header

    zcat my_file_R1.fastq.gz | sed '1~4 s/$/\/1/g' | gzip > my_new_file_R1.fastq.gz
    
    zcat my_file_R2.fastq.gz | sed '1~4 s/$/\/2/g' | gzip > my_new_file_R2.fastq.gz

#### Count bases in Fastq file

    awk 'BEGIN{sum=0;}{if(NR%4==2){sum+=length($0);}}END{print sum;}' sequences.fastq

If your file is gzipped

    zcat sequences.fastq.gz | awk 'BEGIN{sum=0;}{if(NR%4==2){sum+=length($0);}}END{print sum;}'

#### Fastq filter min length

Input fastq file and select reads longer than a minimum length of 10000
and save results to a fastq format file

    awk 'BEGIN {OFS = "\n"} {header = $0 ; getline seq ; getline qheader ; getline qseq ; \
    if (length(seq) >= 10000) {print header, seq, qheader, qseq}}' < input.fastq > filtered_gt10kb.fastq

#### Fastq filter specifying length range

Input fastq file and select reads longer than a minimum length of 10000
and a maximum of 20000 and save results to a fastq format file

    awk 'BEGIN {OFS = "\n"} {header = $0 ; getline seq ; getline qheader ; getline qseq ; \
    if (length(seq) >= 10000 && length(seq) <= 20000) {print header, seq, qheader, qseq}}' < input.fastq > filtered_10kb-20kb.fastq

## SAMtools tips

### Calculate genome coverage from bam

`samtools depth my.bam | awk '{sum+=$3} END { print "Average = ",sum/NR}'`

### Genome size from bam header

` samtools view -H my.bam | grep -P '^@SQ' | cut -f 3 -d ':' | awk '{sum+=$1} END {print sum}'`

### Add MD tags

` samtools calmd -b <my.bam> <ref_genome.fasta> > my_md.bam`

## PacBio

[fileformats](https://pacbiofileformats.readthedocs.io/en/5.1/)

## Java Command options

### picard

Raise the maximum memory usage to 225 GB for the picard java process
using the java -Xmx option:

    module load picard/2.21.6-Java-11
    java -Xmx225g -jar $EBROOTPICARD/picard.jar SortSam INPUT=in.sam OUTPUT=out_sorted.bam SORT_ORDER=coordinate TMP_DIR=$TMPDIR

Use multithreading in the java code if any part of the java process can
utilize multiple threads.

`java -XX:ParallelGCThreads=20 jarfile.jar`

## UNIX and Job Script Tips

### bash aliases

Here are some useful Slurm aliases you can add to your .bashrc file

#### view all your running jobs

add the following line to your ~/.bashrc

    alias q='squeue --format="%.18i %.9P %.50j %.8u %.8T %.10M %.9l %.6D %R" -u $USER'

#### view CPU utilization for all your running jobs

add the following line to your ~/.bashrc

    alias p='pestat -u $USER'

#### list directory contents newest first

    alias lss='ls -lsth'
    alias lsh='ls -lsth | head'
    alias lshh='ls -lsth | head -20'
