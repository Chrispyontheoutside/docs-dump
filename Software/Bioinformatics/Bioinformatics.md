# Bioinformatics Tool Categories (Overview)

  - [ Sequence QC](/kb3/Software/Bioinformatics/Bioinformatics@Sequence_QC/ "wikilink")
  - [Data Normalization, Clustering &
    Collapsing](/kb3/Software/Bioinformatics/Bioinformatics@Data_Normalization.2C_Clustering_.26_Collapsing/ "wikilink")
  - [PacBio Tools](/kb3/Software/Bioinformatics/Bioinformatics@PacBio_tools/ "wikilink")
  - [Oxford Nanopore
    Tools](/kb3/Software/Bioinformatics/Bioinformatics@OxfordNanopore_tools/ "wikilink")
  - [Genome Assembly](/kb3/Software/Bioinformatics/Bioinformatics@Genome_Assembly/ "wikilink")
  - [Metagenomics](/kb3/Software/Bioinformatics/Bioinformatics@Metagenomics/ "wikilink")
  - [RNA-seq](/kb3/Software/Bioinformatics/Bioinformatics@RNA-seq/ "wikilink")
  - [ChIP-seq](/kb3/Software/Bioinformatics/Bioinformatics@ChIP-seq/ "wikilink")
  - [Sequence Variants (SNPs and
    indels)](/kb3/Software/Bioinformatics/Bioinformatics@Sequence_Variants/ "wikilink")
  - [CNV](/kb3/Software/Bioinformatics/Bioinformatics@CNV/ "wikilink")
  - [Methylation](/kb3/Software/Bioinformatics/Bioinformatics@Methylation/ "wikilink")
  - [Sequence Alignments](/kb3/Software/Bioinformatics/Bioinformatics@Sequence_Alignments/ "wikilink")
  - [Multiple Sequence
    Alignments](/kb3/Software/Bioinformatics/Bioinformatics@Multiple_Sequence_Alignments/ "wikilink")
  - [Proteomics](/kb3/Software/Bioinformatics/Bioinformatics@Proteomics/ "wikilink")
  - [Population Genomics](/kb3/Software/Bioinformatics/Bioinformatics@Population_Genomics/ "wikilink")
  - [Phylogenetics](/kb3/Software/Bioinformatics/Bioinformatics@Phylogenetics/ "wikilink")
  - [Genotyping](/kb3/Software/Bioinformatics/Bioinformatics@Genotyping/ "wikilink")
  - [Gene Networks](/kb3/Software/Bioinformatics/Bioinformatics@Gene_Networks/ "wikilink")
  - [Chromatin Structure](/kb3/Software/Bioinformatics/Bioinformatics@Chromatin_structure/ "wikilink")
  - [Software Suites](/kb3/Software/Bioinformatics/Bioinformatics@Software_Suites/ "wikilink")
  - [Common Tools](/kb3/Software/Bioinformatics/Bioinformatics@Common_Tools/ "wikilink")
  - [Data Visualization](/kb3/Software/Bioinformatics/Bioinformatics@Data_Visualization/ "wikilink")
  - [Statistics](/kb3/Software/Bioinformatics/Bioinformatics@Statistics/ "wikilink")
  - [File Format Tools](/kb3/Software/Bioinformatics/Bioinformatics@File_Format_Tools/ "wikilink")
  - [Licenses](/kb3/Software/Bioinformatics/Bioinformatics@Licenses/ "wikilink")
  - [Aspera (SRA, 1000genomes,
    BioMart)](/kb3/Software/Bioinformatics/Bioinformatics@Download_data/ "wikilink")
  - [Conda/Bioconda](/kb3/Software/Bioinformatics/Bioinformatics@Conda_Bioconda/ "wikilink")
  - [Biocontainers](/kb3/Software/Bioinformatics/Bioinformatics@Biocontainers/ "wikilink")
  - [FAQ](/kb3/Software/Bioinformatics/Bioinformatics@FAQ/ "wikilink")

