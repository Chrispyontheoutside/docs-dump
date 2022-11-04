# NGS: Software Suites

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Ensembl-API

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

The Ensembl API is available by loading the following modules:

    module load ensembl/94-GCCcore-6.3.0-Perl-5.24.0
    module load ensembl-io/94-GCCcore-6.3.0-Perl-5.24.0
    module load ensembl-compara/94-GCCcore-6.3.0-Perl-5.24.0
    module load ensembl-funcgen/94-GCCcore-6.3.0-Perl-5.24.0
    module load ensembl-variation/94-GCCcore-6.3.0-Perl-5.24.0

See the Ensembl Core API
[Tutorial](https://useast.ensembl.org/info/docs/api/core/core_tutorial.html)
for usage.

## EMBOSS

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

` module spider EMBOSS`

EMBOSS [homepage](http://emboss.sourceforge.net/)

## UCSCtools

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

List of tools and usages found
[here](ftp://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/FOOTER.txt)

` module spider UCSCtools`

## DART

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

DART [homepage](http://biowiki.org/DART)

` module spider DART`

For DART applications requiring Java, Perl or Python, you will need to
load an appropriate version that matches the DART goolf toolchain:

` module load Java/1.8.0_66`  
` module load Python/2.7.10-goolf-1.7.20`  
` module load Perl/5.20.0-goolf-1.7.20`

The DART library includes a number of bioinformatics programs,
including: stemloc for RNA alignment; xrate for phylo-grammars;
phylocomposer, handalign and other statistical alignment programs in the
Handel package; and more.

The programs use statistical algorithms (MCMC, EM, etc.) to impute
multiple alignments, annotations and other unseen evolutionary
parameters from sequence data.

## PLINK

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

PLINK [homepage](http://pngu.mgh.harvard.edu/~purcell/plink/)

` module spider PLINK`

PLINK is a free, open-source whole genome association analysis toolset,
designed to perform a range of basic, large-scale analyses in a
computationally efficient manner.

## PLINK 1.9

[Plink v1.9](https://www.cog-genomics.org/plink2) is still beta and
being updated frequently so it is best not to add to the HPRC clusters
as a module.

There is a precompiled Linux 64-bit (Stable (beta 6.8, 15 Feb) or newer)
binary version available that you can download and add to your $PATH.

Version 1.9 will change frequently since it is still beta so you should
review your results files and check their website and download the
latest version as needed.

## Gemini

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

Gemini [homepage](http://gemini.readthedocs.org/en/latest/index.html)

` module spider Gemini`

GEMINI (GEnome MINIng) is a flexible framework for exploring genetic
variation in the context of the wealth of genome annotations available
for the human genome.

Gemini Data is saved here:

` /scratch/datasets/Gemini`

## GenHub

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: no

GenHub [homepage](https://github.com/standage/genhub)

GenHub is a free open-source software framework for analyzing eukaryotic
genomes, computing and reporting a variety of statistics reflecting
genome content and organization.

    module load GenomeTools/1.5.9-intel-2015B
    module load AEGeAn/0.15.2-intel-2015B
    module load CD-HIT/4.6.6-intel-2015B
    module load pandas/0.17.0-intel-2015B-Python-2.7.10
    module swap Python python/2.7.6-generic

## CGAT

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [yes (bam files,
bam
stats)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/ada/run_cgat_bam2stats_ada.sh)

CGAT
[homepage](https://www.cgat.org/downloads/public/cgat/documentation/)

Use the following command to find a CGAT version to load using the
'module load' command

` module spider CGAT`

CGAT is a collection of tools for the computational genomicist written
in the python language.

To use CGAT you need to load the CGAT environment:

` source $CGAT_ACTIVATE cgat-scripts`

When your processing is finished, you need to unload the CGAT
environment:

` source deactivate`

The following CGAT tools are available in the CGAT package

``` 
                                          gff2bed             
bam2bam              chain2psl            gff2coverage        
bam2bed              chain2stats          gff2fasta           
bam2fastq            diff_bam             gff2gff             
bam2geneprofile      diff_bed             gff2histogram       
bam2peakshape        diff_chains          gff2psl             
bam2stats            diff_fasta           gff2stats           
bam2wiggle           diff_gtf             gtf2fasta           
bam_vs_bam           fasta2bed            gtf2gff             
bam_vs_bed           fasta2fasta          gtf2gtf             
bam_vs_gtf           fasta2kmercontent    gtf2table           
bed2bed              fasta2table          gtf2tsv             
bed2fasta            fasta2variants       gtfs2tsv            
bed2gff              fastas2fasta         index_fasta         
bed2stats            fastq2fastq          split_gff           
bed2table            fastq2table          vcf2vcf             
beds2beds            fastqs2fasta         version             
beds2counts          fastqs2fastqs
```

### with user(s) on the same Galaxy instance

**User with History to share:**

Click 'History options' -\> 'Share or Publish'

Select "Share with another user" and enter the Galaxy users full email
address.

**User receiving shared history:**

Click 'History options' -\> 'Histories Shared with Me'

Check the box for the history you want to copy to your list of Histories
and click Copy.

Then click the 'View all Histories' icon in the right panel to see the
shared history in your list of histories.

## Manage your HPRC Accounts

There are a number of different types of tools that are configured to
require different amounts of SUs.

Here is how SUs are calculated:

    Max runtime      Cores       Calculation                    Required SUs
      1 day            1        24 hrs * 1 day  *  1 core     =      48
      1 day           48        24 hrs * 1 day  * 48 cores    =    1152
      3 days          48        24 hrs * 3 days * 48 cores    =    3456
      7 days          48        24 hrs * 7 days * 48 cores    =    8064

If a tool does not state how many SUs it requires, then it is most
likely configured to use 1 core for 1 day (24 SUs). If you are unsure of
how many SUs the tool requires, run your "My HPRC SU balance" tool
before you submit a job and then run it again after the job starts
running. You will be able to see how many SUs were charged to your
account.

Using the following HPRC SU balance as an example, if you have two
accounts and one is configured as the default (as indicated by Y in the
default column), the SUs will only be taken from the account with Y in
the Default column:

**Starting balance example:**

    =====================================================================
                    List of users's Project Accounts
    ---------------------------------------------------------------------
    |  Account   | Default | Allocation |Used & Pending SUs|   Balance  |
    ---------------------------------------------------------------------
    |000000000001|        Y|     5000.00|              0.00|     5000.00|
    |000000000002|        N|     5000.00|              0.00|     5000.00|
    ---------------------------------------------------------------------

After submitting a job that requires 1440 SUs and the job starts
running, your balance will look like this:

    =====================================================================
                    List of users's Project Accounts
    ---------------------------------------------------------------------
    |  Account   | Default | Allocation |Used & Pending SUs|   Balance  |
    ---------------------------------------------------------------------
    |000000000001|        Y|     5000.00|          -1440.00|     3560.00|
    |000000000002|        N|     5000.00|              0.00|     5000.00|
    ---------------------------------------------------------------------

Now if you submit two more jobs that require 1440 SUs, then your balance
will look like this once the jobs start running

    =====================================================================
                    List of users's Project Accounts
    ---------------------------------------------------------------------
    |  Account   | Default | Allocation |Used & Pending SUs|   Balance  |
    ---------------------------------------------------------------------
    |000000000001|        Y|     5000.00|          -4320.00|      680.00|
    |000000000002|        N|     5000.00|              0.00|     5000.00|
    ---------------------------------------------------------------------

Now you should not submit any more jobs that require 1440 SUs since your
default account only has 680 SUs.

If you need to submit more 1440 SU jobs, then you will need to change
your default account to your other account that has a balance of 5000
SUs.

If you do not change your default and try to submit a 1440 SU job and
you only have 680 SUs in your default account, then your job will remain
in a queued state and will never run. It will get stopped if Galaxy is
restarted but otherwise, you will have to stop the job.

If your three 1440 SU jobs complete early, after 1 day for example, then
you will be reimbursed for the unused 2 days (960 SUs per job) for each
of the three jobs and your HPRC SU balance will look like this:

``` 

=====================================================================
                List of users's Project Accounts
---------------------------------------------------------------------
|  Account   | Default | Allocation |Used & Pending SUs|   Balance  |
---------------------------------------------------------------------
|000000000001|        Y|     5000.00|          -1440.00|     3560.00|
|000000000002|        N|     5000.00|              0.00|     5000.00|
---------------------------------------------------------------------
```

You can now use the default account if you want to run a job that
requires 1440 SUs since the balance has increased to greater than 1440
SUs.
