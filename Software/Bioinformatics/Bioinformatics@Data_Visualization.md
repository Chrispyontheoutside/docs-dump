# Data Visualization

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## JBrowse

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

## IGV

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

IGV [homepage](https://www.broadinstitute.org/igv/)

The Integrative Genomics Viewer (IGV) is a high-performance
visualization tool for interactive exploration of large, integrated
genomic datasets. It supports a wide variety of data types, including
array-based and next-generation sequence data, and genomic annotations.

IGV is best viewed using the HPRC portal.

  - Open your favorite web browser and go to
    [portal.hprc.tamu.edu](https://portal.hprc.tamu.edu)
  - Log in using your NetID and password
  - Select 'Interactive Apps'
  - Select 'IGV'
  - Adjust the 'Number of hours' as needed.
  - Increase the 'Number of processors' to 20 for viewing large genomes
  - Click the blue 'Launch' button
  - Wait for your job to start and then click the the blue 'Launch noVNC
    in New Tab' button when it appears.
  - Navigate within IGV to find preconfigured genomes at
    /scratch/datasets/IGV
  - You can add your own genomes by creating a .fai index for your fasta
    file using samtools on the command line before launching IGV
      - module load SAMtools
      - samtools faidx my\_genome.fasta
  - When you are finished using IGV, click the red 'Delete' button in
    the 'My Interactive Sessions' section to stop the IGV job.

## Circos

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Circos [homepage](http://circos.ca/)

Circos is a software package for visualizing data and information. It
visualizes data in a circular layout — this makes Circos ideal for
exploring relationships between objects or positions.

` module load Circos/0.69-9-GCCcore-9.3.0`

Sample config files are found here:

` ls $EBROOTCIRCOS/etc`

Sample command:

` circos -conf main.conf -outputfile genome_image.png`

The svg image output format may turn out better than the png format.

Circos is also available in [Maroon
Galaxy](/kb3/Software/Galaxy/SW@Galaxy/)

## MultiQC

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

MultiQC [homepage](http://multiqc.info/)

    module load MultiQC/1.5-intel-2017A-Python-2.7.12

After you load the MultiQC module and run multiqc, you can view the html
page using the HPC portal at
[portal.hprc.tamu.edu](https://portal.hprc.tamu.edu/)

An example command for viewing multiple FastQC processed samples in
MultiQC where the output\_dir contains the FastQC report files ending in
\_fastqc.zip and \_fastqc.html. You can use any directory name for the
output\_dir

    multiqc output_dir

Go to [portal.hprc.tamu.edu](https://portal.hprc.tamu.edu/) and click
the Files menu item and then click your scratch directory:

` `![`   600px   |   Center   |   Portal 
 Files`](Ood_files.png " 600px | Center | Portal Files")

Then navigate the files to find and select your multiqc\_report.html
file and then click the View button:

` `![`   600px   |   Ceter   |   Portal 
 View`](Ood_view.png " 600px | Ceter | Portal View")

Here is an example page of viewing a MultiQC report for FastQC output
files (2 samples) in the portal.hprc.tamu.edu:

` `![`   600px   |   Center   |   View   HTML 
 page`](Ood_multiqc.png " 600px | Center | View HTML page")