***This is a summary of most of the NGS Bioinformatics tools on the HPRC
clusters.***

***Not all NGS Bioinformatics tools installed on each HPRC cluster are
summarized on these pages.***

***A complete software module listing for each cluster can be found
here:***

  - [Grace Module List](https://hprc.tamu.edu/software/grace)
  - [Terra Module List](https://hprc.tamu.edu/software/terra)

***Other software installed as a conda environment and not as a module
can be found with the following two commands***

`module load Anaconda/3-5.0.0.1`  
`conda env list`

***Check the website of the software package you want to use to see if
the version on the HPRC cluster is the latest available version and
advise us if a newer version needs to be installed.***

# Genome Fasta, Index Files and Databases

The following genomes are available on Ada and can be accessed via the
command line.

The idea is that you link to these files in your job script instead of
copying the files to your directories.

| Genomic Reference Sequences, Indexes and Databases                                                     ||
| :----------------------------------------------------------------------------------------------------- | :---------------------------------|
| All of NCBI's [BLAST5 databases](ftp://ftp.ncbi.nlm.nih.gov/blast/db/) (nt, nr, rna, 16SMicrobial,...) |/scratch/data/bio/blast/|
| The latest [UCSC Genomes](https://genome.ucsc.edu/FAQ/FAQreleases.html)                                |/scratch/data/bio/ucsc/gbdb/|
| [BUSCO](/kb3/Software/BUSCO/SW@BUSCO/) lineage files                               |/scratch/data/bio/busco4/ &emsp;&emsp;&emsp; scratch/data/bio/busco5/|             
| [Silva](https://www.arb-silva.de/) database files                                                      |	/scratch/data/bio/silva/|
| CESM                                                                                                   |/scratch/data/bio/cesm/ |
| [Gemini](/kb3/Software/Gemini/SW@Gemini/)                                          |/scratch/data/bio/gemini/ |
| Augustus species                                                                                       |$EBROOTAUGUSTUS/config/species/&emsp;&emsp;&emsp;(after loading AUGUSTUS module)|
| Bowtie, Bowtie2 and BWA indexed genomes\*                                                              |/scratch/data/bio/genome_indexes/|                                                                                                     

\* bowtie indexes will work with any version of the bowtie tool but will
not work with the bowtie2 tool  
\* bowtie2 indexes will work with any version of the bowtie2 tool but
will not work with the bowtie tool  

# Bioinformatics Web Resources

<table border="1" cellpadding="6" style="border-collapse: collapse;">
<tbody><tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">General Tutorials
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://cvw.cac.cornell.edu/topics">Tutorials</a></td>
<td>Cornell Virtual Workshop
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Genomic Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ncbi.nlm.nih.gov/">NCBI</a></td>
<td>National Center for Biotechnology Information
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://useast.ensembl.org/index.html?redirect=no">Ensembl</a></td>
<td>Provides a bioinformatics framework to organise biology around the sequences of large genomes.
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ebi.ac.uk/">EBI</a></td>
<td>The European Bioinformatics Institute
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://jgi.doe.gov/">JGI</a></td>
<td>Genome sequences of plants, fungi, microbes, and metagenomes
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ddbj.nig.ac.jp/">DDBJ</a></td>
<td>DNA Data Bank of Japan
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.genome.gov/ENCODE/">ENCODE</a></td>
<td>ENCyclopedia Of DNA Elements
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://hapmap.ncbi.nlm.nih.gov/">HapMap</a></td>
<td>Identify and catalog genetic similarities and differences in human beings
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://gold.jgi.doe.gov/">GOLD</a></td>
<td>Genomes Online Database: information regarding genome and metagenome sequencing projects
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://david.ncifcrf.gov/">DAVID</a></td>
<td>The Database for Annotation, Visualization and Integrated Discovery
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.girinst.org/">RepBase</a></td>
<td>Genetic Information Research Institute. RepBase: repetitive sequences database
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Gene Nomenclature and Info
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.genenames.org/">HGNC</a></td>
<td>A curated online repository of HGNC-approved gene nomenclature.
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.genecards.org/">GeneCards</a></td>
<td>Information on all annotated and predicted human genes
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Sequencing Projects
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://hmpdacc.org/">HMP</a></td>
<td>Human Microbiome Project: characterizes microbial communities found at multiple human body sites
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.1000genomes.org/">1000 Genomes</a></td>
<td>A Deep Catalog of Human Genetic Variation
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.uk10k.org/">UK10K</a></td>
<td>Rare Genetic Variants in Health and Disease
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Protein Sequence Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ebi.ac.uk/interpro/">InterPro</a></td>
<td>Protein sequence analysis &amp; classification
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.rcsb.org/pdb/home/home.do">PDB</a></td>
<td>Protein Data Bank
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://pfam.xfam.org/">Pfam</a></td>
<td>A large collection of protein families
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.uniprot.org/">UniProt</a></td>
<td>Protein sequences and functional information
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Download Sequence Data
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://useast.ensembl.org/biomart/martview/4395b113a068c80904abb8acf52c221a">BioMart</a></td>
<td>Specific gene regions, Gene Ontology and Alternate IDs
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://useast.ensembl.org/info/data/ftp/index.html">Ensembl</a></td>
<td>cDNA, GTF, VEP, CDS, Protein
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://support.illumina.com/sequencing/sequencing_software/igenome.html">iGenome</a></td>
<td>Ensembl, NCBI, UCSC reference fasta; Bowtie, BWA and Bowtie2 index files
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">RNA Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.mirbase.org/">miRBase</a></td>
<td>A searchable database of published miRNA sequences and annotation
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://rdp.cme.msu.edu/">RDP</a></td>
<td>Aligned and annotated Bacterial and Archaeal 16S rRNA sequences, and Fungal 28S rRNA sequences
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.arb-silva.de/">SILVA</a></td>
<td>A comprehensive on-line resource for quality checked and aligned ribosomal RNA sequence data
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Gene Expression Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.ebi.ac.uk/gxa/home">Expression Atlas</a></td>
<td>EBI Expression Atlas
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://hive.biochemistry.gwu.edu/bioxpress">BioXpress</a></td>
<td>gene expression in cancer
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.emouseatlas.org/emage/home.php">EMAGE</a></td>
<td>Mouse embryo in situ gene expression data
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.proteinatlas.org/">Human Protein Atlas</a></td>
<td>Human protein-coding genes regarding the expression based on both RNA and protein data
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://plantgdb.org/prj/PLEXdb">PLEXdb</a></td>
<td>Gene expression in diverse organs, tissues, or developmental stages
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Metabolic Pathway Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.kegg.jp/">KEGG</a></td>
<td>A database resource for understanding high-level functions and utilities of the biological system
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.reactome.org/">Reactome</a></td>
<td>A curated and peer reviewed pathway database
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.genenetwork.org/webqtl/main.py">GeneNetwork</a></td>
<td>Tools used to study complex networks of genes, molecules, gene function and phenotypes
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Model Organism Databases
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.arabidopsis.org/">TAIR</a></td>
<td>The <i>Arabidopsis</i> Information Resource
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://candidagenome.org/">CGD</a></td>
<td><i>Candida</i> Genome Database
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://flybase.org/">FlyBase</a></td>
<td>A Database of <i>Drosophila</i> Genes &amp; Genomes
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.gramene.org/">Gramene</a></td>
<td>Comparative functional genomics in crops and model plant species
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.maizegdb.org/">MaizeGDB</a></td>
<td><i>Zea mays</i> database
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.informatics.jax.org/">MGI</a></td>
<td>International database resource for the laboratory mouse
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://rgd.mcw.edu/">RGD</a></td>
<td>Rat Genome Database
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.yeastgenome.org/">Saccharomyces</a></td>
<td>Comprehensive integrated biological information for the budding yeast <i>Saccharomyces cerevisiae</i>
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.vectorbase.org/">VectorBase</a></td>
<td>Bioinformatics Resource for Invertebrate Vectors of Human Pathogens
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.wormbase.org/#01-23-6">WormBase</a></td>
<td>Nematodes
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.xenbase.org/entry/">Xenbase</a></td>
<td><i>Xenopus</i> Database
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://zfin.org/">ZFIN</a></td>
<td>The Zebrafish Model Organism Database
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Genome Browsers
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://genome.ucsc.edu/cgi-bin/hgGateway">UCSC</a></td>
<td>
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.ncbi.nlm.nih.gov/genome/gdv/">Genome Data Viewer</a></td>
<td>NCBI genome browser for 600+ RefSeq genome assemblies
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://useast.ensembl.org/index.html">Ensembl</a></td>
<td>
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Forums and Techniques
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.rna-seqblog.com/">RNA-Seq Blog</a></td>
<td>Blog on the latest RNA-seq experimental design and analysis techniques
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.seqanswers.com/">SeqAnswers</a></td>
<td>Forums on everything Bioinformatics
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.biostars.org/">BioStar</a></td>
<td>Forums on everything Bioinformatics
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://genohub.com/resources/">Genohub</a></td>
<td>Designing your Next Generation Sequencing Run
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://genohub.com/recommended-sequencing-coverage-by-application/">Genohub</a></td>
<td>Coverage and Read Depth Recommendations by Sequencing Application
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Software and Database Lists
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ncbi.nlm.nih.gov/guide/all/#databases_">NCBI</a></td>
<td>Databases available at NCBI
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ncbi.nlm.nih.gov/guide/all/#tools_">NCBI</a></td>
<td>Tools available at NCBI
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.expasy.org/proteomics">ExPASy</a></td>
<td>Bioinformatics Resource Portal
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.oxfordjournals.org/our_journals/nar/database/cap/">NAR</a></td>
<td>Nucleic Acids Research, published papers on databases
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Bioinformatics Web Tutorials
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://nihlibrary.nih.gov/Services/Bioinformatics/Pages/Biotutorials.aspx">NCBI</a></td>
<td>NIH Online Bioinformatics Tutorials
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ebi.ac.uk/training/online/">EMBL-EBI</a></td>
<td>Train online with EMBL-EBI (Home)
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ebi.ac.uk/training/online/course/ebi-next-generation-sequencing-practical-course">EMBL-EBI</a></td>
<td>Train online with EMBL-EBI (Next Generation Sequencing Practical Course)
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="http://www.ensembl.org/info/website/tutorials/index.html">Ensembl</a></td>
<td>Ensembl Tutorials and Worked Examples
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://datacarpentry.org/wrangling-genomics">Data Carpentry</a></td>
<td>Genomics (QC, trim, call variants)
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://www.melbournebioinformatics.org.au/tutorials/tutorials/">Melbourne Bioinformatics</a></td>
<td>A few good tutorials including some for Galaxy
</td></tr>
<tr>
<th colspan="2" style="background-color: #BCC6CC;" align="left">Other Useful Tools
</th></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://broadinstitute.github.io/picard/explain-flags.html">SAM Flags</a></td>
<td>Explain SAM/BAM bitwise flags
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://ewels.github.io/sra-explorer/">SRA Explorer</a></td>
<td>Explore SRA by SRA/GEO id, organism, seq type, tissue type, ...
</td></tr>
<tr>
<td><a rel="nofollow" class="external text" href="https://snp-nexus.org/">SNPnexus</a></td>
<td>Web-based annotation of human SNPs
</td></tr>
</tbody></table>