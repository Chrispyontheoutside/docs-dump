# Grace Exercises Guide


## Grace Usage Policies

**Access to Grace is granted with the condition that you will understand
and adhere to all TAMU HPRC and Grace-specific policies.**

General policies can be found on the [HPRC Policies
page](https://hprc.tamu.edu/policies/).

## Accessing Grace

Most access to Grace is done via a secure shell session. In addition,
**two-factor authentication** is required to login to any cluster.

Users on **Windows** computers use either [PuTTY](http://www.putty.org/)
or [MobaXterm](http://mobaxterm.mobatek.net/). If MobaXterm works on
your computer, it is usually easier to use. When starting an ssh session
in PuTTY, choose the connection type 'SSH', select port 22, and then
type the hostname 'grace.hprc.tamu.edu'. For MobaXterm, select
'Session', 'SSH', and then remote host 'grace.hprc.tamu.edu'. Check the
box to specify username and type your NetID. After selecting 'Ok', you
will be prompted for Duo Two Factor Authentication. For more detailed
instructions, visit the [Two Factor
Authentication](/kb3/Helpful-Pages/Two-Factor/Two_Factor/#mobaxterm/) page.

Users on **Mac** and **Linux/Unix** should use whatever SSH-capable
terminal is available on their system. The command to connect to Grace
is as follows. Be sure to replace \[NetID\] with your TAMU NetID.

`[user1@localhost ~]$ `**`ssh   `*`[NetID]`*`@grace.hprc.tamu.edu`**

<font color=teal>**Note:** In this example *\[user1@localhost ~\]$*
represents the command prompt on your local machine.</font>  
Your login password is the same that used on
[Howdy](https://howdy.tamu.edu/). You will not see your password as your
type it into the login prompt.

### Off Campus Access

Please visit [this page](/kb3/Helpful-Pages/Access/HPRC@Access/#access-using-ssh/)
to find information on accessing Grace remotely.

For more detailed instructions on how to access our systems, please see
the [ HPRC Access page](/kb3/Helpful-Pages/Access/HPRC@Access/ "wikilink").

## Grace Exercises: Logging In

When you first access Grace, you will be within your *home* directory.
This directory has smaller storage quotas and should not be used for
general purpose. You will also see your current disk and file quota's
printed along with the Message of the Day. The Message of the Day
includes important policy information and announcements.

You can check your quota with the following command:

`[NetID@grace1 ~]$ `**`showquota`**

You can view the Message of the Day with the following command:

`[NetID@grace1 ~]$ `**`motd`**

You can see your current location in the system with the "print work
directory" command:

`[NetID@grace1 ~]$ `**`pwd`**

By default, user's will be placed in their home directory. The home
directory has a limit of 10,000 files  or **10GB of data**.
<font color=red> Per our policy, the home directory quota *cannot be
expanded* </font>

`[NetID@grace1 ~]$ `**`cd   $SCRATCH`**

Navigate to *home* with the following command:

`[NetID@grace1 ~]$ `**`cd   $HOME`**

<font color=purple> Your *scratch* directory is restricted to
1TB/250,000 files of storage. This storage quota is **expandable** upon
request.

Your *home* directory is restricted to 10GB/10,000 files of storage.
This storage quota is **not expandable**. </font>

You can see the current status of your storage quotas with:

`[NetID@grace1 ~]$ `**`showquota`**

If you need a storage quota increase, please contact us with
justification and the expected length of time that you will need the
quota increase.

## The Batch System

The batch system is a load distribution implementation that ensures
convenient and fair use of a shared resource. Submitting jobs to a batch
system allows a user to reserve specific resources with minimal
interference to other users. All users are required to submit
resource-intensive processing to the compute nodes through the batch
system - <font color=red> attempting to circumvent the batch system is
not allowed.</font>

On Grace, **Slurm** is the batch system that provides job management.
More information on **Slurm** can be found in the [ Grace
Batch](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink") page.

## Running Your Program / Preparing a Job File

In order to properly run a program on Grace, you will need to create a
job file and submit a job.

The simple example job file below requests 1 core on 1 node with 2.5GB
of RAM for 1.5 hours. **Note that typical nodes on Grace have 48 cores
with 384 GB of usable memory and ensure that your job requirements will
fit within these restrictions.** Any modules that need to be loaded or
executable commands will replace the *"\#First Executable Line"* in this
example.

`#!/bin/bash`  
`##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION`  
`#SBATCH --export=NONE        #Do not propagate environment`  
`#SBATCH --get-user-env=L     #Replicate login environment`  
`  `  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=JobExample1     #Set the job name to "JobExample1"`  
`#SBATCH --time=01:30:00            #Set the wall clock limit to 1hr and 30min`  
`#SBATCH --ntasks=1                 #Request 1 task`  
`#SBATCH --ntasks-per-node=1        #Request 1 task/core per node`  
`#SBATCH --mem=2560M                #Request 2560MB (2.5GB) per node`  
`#SBATCH --output=Example1Out.%j    #Send stdout/err to "Example1Out.[jobID]"`  
  
`#First Executable Line`

Note: If your job file has been written on an older Mac or DOS
workstation, you will need to use "dos2unix" to remove certain
characters that interfere with parsing the script.

`[NetID@grace1 ~]$ `**`dos2unix   `*`MyJob.slurm`***

More information on **job options** can be found in the [ Building Job
Files](/kb3/User-Guides/Grace/Grace@Batch/#building-job-files "wikilink") section of the [ Grace
Batch](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink") page.

More information on **dos2unix** can be found on the [
dos2unix](/kb3/Software/useful-tools/SW@dos2unix/ "wikilink") section of the [ HPRC Available
Software](/kb3/Software/SW/ "wikilink") page.

## Submitting and Monitoring Jobs

Once you have your job file ready, it is time to submit your job. You
can submit your job to slurm with the following command:

`[NetID@Grace ~]$ `**`sbatch   `*`MyJob.slurm`***  
`Submitted batch job 3606`

After the job has been submitted, you are able to monitor it with
several methods. To see the status of all of your jobs, use the
following command:

`[NetID@grace1 ~]$ `**`squeue   -u   `*`NetID`***  
`JOBID       NAME                USER                    PARTITION   NODES CPUS STATE       TIME        TIME_LEFT   START_TIME           REASON      NODELIST            `  
`3606        myjob2              NetID                   short       1     3    RUNNING     0:30        00:10:30    2016-11-27T23:44:12  None        tnxt-[0340]  `

To see the status of one job, use the following command, where *XXXX* is
the JobID:

`[NetID@grace1 ~]$ `**`squeue   --job   `*`XXXX`***  
`JOBID       NAME                USER                    PARTITION   NODES CPUS STATE       TIME        TIME_LEFT   START_TIME           REASON      NODELIST            `  
`XXXX        myjob2              NetID                   short       1     3    RUNNING     0:30        00:10:30    2016-11-27T23:44:12  None        tnxt-[0340]  `

To cancel a job, use the following command, where *XXXX* is the JobID:

`[NetID@grace1 ~]$ `**`scancel   `*`XXXX`***

More information on **submitting** and **monitoring** Slurm jobs can be
found in the [ Job Submission](/kb3/User-Guides/Grace/Grace@Batch/#job-submission "wikilink")
section of the [ Grace Batch System](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink") page.

## Additional Topics

The [ HPRC Batch Translation](/kb3/Helpful-Pages/Batch-Translation/HPRC@Batch_Translation/ "wikilink") page
contains information on **converting** between LSF, PBS, and Slurm.

Our staff has also written some example jobs for specific software.
These software-specific examples can be seen on the [ Individual
Software Pages](/kb3/Software/SW/ "wikilink") where available.

### Finding Software

Software on Grace is loaded using **modules**.

You can see the most popular software on the [ HPRC Available
Software](/kb3/Software/SW/ "wikilink") page.

You can **find** *most* available software on Grace with the following
command:

`[NetID@grace1 ~]$ `**`module   avail`**

You can **search for** particular software by keyword using:

`[NetID@grace1 ~]$ `**`module   spider   `*`keyword`***

You can load a module using:

`[NetID@grace1 ~]$ `**`module   load   `*`moduleName`***

You can list all currently loaded modules using:

`[NetID@grace1 ~]$ `**`module   list`**

You can remove all currently loaded modules using:

`[NetID@grace1 ~]$ `**`module   purge`**

If you need **new software** or **an update**, please contact us with
your request.

There are restrictions on what software we can install. There is also
regularly a queue of requested software installations.

<font color=teal>Please account for **delays** in your installation
request timeline. </font>

### Transferring Files

Files can be transferred to Grace using the *scp* command or a file
transfer program.

Our users most commonly utilize:

  - [WinSCP](https://winscp.net/eng/download.php) - Straightforward,
    legacy
  - [FileZilla Client](https://filezilla-project.org/) - Easy to use,
    additional features, available on most platforms
  - [MobaXterm Graphical
    SFTP](https://mobaxterm.mobatek.net/features.html) - Included with
    MobaXterm

<font color=teal>**Advice:** while GUIs are acceptable for file
transfers, the cp and scp commands are much quicker and may
significantly benefit your workflow.</font>

#### Reliably Transferring Large Files

For files larger than several GB, you will want to consider the use of a
more fault-tolerant utility such as rsync.

`[NetID@grace1 ~]$ `**`rsync   -av   [-z]   `*`localdir/ 
 userid@remotesystem:/path/to/remotedir/`***

An rsync example can be seen on the [ Ada Fast
Transfer](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink")
page.

### Graphic User Interfaces (Visualization)

The Open on Demand Portal is the preferred way to access visual
applications on Grace. From the OOD portal, you can browse and manage
the files in your home and scratch directories. This allows user's to
easily view media files (.png .jpeg .mp4 etc) through their web browser
of choice.

Here's a quick summary of the functions of the OOD Portal:

  - View and submit visualization jobs
  - View and submit interactive applications such as Matlab & ANSYS
  - View your active jobs on Ada
  - Access the shell of Ada, Terra, and Grace
  - View and manage the files in your Ada home and scratch directories
