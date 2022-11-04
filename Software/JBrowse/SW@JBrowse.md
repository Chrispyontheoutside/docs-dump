# JBrowse

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no, JBrowse is
only available at the HPRC Portal

JBrowse is a fast, scalable genome browser built completely with
JavaScript and HTML5.

JBrowse is available on the Terra [portal](https://portal.hprc.tamu.edu)

You will need to index the genome fasta file prior to loading the genome
file in JBrowse.

To do this, you will need to go to the Terra Unix command line and index
the fasta reference file using samtools which will create a .fai index
file

    module load SAMtools/1.9-intel-2018b
    samtools faidx reference_genome.fasta

  - Then you start JBrowse in the portal (under the Interactive Apps
    section) selecting the Number of hours and Number of cores as
    needed.

<!-- end list -->

  - Select 'Open Sequence File' and click the 'Select Files...' button
    in the 'Local files' section (files that are located on Terra)

<!-- end list -->

  - Load the reference\_genome.fasta and the reference\_genome.fasta.fai
    at the same time in JBrowse.

<!-- end list -->

  - Then you can add tracks (gff, bam, ...) by selecting Track in the
    JBrowse right panel at the top.

<!-- end list -->

  - All files that you add as tracks or genomes must be located on
    Terra. URLs are not supported since JBrowse on the
    portal.hprc.tamu.edu runs on the compute nodes which do not have
    internet access.

<!-- end list -->

  - Remember to delete the interactive session when you are finished.
