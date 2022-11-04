# Psi4

## Description

Psi4 is an open-source quantum chemistry software built upon a modified
Python interpreter named Psithon that features on task automation. It
provides a wide variety of standard quantum chemical methods as well as
rare modules including the newly-developed density cumulant theory
(DCT), orbital-optimized post-Hartree–Fock methods, etc.

For more information, visit the [Psi4 Official
Website](https://psicode.org/).  
Documentation: [Psi4
Doc](https://psicode.org/psi4manual/master/index.html)

### License Information

PSI4 is free and distributed under the truly open-source LGPL3 license.
Use in education, research, and industry is encouraged.

### Loading the Psi4 modules

**Grace Instructions:**

List the versions of Psi4 installed:

`mla psi4`

If psi4 modules are not shown, try with the -f flag and run mla psi4
again:

`mla -f psi4`  
`mla psi4 `

List the required module dependencies for *PSI4version*:

`ml spider `*`PSI4version`*

Finally, load *PSI4version* with the *dependencies* listed first to
setup your environment to run Psi4:

`ml `*`dependencies`*` `*`PSI4version`*

**Terra Instructions**:

List the versions of Psi4 installed:

`mla psi4`

Finally, load *PSI4version* to setup your environment to run Psi4:

`ml `*`PSI4version`*

### Running Psi4 in Parallel

Control of threading in PSI4 can be accomplished at a variety of levels.
To change the number of threads at runtime, the psi4 -n flag may be
used.  
For example, to run a calculation on four threads:

`psi4 -i input.in -o output.out -n 4`

Note that is is not available for PsiAPI mode of operation.

### Grace Example Job file

A multicore (48 core) example: (Updated Jun. 2, 2021)

        #!/bin/bash
        ##NECESSARY JOB SPECIFICATIONS
        #SBATCH --job-name=psi4Job            # Sets the job name to psi4Job
        #SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr
        #SBATCH --ntasks=48                   # Requests 48 cores
        #SBATCH --ntasks-per-node=48          # Requests 48 cores per node (1 node)
        #SBATCH --mem=360G                    # Requests 360GB of memory per node
        #SBATCH --error=psi4Job.job.e%J       # Sends stderr to psi4Job.job.e[jobID]
        #SBATCH --output=psi4Job.job.o%J      # Sends stdout to psi4Job.job.o[jobID]<br \>
        cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from
        ml purge                              # purge all module
        ml iccifort/2019.5.281  impi/2018.5.288 PSI4/1.3.2-Python-3.7.4      # load the module for psi4
        psi4 -i psi4Job.in -o psi4Job.dat -n $SLURM_NPROCS      # run psi4
        exit                                              #exit when the job is done   

To submit the job to the queue, use the following command:

\[ NetID@Grace ~\]$ **sbatch *jobscript***

### Terra Example Job file

A multicore (28 core) example: (Updated Jun. 2, 2021)


        #!/bin/bash
        ##NECESSARY JOB SPECIFICATIONS
        #SBATCH --job-name=psi4Job            # Sets the job name to psi4Job
        #SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr
        #SBATCH --ntasks=28                   # Requests 28 cores
        #SBATCH --ntasks-per-node=28          # Requests 28 cores per node (1 node)
        #SBATCH --mem=56G                     # Requests 56GB of memory per node
        #SBATCH --error=psi4Job.job.e%J       # Sends stderr to psi4Job.job.e[jobID]
        #SBATCH --output=psi4Job.job.o%J      # Sends stdout to psi4Job.job.o[jobID]<br \>
        cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from
        ml purge                              # purge all module
        ml PSI4/1.2.1-intel-2018b-Python-2.7.15      # load the module for psi4
        psi4 -i psi4Job.in -o psi4Job.out -n $SLURM_NPROCS      # run psi4
        exit                                              #exit when the job is done  

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***
