# Galaxy

## Maroon Galaxy Accounts

The new Maroon Galaxy (v21.01) on Grace is available to students,
faculty and staff for research use.

See the Maroon Galaxy usage
[slides](https://hprc.tamu.edu/files/training/HPRC_Maroon_Galaxy.pdf)

Before you request an account on Maroon Galaxy, you must do the
following:

  - Go to [usegalaxy.org](http://usegalaxy.org) and get familiar with
    Galaxy. You can start with a free account and learn about Galaxy
    tools.

<!-- end list -->

  - Request a Grace Maroon Galaxy account only if you have data to
    analyze, otherwise use [usegalaxy.org](https://usegalaxy.org) Galaxy
    for training and practice.

<!-- end list -->

  - If you decide that Galaxy is a good choice for your research project
    then do the following
      - Establish an HPRC account by sending a request. See the
        [NewUser](https://hprc.tamu.edu/user_services/new_user_information.html)
        page for details on how to request an account.
      - After you have your HPRC account approved, send an email to
        help@hprc.tamu.edu requesting an account on Maroon Galaxy
      - Send us information on what type of data you will be analyzing
        and which tools you expect to use for your research project.

If you are off campus then you will have to install and run the [TAMU
VPN](https://u.tamu.edu/KB0010938) to connect to Maroon Galaxy.

Maroon Galaxy can be accessed using your favorite web browser such as
Firefox, Chrome or IE.

<https://galaxy-grace.hprc.tamu.edu/maroon>

## Silver Galaxy

Silver Galaxy (v20.09) is available on the HPRC Terra cluster and was
used as a temporary Galaxy until the new Galaxy became available on
Grace.

## Set Your Default Account

Use the HPRC *My HPRC SU Balance* tool. If you are unable to use the
tool, you are either out of SUs or need to
[renew](https://hprc.tamu.edu/apply) your HPRC account.

You can also check your Grace SU balance at the Grace
[portal](https://portal-grace.hprc.tamu.edu/pun/sys/OOD-Dashboard)

## Data Security

If you have restricted access data then you should not be using Galaxy.

Read the Galaxy privacy
[notice](https://docs.galaxyproject.org/en/latest/admin/cluster.html#submitting-jobs-as-the-real-user)

## Account Security

Do not share your Galaxy account with anyone. Galaxy uses the TAMU
Central Authentication Service which is linked to your TAMU account.

Make sure you always logout of Galaxy by selecting User -\> Logout and
then click the Logout button on the next screen and then close your
browser when you are finished using Galaxy.

## Permanently Delete unwanted files

In order to free disk space, you should permanently delete files that
you have already deleted from the history.

Please make this part of your Galaxy work routine in order to free up
disk space.

This is a two step process.

1\. Click the X on the history item you want deleted.

2\. At the top of the history panel, you will see a link to
<u>deleted</u> files. Click that link and then select "Permanently
remove it from disk" for the history item that you want removed

Alternative method to permanently delete all deleted files at once:

1\. Click the X on the history items you want deleted.

2\. Click the 'History options' gear icon and select 'Purge Deleted
Datasets' which will permanently delete all deleted datasets for the
current history.

## Download all files in a history

Click the gear icon and select 'Export History to File'

Then select 'to a remote file' and select 'Click to select directory'
and select 'FTP Directory'

Then give it a name ending with .tar.gz and click 'Export'

This will create a tar.gz file in your Galaxy FTP directory which you
can download. See the "Downloading Files \> 2GB via FTP from Maroon
Galaxy to your desktop" section below.

## Uploading Files \> 2GB via FTP to Maroon Galaxy

### From a Unix Computer (Mac or Linux)

Go to the directory containing the file on your local computer. (for
example: sample\_file.fastq)

Click "Upload File" icon then click "Choose FTP file" for which port to
use. Port 2121 is for Maroon Galaxy.

| Galaxy       | Host                       | port |
| ------------ | -------------------------- | ---- |
| Grace Maroon | portal-grace.hprc.tamu.edu | 2121 |
| Silver       | portal-terra.hprc.tamu.edu | 2129 |
|              |                            |      |

Each Galaxy instance has its own port. The port number can be found by
clicking the "Choose FTP file" button in the Galaxy upload tool menu.

Connect to the ftp server using your Maroon Galaxy credentials

` sftp -P 2121 Your_NetID@portal-grace.hprc.tamu.edu`

Depending on your sftp version or if you are on an Grace fast transfer
node, you may have to use the following:

` sftp -oPort=2121 Your_NetID@portal-grace.hprc.tamu.edu`

The sftp prompt looks like this:

` sftp>`

When you see the sftp prompt, you can upload a file with the put command
followed by the file name to upload.

` put sample_file.fastq`

Then you can verify that the file was uploaded by using the ls command.

` ls`

Then exit the sftp prompt and go to Galaxy to upload files and click the
button 'Choose FTP file' which will show you the file you uploaded.

` exit`

### From one of your directories on Grace or Terra

You can copy files from one of your directories on Grace to your Galaxy
ftp directory and later import it to your history using the 'Choose FTP
file' button in the Galaxy upload tool.

Login to Grace using MobaXTerm or a Unix Terminal and go to the
directory containing the file on Grace. (for example: **cd
$SCRATCH/my\_dir** which contains a file named **sample\_file.fastq**)

Connect to the port number for your Galaxy instance. The example below
is for Maroon port 2121

` sftp -oPort=2121 Your_NetID@portal-grace.hprc.tamu.edu`

The sftp prompt looks like this:

` sftp>`

When you see the sftp prompt, you can upload a file from your $SCRATCH
directory on Grace to your Galaxy ftp account with the put command
followed by the file name to upload.

` put sample_file.fastq`

Then you can verify that the file was uploaded by using the ls command.

` ls`

Then exit the sftp prompt and go to Galaxy to upload files and click the
button 'Choose FTP file' which will show you the file you uploaded.

` exit`

### Using Bitvise

Download and install the Bitvise client to your Windows computer.

<https://www.bitvise.com/ssh-client-download>

| Galaxy       | Host                       | port |
| ------------ | -------------------------- | ---- |
| Grace Maroon | portal-grace.hprc.tamu.edu | 2121 |
| Silver       | portal-terra.hprc.tamu.edu | 2129 |
|              |                            |      |

Once connected, drag and drop files from the 'Local files' panel on the
left to the 'Remote files' panel on the right.

### Using MobaXterm

Click the Session button in the top left corner then click the SFTP
button and set Remote Host = portal-grace.hprc.tamu.edu, port = 2121 for
Maroon Galaxy, also enter your username.

Then in the Advanced Sftp settings tab, check the box for 2-steps
authentication and then click the OK button.

Enter your password at the first the password prompt.

The second prompt does not display the DUO authentication menu instead
it asks for your password again but you should enter the number 1 to
receive a DUO push or phone call whichever is enabled for your account
instead of entering your password again. If you have a YubiKey, you can
push it at the second password prompt instead of entering the number 1

### Using Filezilla

Filezilla does not work with 2 factor authentication for Galaxy ftp
uploads. It is recommended to use BitVise as an alternative.

### Using WinSCP

WinSCP does not work with 2 factor authentication for Galaxy ftp uploads
due to using non-standard port numbers. It is recommended to use BitVise
as an alternative.

## Downloading Files \> 2GB via FTP from Maroon Galaxy to your desktop

### Stage files to copy

Use the 'Files 2 FTP' tool in Galaxy to copy files from your Galaxy
history to your Galaxy FTP directory which is located on Grace.

In the 'Files 2 FTP' tool, add a directory name such as a date or
project or history name and then select multiple files to add to the new
or existing directory.

After copying files in Galaxy, use your SSH client, (terminal on Mac or
Linux, or BitVise on Windows) and copy files from Galaxy FTP port 2121
to your desktop.

## Moving Files \> 2GB via FTP from Maroon Galaxy to your Grace $SCRATCH directory

Use the 'Files 2 FTP' tool in Galaxy to copy files from your Galaxy
history to your Galaxy FTP directory which is located on Grace.

Login to the Grace command line and go to the directory where you want
to download the Galaxy ftp files.

Connect to the port number for your Galaxy instance. The example below
is for Maroon port 2121

` sftp -oPort=2121 Your_NetID@portal-grace.hprc.tamu.edu`

The sftp prompt looks like this:

` sftp>`

At the sftp\> prompt, list the files to make sure the transfer was
successful.

` sftp> ls`

You can download a file from your Galaxy ftp account to your Grace
working directory with the get command followed by the file name.

` get sample_file.fastq`

Exit the sftp\> prompt by typing **exit** and then type **ls** to see
the file in your Grace scratch working directory.

#### Download using a terminal

If you are using a terminal, then you can use the sftp command to access
your Maroon FTP directory as described in section
[1.8.1](/kb3/Software/Galaxy/SW@Galaxy/#from-a-unix-computer-.28mac-or-linux.29/)

Once in your FTP directory, you can 'cd' to the directory you created
with the 'Files 2 FTP' tool and use the 'get' command **get filename**
to copy files from your Galaxy FTP directory to your desktop.

You can copy multiple files by using the \* wild card character: **get
file\***

You can copy an entire directory using the -r option: **get -r
directory\_name**

#### Download using a GUI client

If you are using the Bitvise GUI as described in section
[1.8.3](/kb3/Software/Galaxy/SW@Galaxy/#using-bitvise/), you can
select a file and drag and drop on to your desktop.

### Delete files after copying

After you have copied your files from your Grace ftp directory to your
desktop, you can delete the file from the ftp directory while logged
into the ftp terminal by using **rm filename**

Deleting a directory using the terminal is a two step process. First
delete all files in the directory **rm directory\_name/\*** then delete
the directory **rmdir directory\_name**

You can also delete the files in the Bitvise interface. Deleting the
files after downloading from your ftp directory will save disk space.

## Requesting New Galaxy Tools

  - Go to [usegalaxy.org](https://usegalaxy.org) or
    [galaxy\_toolshed](https://toolshed.g2.bx.psu.edu/) and find a tool
    you want installed in Silver Galaxy and send us the URL for the
    tool.
  - Send us a list of tools with the URLs that you would like installed
    so we can install them all at once.
  - Each time a tool is installed, the Galaxy server must be restarted.
      - We would prefer to install many tools at once and then restart
        the Galaxy server.
      - It is rare that restarting the Galaxy server can corrupt some
        jobs but it has happened and we want to reduce the chances of
        interrupting submitted jobs.

### When a Galaxy tool is Available

  - If you know of an existing Galaxy tool that you have found at
    usegalaxy.org, for example, send us a request identifying the URL
    for the tool in the toolshed repository or usegalaxy.org.

### When a tool has no Galaxy interface

  - There are some Bioinformatics tools that do not have a Galaxy
    interface developed.
  - We will need to spend more time creating the xml configuration files
    and testing.
      - This will take more time than adding a tool from the Galaxy
        toolshed.
      - Some tools are simple and can be done rather quickly but others
        will require extensive development time.
      - In some rare cases we may not be able to configure a Galaxy tool
        for a software application due to the complexity of the tool
        installation which will not work in the Galaxy environment.

## FAQ

1\. Q: My job immediately fails with the message:

`The cluster DRM system terminated this job`

1\. A: Check your file quota at the HPRC Grace portal
[dashboard](https://portal-grace.hprc.tamu.edu/pun/sys/OOD-Dashboard) or
use the 'showquota' command at the Grace command line

2\. Q: My job fails after running for a long time with the message:

`The cluster DRM system terminated this job`

2\. A: Check the stderr and stdout for your Galaxy job and see if you
see one of the following lines then your job requires more memory or
time to run. Contact us to update the tool configuration if needed.

` TERM_MEMLIMIT: job killed after reaching LSF memory usage limit.`

` TERM_RUNLIMIT: job killed after reaching LSF run time limit.`

3\. Q: My job has been in the queue status for a long time, what is
going on?

3\. A: First check the Grace command line to see if you job is pending
(PEND) in the queue by using the squeue command. If the job is PEND then
the cluster is busy at the moment. You can see how busy the Grace
cluster is by looking at the System Load Levels on the HPRC
[homepage](https://hprc.tamu.edu/).

3\. A: Check your SUs to make sure you have enough to run the Galaxy job
by using the "My HPRC SU balance" tool in Galaxy or you can use the Unix
command 'myproject -l' on the Grace command line or check your balance
at the HPRC Grace portal
[dashboard](https://portal-grace.hprc.tamu.edu/pun/sys/OOD-Dashboard)

## Tool specific notes

### Fastq groomer

The new Grace Maroon Galaxy automatically detects quality score encoding
so there is no need to use Fastq Groomer on newer sequence data
generated by the newer Illumina sequencing platforms.

Fastq groomer is generally for older sequence runs that were sequenced
on the early Illumina sequence machines.

The fastqsanger format is needed to run many Galaxy tools such as
Bowtie. The default format for uploaded fastq files is fastq. If your
sequence files are from newer Illumina machines such as the MiSeq and
HiSeq, then they are already in fastqsanger format. You can set the type
to fastqsanger when uploading or you can click the pencil icon on your
file in the right panel and change the datatype to fastqsanger. Both of
these options are more efficient than running Fastq groomer.

See Galaxy [tutorial](https://vimeo.com/76024253) on checking if
Illumina reads are already in fastqsanger format.

You can find out the specific fastq format of your file by running the
FastQC tool and looking at the RawData result for the Encoding.

If you see something like the following then all you need to do instead
of running Fastq groomer is to click the pencil icon on your file in the
right panel and change the datatype to fastqsanger which is more
efficient than running Fastq groomer.

`Encoding   Sanger / Illumina 1.9`

If your file Encoding is already Sanger / Illumina 1.8+ then running
fastq groomer on your file will only make an exact duplicate of the file
and you will have unnecessarily used up SUs and disk space.

### Trinity

#### Before you run a Trinity job

Please monitor your file quota during your job run using the following
command and request an increase if your job is creating enough files
that your file quota might be reached.

` showquota`

Be aware that starting multiple Trinity jobs at the same time may cause
you to reach your file quota at a quicker pace. Please monitor your file
quota during your job run.

#### If your Trinity job Fails

  - If your Trinity job failed and after you have determined the reason
    for you Trinity job failing, you will need to delete the failed job
    files by selecting the 'Permanently remove it from disk' link which
    is part of a two step process.
      - First delete the job file in the right panel by clicking the X,
        then select the 'deleted' link in the right panel at the top
        which will show all deleted files.
      - Then click the link 'Permanently remove it from disk' for the
        failed job that you would like to permanently delete which will
        also delete all temporary files.
  - If you do not 'Permanently remove it from disk', then the temporary
    files from the failed job are still counted towards your quota and
    your next job will likely fail due to your file quota met again.

For more information on Delete vs Delete Permanently see this link

` `<https://wiki.galaxyproject.org/Learn/ManagingDatasets#Delete_vs_Delete_Permanently>

### RSEM

The Galaxy interface was downloaded from a git repo and was developed to
work with RSEM 1.1.17.

Since we have RSEM 1.2.29 installed, we are updating the tool to work
with RSEM 1.2.29 which means some additional parameters you select other
than the defaults may fail.

We have had success with the default RSEM Galaxy tool settings.

Currently the option "Transcript and genome bam results files" in the
RSEM calculate expression tool is not workiing. You should leave it at
"No BAM results files" or "Transcript bam results file" for now.

Let us know if specific RSEM options you require cause the tool to fail
and we will update the RSEM Galaxy tool.

### BLAST

There are some genomes already available and we can enable other
organism genomes upon request.

When requesting additional genomes, send the HPRC helpdesk a link to the
genome at NCBI, Ensembl or UCSC or other model organism databases.

### bwa, bowtie, bowtie2 hisat2

We can create genome indexes for common model organisms upon request.

When requesting additional genomes, send the HPRC helpdesk a link to the
genome at NCBI, Ensembl or UCSC or other model organism databases.

### HISAT2

If you will be using cufflinks on HISAT2 output, you will need to select
the following option in the HISAT2 Galaxy tool:

  - 'Spliced Alignment Parameters'
      - 'Specify spliced alignment parameters'
          - 'Transcriptome assembly reporting'
              - 'Report alignments tailored specifically for Cufflinks'

## Share your History

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
