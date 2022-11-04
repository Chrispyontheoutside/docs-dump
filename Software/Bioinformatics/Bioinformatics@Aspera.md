# Aspera

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Install Aspera

SRA-Toolkit will look to see if you have Aspera installed.

The Aspera ascp command will download SRA files quicker than wget.

Run the following command from any directory. This will install
configuration files in your ~/.aspera

`/scratch/data/bio/bin/ibm-aspera-connect_4.0.2.38_linux.sh`

Then add the following to your PATH in your ~/.bash\_profile file

    PATH=$PATH:$HOME/.aspera/connect/bin

Example command: ascp -QT -l 300m -P33001 -i
$HOME/.aspera/connect/etc/asperaweb\_id\_dsa.openssh
era-fasp@fasp.sra.ebi.ac.uk:vol1/fastq/ERR315/009/ERR3155119/ERR3155119.fastq.gz
./

## Downloading 1000 genomes data

Login to an Grace data transfer node from your desktop

    ssh netid@grace-dtn1.hprc.tamu.edu

Sample command to download a fastq.gz file

    ascp -i ~/.aspera/connect/etc/asperaweb_id_dsa.openssh -QTr -l10000m \
    anonftp@ftp-trace.ncbi.nih.gov:/1000genomes/ftp/phase3/data/NA21087/sequence_read/SRR442587_1.filt.fastq.gz ./

## Uploading to SRA

Login to a fast transfer node from your desktop

`Terra: terra-ftn.hprc.tamu.edu`  
`Grace: grace-dtn1.hprc.tamu.edu or grace-dtn2.hprc.tamu.edu`

    ssh netid@grace-dtn1.hprc.tamu.edu

Sample command to upload to SRA

    time ascp -i <path/to/ncbi_key_file> -QT -l10000m -k1 -d <path/to/files/directory/> \
    subasp@upload.ncbi.nlm.nih.gov:uploads/<ncbi_account_email>_<random_code>/<submission_folder>/

The above command is used without the \< and \> which are just used to
highlight what you need to provide.

  - <path/to/ncbi_key_file> key file is provided by NCBI. must be an
    absolute path, e.g.: /home/<your_NetID>/keys/aspera.openssh

<!-- end list -->

  - <random_code> random code for upload is provided by NCBI

<!-- end list -->

  - <submission_folder> is required and will be created automatically by
    the ascp command.

Notice usage of the **time** command before the ascp command. If the
command stops at 60 minutes then your upload was not complete.

# SRA-toolkit

Used to download Sequence Read Archive files and extract into fasta
file(s).

` # on Grace`  
` module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9`

` # on Terra`  
` module load SRA-Toolkit/2.10.8-gompi-2020a`

SRA-toolkit will download files to your home directory be default and
since your home directory is limited to 10GB, you can redirect the
downloads to your scratch space by creating a directory in scratch and
making a symbolic link to that directory from your home directory.

For the newer versions of SRA-Toolkit, this is done using the vdb-config
command to configure the cache directory to a directory in your $SCRATCH
directory. You only need to run vdb-config once to set up the cache
directory. Do the following on the Grace login command prior to
submitting a job script.

    mkdir /scratch/user/YOUR_NETID/ncbi
    
    # on Grace
    module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9
    vdb-config --interactive
    
        # use letter and tab keys or mouse click to select menu items
    type c for CACHE
    type o for choose
    click [ Create Dir ] then hit enter and type /scratch/user/YOUR_NETID/ncbi
    then select OK and hit enter and hit y to select yes for the question to change the location
    then click s to save and x to exit
    
        # when you are done downloading and processing sra files, you will need to remove downloaded .sra files
        #   from the directory /scratch/user/your_netid/ncbi/sra/

The compute nodes are not connected to the internet so you will need to
add the proxy lines after loading the SRA-Toolkit module in your job
script.

</kb3/Software/Web-Proxy/SW@WebProxy/>

With the web proxy lines added to a job script, you can prefetch a .sra
file then use fastq-dump to process the .sra file. Downloading the .sra
file to $TMPDIR is a good approach since the $TMPDIR is deleted after
the job is complete. You just need to specify an output directory for
the processed fastq files.

    #!/bin/bash
    #SBATCH --export=NONE               # do not export current env to the job
    #SBATCH --job-name=fastq-dump       # job name
    #SBATCH --time=1-00:00:00           # max job run time dd-hh:mm:ss
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node
    #SBATCH --cpus-per-task=2           # CPUs (threads) per command
    #SBATCH --mem=10G                   # total memory per node
    #SBATCH --output=stdout.%x.%j          # save stdout to file
    #SBATCH --error=stderr.%x.%j           # save stderr to file
    
    # on Grace
    module load GCC/10.2.0  OpenMPI/4.0.5  SRA-Toolkit/2.10.9
    
    # enable proxy to allow compute node connection to internet
    module load WebProxy
    
    prefetch --output-directory $TMPDIR SRR575500  && \
    fastq-dump --outdir seqs -F -I --gzip $TMPDIR/SRR575500/SRR575500.sra

  - add the --split-files option to the fastq-dump command for paired
    end reads

