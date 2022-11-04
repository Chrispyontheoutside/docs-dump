# Dalton Suite

## Description

The Dalton suite is a powerful tool for electronic structure
calculations that consists of two separate executables, **Dalton** and
**LSDalton**. The Dalton code supports calculations of molecular
properties at different levels of theory (HF, DFT, MCSCF, MC-srDFT, CC,
*etc.*) , whereas LSDalton is a linear-scaling HF and DFT code suitable
for large molecular systems. A longer description of the Dalton and
LSDalton programs features can be found
[here](https://daltonprogram.org/features/). The Dalton suite is
licensed under the GNU Lesser General Public License, Version 2.1.  
For more information, visit the [Dalton Official
Website](https://daltonprogram.org/).  

### Loading the **Dalton** Module

**Grace Instructions:**  
To purge unnecessary modules before getting started:

    [netID@grace2]ml purge

List the versions of Dalton installed (as of 07/26/2021):

    [netID@grace2] mla dalton   
    Dalton/2020.0

List the required module dependencies for *DaltonVersion*:

\[netID@grace2\] ml spider Dalton/2020.0

Finally, load *DaltonVersion* with the *dependencies* listed first to
setup your environment to run Dalton:

\[netID@grace2\] ml intel/2020b Dalton/2020.0

### Grace Example Job file for Dalton

A multicore (48 cores per node) example: (Updated July 26, 2021)

    #!/bin/bash  
    ##NECESSARY JOB SPECIFICATIONS  
    #SBATCH --job-name=dalton             # Sets the job name to dalton  
    #SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr  
    #SBATCH --ntasks=48                   # Requests 48 cores  
    #SBATCH --ntasks-per-node=48          # Requests 48 cores per node (1 node)  
    #SBATCH --mem=360G                    # Requests 360GB of memory per node  
    #SBATCH --error=dalton.job.e%J        # Sends stderr to dalton.job.e[jobID]  
    #SBATCH --output=dalton.job.o%J       # Sends stdout to dalton.job.o[jobID]   
     cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from  
    ml purge                              # purge all module  
    ml intel/2020b Dalton/2020.0          # load the module for dalton  
     export DALTON_NUM_MPI_PROCS=$SLURM_NPROCS   # set OMP_NUM_THREADS to the number of cores requested above  
    dalton -N $SLURM_NPROCS filename.dal filename.mol   # run Dalton   
     exit                                  #exit when the job is done

To submit the job to the queue, use the following command:

\[NetID@Grace ~\]$ **sbatch *jobscript***
