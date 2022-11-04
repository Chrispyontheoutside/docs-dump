# Amber

## Description

Amber is a suite of biomolecular simulation programs. - Homepage:
<http://ambermd.org/>

**Documentation:** <http://ambermd.org/Manuals.php>

## Access

Amber is only accessible to subscribers of the Laboratory for Molecular
Simulation. Please visit <https://lms.hprc.tamu.edu/> for subscription
rates.

### Loading the Module

To see all versions of Amber available:

`[ netID@cluster ~]$ `**`module   spider   amber`**

To load a particular version of Amber (Example: 18):

`[ netID@cluster ~]$ `**`module   load   Amber/18-intel-2017b`**

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

### Terra Examples

On Terra, to submit a batch job, run:

`[NetID@terra1 ~]$ `**`sbatch   `*`jobscript`***

#### MPI Job Example

    #!/bin/bash
    ## ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE            # Do not propagate environment
    #SBATCH --get-user-env=L         # Replicate login environment
    
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=amber         # Set the job name to "amber"
    #SBATCH --time=01:30:00          # Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=56              # Request 56 tasks
    #SBATCH --ntasks-per-node=28     # Request 28 tasks per node
    #SBATCH --mem=56G                # Request 56GB per node
    #SBATCH --output=amber.%j        # Send stdout/err to "amber.[jobID]"
    
    module purge
    ml Amber/18-intel-2017b
    
    # Please visit the Amber documentation for a full list of options for pmemd.MPI and the other programs availabe in the amber suite of programs.  
    mpirun -np $SLURM_NPROCS pmemd.MPI -O -i amber.in -o amber.out -p amber.prmtop -c amber.rst -r amber.rst -x amber.nc
    
    exit
