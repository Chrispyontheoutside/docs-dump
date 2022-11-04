# Quantum ESPRESSO

## Description

Quantum ESPRESSO is an integrated suite of Open-Source computer codes
for electronic-structure calculations and materials modeling at the
nanoscale. It is based on density-functional theory, plane waves, and
pseudopotentials.

Homepage: <https://www.quantum-espresso.org/>  

### Loading the Quantum ESPRESSO modules

**Grace Instructions:**

List the versions of Quantum ESPRESSO installed:

`mla espresso`

List the required module dependencies for *espresso\_version*:

`ml spider `*`espresso_version`*

Finally, load *espresso\_version* with the *dependencies* listed first
to setup your environment to run Quantum ESPRESSO:

`ml `*`dependencies`*` `*`espresso_version`*

**Terra Instructions**:

List the versions of Quantum ESPRESSO installed:

`mla espresso`

Finally, load *espresso\_version* to setup your environment to run ORCA:

`ml `*`espresso_version`*

### Terra Example Job file

A multicore, multinode (56 core) example: (Last updated April 4, 2020)

        #!/bin/bash

        ##NECESSARY JOB SPECIFICATIONS
        #SBATCH --job-name=QE                 # Sets the job name to QEJob
        #SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr
        #SBATCH --ntasks=56                   # Requests 56 cores
        #SBATCH --ntasks-per-node=28          # Requests 28 cores per node (2 node)
        #SBATCH --mem=56G                     # Requests 56GB of memory per node
        #SBATCH --error=QE.job.e%J            # Sends stderr to QE.job.e[jobID]
        #SBATCH --output=QE.job.o%J           # Sends stdout to QE.job.o[jobID]

        cd $SLURM_SUBMIT_DIR                  # Change to the directory the job was submitted from

        module purge                                    # purge all module
        module load  QuantumESPRESSO/6.4.1-intel-2019a  # load the module for Quantum Espresso                                               

        mpirun -np $SLURM_NPROCS pw.x < input > output  # run Quantum Espresso pw.x module

        exit                                  #exit when the job is done

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***

where *jobscript* is the name of the job file.

### Grace Example Job file

A multicore, multinode (96 core) example: (Last updated Septermber 1,
2021)

        #!/bin/bash

        ##NECESSARY JOB SPECIFICATIONS
        #SBATCH --job-name=QE                 # Sets the job name to QEJob
        #SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr
        #SBATCH --ntasks=96                   # Requests 96 cores
        #SBATCH --ntasks-per-node=48          # Requests 48 cores per node (2 node)
        #SBATCH --mem=356G                     # Requests 356GB of memory per node
        #SBATCH --error=QE.job.e%J            # Sends stderr to QE.job.e[jobID]
        #SBATCH --output=QE.job.o%J           # Sends stdout to QE.job.o[jobID]

        cd $SLURM_SUBMIT_DIR                  # change to the directory the job was submitted from

        module purge                                    # purge all module
        module load  GCC/8.3.0  OpenMPI/3.1.4 iccifort/2019.5.281  impi/2018.5.288 QuantumESPRESSO/6.6 # load the module for Quantum Espresso                                               

        mpirun -np $SLURM_NPROCS pw.x < input > output  # run Quantum Espresso pw.x module

        exit                                  #exit when the job is done

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***

where *jobscript* is the name of the job file.

### Ada Example Job file

A multicore (40 core) example: (Last updated April 4, 2020)

        #BSUB -J QE                            # sets the job name to QE.
        #BSUB -L /bin/bash                     # uses the bash login shell to initialize the job's execution environment.
        #BSUB -W 2:00                          # sets to 2 hours the job's runtime wall-clock limit.
        #BSUB -n 20                            # assigns 40 cores for execution.
        #BSUB -R "span[ptile=20]"              # assigns 20 cores per node.
        #BSUB -R "rusage[mem=2700]"            # reserves 2700MB per process/CPU for the job (2700MB * 20 Core = 54GB per node) 
        #BSUB -M 2700                          # sets to 2700MB (2700MB) the per process enforceable memory limit.
        #BSUB -o QE.job.o%J                    # directs the jobs standard output to QE.job.o[jobid]
        #BSUB -e QE.job.e%J                    # directs the jobs standard error to QE.job.e[jobid]

        cd $LS_SUBCWD                          # change to the directory the job was submitted from

        module purge                                    # purge all module
        module load  QuantumESPRESSO/6.4.1-intel-2019a  # load the module for Quantum Espresso                                               

        mpirun -np $LSB_MAX_NUM_PROCESSORS pw.x < input > output  # run Quantum Espresso pw.x module

        exit                                   #exit when the job is done

To submit the job to the queue, use the following command:

\[ NetID@ada1 ~\]$ **bsub \< *jobscript***

where *jobscript* is the name of the job file.

## Frequently Asked Questions
