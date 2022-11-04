# WRF

<font color=red> *THIS PAGE IS UNDER CONSTRUCTION*</font>

The Weather Research and Forecasting (WRF) Model is a next-generation
mesoscale numerical weather prediction system designed to serve both
operational forecasting and atmospheric research needs.

  - Homepage: <http://www.wrf-model.org>

## Access

WRF is open to all HPRC users.

### Loading the Module

To see all versions of WRF available on Ada:

` [ netID@cluster ~]$ `**`module   spider   WRF`**

To load a particular version of WRF on (Example: 3.8.0):

` [ netID@cluster ~]$ `**`module   load 
 WRF/3.8.0-intel-2016a-dmpar`**`  `

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

  - Ada: [ About Ada Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Terra: Terra Link

### Ada Example

Updated: June 27, 2016

    #BSUB -J wrftest          # sets the job name to myjob1.
    #BSUB -L /bin/bash        # uses the bash login shell to initialize the job's execution environment.
    #BSUB -W 10:00            # sets to 10 hours the job's runtime wall-clock limit.
    #BSUB -n 40               # assigns 40 cores for execution.
    #BSUB -R "span[ptile=20]"   # assigns 20 cores per node.
    #BSUB -R "rusage[mem=2700]" # reserves 2700MB per process/CPU for the job
    #BSUB -M 2700               # sets to 2,700MB the per process enforceable memory limit.
    #BSUB -o wrf.%J             # directs the job's standard output to wrf.jobid
    
    # Load the modules
    module load WRF/3.8.0-intel-2016a-dmpar
    
    # Use mpirun to start wrf
    mpirun wrf.exe

### Terra Example
