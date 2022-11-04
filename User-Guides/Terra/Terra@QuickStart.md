# Terra Quick Start Guide


## Terra Usage Policies

**Access to Terra is granted with the condition that you will understand
and adhere to all TAMU HPRC and Terra-specific policies.**

General policies can be found on the [HPRC Policies
page](https://hprc.tamu.edu/policies/).

Terra-specific policies, which are similar to Grace, can be found on the
[ Terra Policies page](/kb3/User-Guides/Terra/Terra@Policies/ "wikilink").

## Accessing Terra

Most access to Terra is done via a secure shell session. In addition,
**two-factor authentication** is required to login to any cluster.

Users on **Windows** computers use either [PuTTY](http://www.putty.org/)
or [MobaXterm](http://mobaxterm.mobatek.net/). If MobaXterm works on
your computer, it is usually easier to use. When starting an ssh session
in PuTTY, choose the connection type 'SSH', select port 22, and then
type the hostname 'terra.tamu.edu'. For MobaXterm, select 'Session',
'SSH', and then remote host 'terra.tamu.edu'. Check the box to specify
username and type your NetID. After selecting 'Ok', you will be prompted
for Duo Two Factor Authentication. For more detailed instructions, visit
the [Two Factor
Authentication](/kb3/Helpful-Pages/Two-Factor/Two_Factor/#mobaxterm/) page.

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/PXIGhqLJP3g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

Users on **Mac** and **Linux/Unix** should use whatever SSH-capable
terminal is available on their system. The command to connect to Terra
is as follows. Be sure to replace \[NetID\] with your TAMU NetID.

`[user1@localhost ~]$ `**`ssh   `*`[NetID]`*`@terra.tamu.edu`**

<font color=teal>**Note:** In this example *\[user1@localhost ~\]$*
represents the command prompt on your local machine.</font>  
Your login password is the same that used on
[Howdy](https://howdy.tamu.edu/). You will not see your password as your
type it into the login prompt.

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/KjHwfZI_ej4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

### Off Campus Access

Please visit [this page](/kb3/Helpful-Pages/Access/HPRC@Access/#access-using-ssh/)
to find information on accessing Terra remotely.

For more detailed instructions on how to access our systems, please see
the [ HPRC Access page](/kb3/Helpful-Pages/Access/HPRC@Access/ "wikilink").

## Navigating Terra & Storage Quotas

When you first access Terra, you will be within your *home* directory.
This directory has smaller storage quotas and should not be used for
general purpose.

You can navigate to your *home* directory with the following command:

`[NetID@terra1 ~]$ `**`cd   /home/`*`NetID`***

Your *scratch* directory has more storage space than your *home*
directory and is recommended for general purpose use. You can navigate
to your *scratch* directory with the following command:

`[NetID@terra1 ~]$ `**`cd   /scratch/user/`*`NetID`***

You can navigate to *scratch* or *home* easily by using their respective
environment variables.

Navigate to *scratch* with the following command:

`[NetID@terra1 ~]$ `**`cd   $SCRATCH`**

Navigate to *home* with the following command:

`[NetID@terra1 ~]$ `**`cd   $HOME`**

<font color=purple> Your *scratch* directory is restricted to
1TB/250,000 files of storage. This storage quota is **expandable** upon
request. A user's *scratch directory* is **NOT** backed up.

Your *home* directory is restricted to 10GB/10,000 files of storage.
This storage quota is **not expandable**. A user's *home* directory is
backed up on a nightly basis. </font>

You can see the current status of your storage quotas with:

`[NetID@terra1 ~]$ `**`showquota`**

If you need a storage quota increase, please contact us with
justification and the expected length of time that you will need the
quota increase.

## Transferring Files

Files can be transferred to Terra using the *scp* command or a file
transfer program.

Our users most commonly utilize:

  - [WinSCP](https://winscp.net/eng/download.php) - Straightforward,
    legacy
  - [FileZilla Client](https://filezilla-project.org/) - Easy to use,
    additional features, available on most platforms
  - [MobaXterm Graphical
    SFTP](https://mobaxterm.mobatek.net/features.html) - Included with
    MobaXterm

See our \[Terra-Filezilla example video\] for a demonstration of this
process.

<font color=teal>**Advice:** while GUIs are acceptable for file
transfers, the cp and scp commands are much quicker and may
significantly benefit your workflow.</font>

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/oCSzuJf6p7g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>


### Reliably Transferring Large Files

For files larger than several GB, you will want to consider the use of a
more fault-tolerant utility such as rsync.

`[NetID@terra1 ~]$ `**`rsync   -av   [-z]   `*`localdir/ 
 userid@remotesystem:/path/to/remotedir/`***

## Managing Project Accounts

The batch system will charge SUs from the either the account specified
in the job parameters, or from your default account (if this parameter
is omitted). To avoid errors in SU billing, you can view your active
accounts, and set your default account using the
[myproject](/kb3/Helpful-Pages/myproject/HPRC@myproject/) command.

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/dg3KaUvIWcU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## Finding Software

Software on Terra is loaded using **modules**.

A list of the most popular software on our systems is available on the [
HPRC Available Software](/kb3/Software/SW/ "wikilink") page.

To **find** *most* available software on Terra, use the following
command:

`[NetID@terra1 ~]$ `**`module   avail`**

To **search for** particular software by keyword, use:

`[NetID@terra1 ~]$ `**`module   spider   `*`keyword`***

To load a module, use:

`[NetID@terra1 ~]$ `**`module   load   `*`moduleName`***

To list all currently loaded modules, use:

`[NetID@terra1 ~]$ `**`module   list`**

To remove all currently loaded modules, use:

`[NetID@terra1 ~]$ `**`module   purge`**

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/drxpbrOCPFw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

If you need **new software** or **an update**, please contact us with
your request.

There are restrictions on what software we can install. There is also
regularly a queue of requested software installations.

<font color=teal>Please account for **delays** in your installation
request timeline. </font>

## Running Your Program / Preparing a Job File

In order to properly run a program on Terra, you will need to create a
job file and submit a job to the batch system. The batch system is a
load distribution implementation that ensures convenient and fair use of
a shared resource. Submitting jobs to a batch system allows a user to
reserve specific resources with minimal interference to other users. All
users are required to submit resource-intensive processing to the
compute nodes through the batch system - <font color=red> attempting to
circumvent the batch system is not allowed.</font>

On Terra, **Slurm** is the batch system that provides job management.
More information on **Slurm** can be found in the [ Terra
Batch](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink") page.

The simple example job file below requests 1 core on 1 node with 2.5GB
of RAM for 1.5 hours. Note that typical nodes on Terra have 28 cores
with 120GB of usable memory and ensure that your job requirements will
fit within these restrictions. Any modules that need to be loaded or
executable commands will replace the *"\#First Executable Line"* in this
example.

    #!/bin/bash
    ##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE        #Do not propagate environment
    #SBATCH --get-user-env=L     #Replicate login environment

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=JobExample1     #Set the job name to "JobExample1"
    #SBATCH --time=01:30:00            #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=1                 #Request 1 task
    #SBATCH --ntasks-per-node=1        #Request 1 task/core per node
    #SBATCH --mem=2560M                #Request 2560MB (2.5GB) per node
    #SBATCH --output=Example1Out.%j    #Send stdout/err to "Example1Out.[jobID]"

    #First Executable Line

Note: If your job file has been written on an older Mac or DOS
workstation, you will need to use "dos2unix" to remove certain
characters that interfere with parsing the script.

`[NetID@terra1 ~]$ `**`dos2unix   `*`MyJob.slurm`***

More information on **job options** can be found in the [ Building Job
Files](/kb3/User-Guides/Terra/Terra@Batch/#building-job-files "wikilink") section of the [ Terra
Batch](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink") page.

More information on **dos2unix** can be found on the [
dos2unix](/kb3/Software/useful-tools/SW@dos2unix/ "wikilink") section of the [ HPRC Available
Software](/kb3/Software/SW/ "wikilink") page.

## Submitting and Monitoring Jobs

Once you have your job file ready, it is time to submit your job. You
can submit your job to slurm with the following command:

`[NetID@terra1 ~]$ `**`sbatch   `*`MyJob.slurm`***  
`Submitted batch job 3606`

After the job has been submitted, you are able to monitor it with
several methods. To see the status of all of your jobs, use the
following command:

    [NetID@terra1 ~]$ squeue -u NetID
    JOBID       NAME                USER                    PARTITION   NODES CPUS STATE       TIME        TIME_LEFT   START_TIME           REASON      NODELIST            
    3606        myjob2              NetID                   short       1     3    RUNNING     0:30        00:10:30    2016-11-27T23:44:12  None        tnxt-[0340]

To see the status of one job, use the following command, where *XXXX* is
the JobID:

    [NetID@terra1 ~]$ squeue --job XXXX
    JOBID       NAME                USER                    PARTITION   NODES CPUS STATE       TIME        TIME_LEFT   START_TIME           REASON      NODELIST            
    XXXX        myjob2              NetID                   short       1     3    RUNNING     0:30        00:10:30    2016-11-27T23:44:12  None        tnxt-[0340]

To cancel a job, use the following command, where *XXXX* is the JobID:

`[NetID@terra1 ~]$ `**`scancel   `*`XXXX`***

More information on [ Job
Submission](/kb3/User-Guides/Terra/Terra@Batch/#job-submission "wikilink") and [ Job
Monitoring](/kb3/User-Guides/Terra/Terra@Batch/#job-monitoring-and-control-commands "wikilink")
Slurm jobs can be found at the [ Terra Batch
System](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink") page.

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/dQzBZJpoU64" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## tamubatch

**tamubatch** is an automatic batch job script that submits jobs for the
user without the need of writing a batch script on the Grace and Terra
clusters. The user just needs to provide the executable commands in a
text file and tamubatch will automatically submit the job to the
cluster. There are flags that the user may specify which allows control
over the parameters for the job submitted.

''tamubatch is still in beta and has not been fully developed. Although
there are still bugs and testing issues that are currently being worked
on, tamubatch can already submit jobs to both the Grace and Terra
clusters if given a file of executable commands. ''

For more information, visit [this
page.](/kb3/Helpful-Pages/tamubatch/SW@tamubatch/)

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/sP7GnQNvMVo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## Graphic User Interfaces (Visualization)

The use of GUIs on Terra is a more complicated process than running
non-interactive jobs or doing resource-light interactive processing.

You have **two options** for using GUIs on Terra.

The **first option** is to use the [Open On Demand
Portal](https://portal.hprc.tamu.edu/), which is a web interface to our
clusters. Users must be connected to the campus network either directly
or via VPN to access the portal. More information can be found
[here](/kb3/Software/Portal/SW@Portal/), or on our [YouTube
channel](https://www.youtube.com/watch?v=dqa2ZzsEmQs&list=PLHR4HLly3i4aJJDxKTZIpxyJG6uSqgAgd)

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/videoseries?list=PLHR4HLly3i4aJJDxKTZIpxyJG6uSqgAgd" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

The **second option** is to run on the login node. When doing this, you
**must** observe the fair-use policy of login node usage. Users commonly
violate these policies by accident, resulting in terminated processes,
confusion, and warnings from our admins.
