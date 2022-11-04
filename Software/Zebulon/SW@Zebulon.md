# Zébulon

## Description

Zébulon is a non-linear finite element solver of the Z-set suite which
addresses the whole range of problems arising in structural mechanics.
It is jointly developed by École des Mines ParisTech (France), Onera –
the French Aerospace Lab, and NW Numerics & Moldeling, Inc
(USA). Zebulon may use multi-threading to accelerate material
integration and linear system resolution on a single shared memory
machine.  
For more information, visit the [Zébulon Official
Website](http://www.zset-software.com/products/zebulon/).  
The TAMU License for Zébulon is for Academic Research only.

## Loading the Zébulon modules

**Grace Instructions:**

List the versions of Zébulon installed:

`mla zebulon`

Load a specific *ZebulonVersion* to setup your environment to run
Zébulon:

`ml `*`ZebulonVersion`*

**Terra Instructions**:

List the versions of Zébulon installed:

`ml spider Zebulon`

Finally, load *NWChemversion* to setup your environment to run Zébulon:

`ml `*`ZebulonVersion`*

### Grace Example Job file

A multicore (48 cores per node) example: (Updated Jun. 5, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=ZebulonJob           # Sets the job name to ZebulonJob`  
`#SBATCH --time=2:00:00                  # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=48                     # Requests 48 cores`  
`#SBATCH --ntasks-per-node=48            # Requests 48 cores per node`  
`#SBATCH --mem=360G                      # Requests 360GB of memory per node`  
`#SBATCH --error=ZebulonJob.job.e%J      # Sends stderr to ZebulonJob.job.e[jobID]`  
`#SBATCH --output=ZebulonJob.job.o%J     # Sends stdout to ZebulonJob.job.o[jobID]<br \> `  
`ml purge                                                            # purge all module`  
`ml ZEBULON/z904                                                     # load the modules for ZEBULON/z904 `  
`ml list                                                             # list the modules loaded `  
` export OMP_NUM_THREADS = $SLURM_NPROCS                              # set OMP_NUM_THREADS to the number of cores requested above`  
` Zrun -smp $SLURM_NPROCS calcul.inp > calcul.out                     # zrun`  
` exit                                                                # exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@Grace ~\]$ **sbatch *jobscript***

### Terra Example Job file

A multicore (28 cores per node) example: (Updated Jun. 29, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=ZebulonJob           # Sets the job name to ZebulonJob`  
`#SBATCH --time=2:00:00                  # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=28                     # Requests 28 cores`  
`#SBATCH --ntasks-per-node=28            # Requests 28 cores per node`  
`#SBATCH --mem=56G                      # Requests 56GB of memory per node`  
`#SBATCH --error=ZebulonJob.job.e%J      # Sends stderr to ZebulonJob.job.e[jobID]`  
`#SBATCH --output=ZebulonJob.job.o%J     # Sends stdout to ZebulonJob.job.o[jobID]<br \> `  
`ml purge                                                            # purge all module`  
`ml ZEBULON/z904                                                     # load the modules for ZEBULON/z904 `  
`ml list                                                             # list the modules loaded `  
` export OMP_NUM_THREADS = $SLURM_NPROCS                              # set OMP_NUM_THREADS to the number of cores requested above`  
` Zrun -smp $SLURM_NPROCS calcul.inp > calcul.out                     # zrun`  
` exit                                                                # exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@Grace ~\]$ **sbatch *jobscript***
