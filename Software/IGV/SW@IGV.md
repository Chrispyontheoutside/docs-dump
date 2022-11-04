# IGV

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
