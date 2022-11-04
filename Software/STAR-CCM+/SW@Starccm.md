# STAR-CCM+

## Description

Much more than just a CFD solver, STAR-CCM+ is an entire engineering
process for solving problems involving flow (of fluids or solids), heat
transfer and stress.

  - Homepage: <http://mdx.plm.automation.siemens.com/star-ccm-plus>

## Access

<font color=red size=3>**STAR-CCM+ is available ONLY for HPRC users at
the Texas A\&M College Station and Galveston campuses. Our license does
NOT permit use of STAR-CCM+ by any HPRC users from the TAMU Qatar branch
campus.**</font>

If you have particular concerns about whether specific usage falls
within the TAMU HPRC license, please send an email to the HPRC Helpdesk.
Usage of STAR-CCM+ is restricted by the number of available tokens. To
see the number of available tokens, use the [ License Checker
Tool](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink").

### Loading the Module

To see all versions of STAR-CCM+ available on Ada:

`[NetID@cluster ~]$ `**`module   spider   STAR-CCM+`**

To load a particular version of STAR-CCM+ on Ada (Example: 14.02.012):

`[NetID@cluster ~]$ `**`module   load   STAR-CCM+/14.02.012`**

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use
non-interactive batch jobs for resource-intensive and/or multiple-core
processing. Users are requested to be
<font color=teal>**responsible**</font> and <font color=teal>**courteous
to other users**</font> when using software on the login nodes.

The most important processing limits here are:  
\* **ONE HOUR** of **PROCESSING TIME** per login session.

  - **EIGHT CORES** per login session on the same node or (cumulatively)
    across all login nodes.

<font color=red size=3>**Anyone found violating the processing limits
will have their processes killed without warning. Repeated violation of
these limits will result in account suspension.**</font>  
<font color=teal>**Note:** Your login session will disconnect after
**one hour** of inactivity.</font>

## Usage on the Compute Nodes

Non-interactive batch jobs on the compute nodes allows for
resource-demanding processing. Non-interactive jobs have higher limits
on the number of cores, amount of memory, and runtime length.

For instructions on how to create and submit a batch job, please see the
appropriate wiki page for each respective cluster:

  - Terra: [ About Terra Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Grace: [ About Grace Batch Processing](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink")

### Recommendations for Parallel Processing

A general good rule to follow is to not have fewer than 50,000 cells per
core when parallel processing. The reason for this is when fewer than
50,000 cells per core are used, the computational time decrease does not
scale linearly. The most efficient computing time in terms of linear
scaling occur with 50,000 cells per core or more.

### Ada Example Job Script

<font color=purple>NOTE: Job examples are NOT lists of commands, but are
a template of the contents of a job file. These examples should be
pasted into a text editor and submitted as a job to be tested, not
entered as commands line by line. </font>

**Updated: May 14, 2019**

    #BSUB -J StarJob             # sets the job name to StarJob.
    #BSUB -L /bin/bash           # uses the bash login shell to initialize the job's execution environment.
    #BSUB -W 2:00                # sets to 2 hours the job's runtime wall-clock limit.
    #BSUB -n 40                  # assigns 40 core for execution.
    #BSUB -R "span[ptile=20]"    # assigns 20 core per node.
    #BSUB -R "rusage[mem=5000]"  # reserves 5000MB per process/CPU for the job (5GB * 1 Core = 5GB per node) 
    #BSUB -M 5000            # sets to 5,000MB (~5GB) the per process enforceable memory limit.
    #BSUB -o StarCCM.%J          # directs the job's standard output to StarCCM.jobid
    
    
    # Load the modules
    module load STAR-CCM+/14.02.012
    
    # Launch STAR-CCM+ with proper parameters 
    starccm+ -np 40 -batchsystem lsf -rsh blaunch -batch simfile -machinefile $LSB_DJOB_HOSTFILE

To submit the batch job, run:

`[NetID@ada1 ~]$ `**`bsub   <   `*`jobscript`***

### Terra Example

**Updated: April 20, 2021**

<font color=teal>**Note:**A script (starccm\_wrapper) is provided to use
the correct settings for running STAR-CCM+ in a batch job on
Terra.</font>

    #!/bin/bash
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=starccm      # set job name to starccm
    #SBATCH --time=1:30:00          # set time to 1.5 hours
    #SBATCH --ntasks=56             # assign 56 total cores
    #SBATCH --ntasks-per-node=28    # assign 28 cores per node
    #SBATCH --mem=28G               # request 28 GB of memory per node.
    #SBATCH --output=starccm.out.%j # set output file to starccm.out.$SLURM_JOB_ID
    
    ml STAR-CCM+/14.02.012
    starccm_wrapper -batch simfile

To submit the batch job, run:

`[NetID@terra1 ~]$ `**`sbatch   `*`jobscript`***

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.