SRA-toolkit (fast-dump) is also available in Maroon Galaxy.

Browse SRA using [SRA Explorer](https://ewels.github.io/sra-explorer/)
where you can get URLs using the 'saved datasets' feature to directly
download fastq files using wget instead of having to use SRA-toolkit.

## Install Aspera

SRA-Toolkit will look to see if you have Aspera installed. The Aspera
ascp command will download SRA files quicker than wget. Run the
installation script from any directory. This will install configuration
files in your ~/.aspera

`/scratch/helpdesk/ngs/ibm-aspera-connect-3.9.8.176272-linux-g2.12-64.sh`

Example command: ascp -QT -l 300m -P33001 -i
$HOME/.aspera/connect/etc/asperaweb\_id\_dsa.openssh
era-fasp@fasp.sra.ebi.ac.uk:vol1/fastq/ERR315/009/ERR3155119/ERR3155119.fastq.gz
./

# BioMart

## biomaRt

The biomaRt package, provides an interface to a growing collection of
databases implementing the BioMart software suite. The package enables
retrieval of large amounts of data in a uniform way without the need to
know the underlying database schemas or write complex SQL queries.

biomaRt
[userguide](http://www.bioconductor.org/packages/release/bioc/vignettes/biomaRt/inst/doc/biomaRt.html#introduction)

*Rstudio on the HPRC portal cannot be used for biomaRt since Rstudio
runs on a compute node and the compute nodes do not have internet
access*

Once you have saved your XML query from a web based BioMart interface to
a text file, use the following example to retrieve your query from
biomart.org.

Read your BioMart XML query file into R, retreive sequencees and print
output to a file:

Example of XML query saved to a text file (query.xml for example):

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE Query>
    <Query  virtualSchemaName = "default" formatter = "FASTA" header = "0" uniqueRows = "0" count = "" datasetConfigVersion = "0.6" >
                    
        <Dataset name = "mmusculus_gene_ensembl" interface = "default" >
            <Filter name = "start" value = "1"/>
            <Filter name = "chromosome_name" value = "18"/>
            <Filter name = "end" value = "5000000"/>
            <Attribute name = "peptide" />
            <Attribute name = "ensembl_gene_id" />
            <Attribute name = "ensembl_transcript_id" />
        </Dataset>
    </Query>

The biomaRt R package can be accessed using the R\_tamu module:

`module load R_tamu/3.5.0-iomkl-2017b-recommended-mt`

Start the R command line

`R`

Then on the R command line load the biomarRt library

`library(biomaRt)`

R commands to retrieve fasta sequences using the query.xml file and save
results to a file (martout.fasta in this example):

    myxml<-readLines('query.xml')
    mytxt<-paste(unlist(myxml), collapse='')
    myseqs<-getXML(xmlquery=mytxt)
    write.table(myseqs, 'martout.fasta', row.names=F, col.names=F, quote=F)

There is a warning message which can be ignored:

*Warning message:*

*Function 'getXML()' is deprecated.*

*Use 'biomaRt:::.submitQueryXML' instead*

*See help('getXML') for further details*

# Illumina BaseMount

## Basemount

Basemount is used to mount your Illumina BaseSpace account so you can
copy files directly from BaseSpace to Grace.

Install the BaseSpace executable in your $HOME/bin directory using the
following:

``` 
 mkdir $HOME/bin
 wget "https://launch.basespace.illumina.com/CLI/latest/amd64-linux/bs" -O $HOME/bin/bs
 chmod u+x $HOME/bin/bs
```

Then run the following to authenticate your BaseSpace account

`bs auth`

You will be prompted with an Illumina BaseSpace URL to complete the
authentication at the BaseSpace website.

Once you login to the Illumina BaseSpace website and allow access, you
will see a welcome message back at the terminal command line.

Example command to list your BaseSpace projects:

`bs list project`

Example command to see files (datasets) within each project:

`bs list datasets`

See the [BaseSpace CLI
examples](https://developer.basespace.illumina.com/docs/content/documentation/cli/cli-examples)
for more commands including downloading fastq files:
