# NWChem

## Description

NWChem is an open source high-performance computational chemistry code
actively developed by a consortium of developers and maintained by the
EMSL located at the Pacific Northwest National Laboratory (PNNL) in
Washington State. NWChem aims to provide its users with computational
chemistry tools that are scalable both in their ability to treat large
scientific computational chemistry problems efficiently, and in their
use of available parallel computing resources from high-performance
parallel supercomputers to conventional workstation clusters. NWChem
software can handle: biomolecules, nanostructures, and solid-state; from
quantum to classical, and all combinations; Gaussian basis functions or
plane-waves; scaling from one to thousands of processors; properties and
relativity.  
For more information, visit the [NWChem Official
Website](https://www.nwchem-sw.org/).  
Documentation: [NWChem Doc](http://github.com/nwchemgit/nwchem/wiki)

## License Information

The code is distributed as open-source under the terms of the
Educational Community License version 2.0 (ECL 2.0).

## Loading the NWChem modules

**Grace Instructions:**

List the versions of NWChem installed:

`mla nwchem`

List the required module dependencies for *version*:

`ml spider `*`NWChemversion`*

Finally, load *NWChemversion* with the *dependencies* listed first to
setup your environment to run NWChem:

`ml `*`dependencies`*` `*`NWChemversion`*

**Terra Instructions**:

List the versions of NWChem installed:

`ml spider NWChem`

Finally, load *NWChemversion* to setup your environment to run NWChem:

`ml `*`NWChemversion`*

### Grace Example Job file

A multinode (2 nodes), multicore (48 cores per node) example: (Updated
Jun. 5, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=NWChemJob            # Sets the job name to NWChemJob`  
`#SBATCH --time=2:00:00                  # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=96                     # Requests 96 cores`  
`#SBATCH --ntasks-per-node=48            # Requests 48 cores per node`  
`#SBATCH --mem=360G                      # Requests 360GB of memory per node`  
`#SBATCH --error=NWChemJob.job.e%J       # Sends stderr to NWChemJob.job.e[jobID]`  
`#SBATCH --output=NWChemJob.job.o%J      # Sends stdout to NWChemJob.job.o[jobID]<br \>`  
`cd  $SLURM_SUBMIT_DIR                   # Change to the directory where the job was submitted from`  
` ml purge                                                            # purge all module`  
`ml iccifort/2019.5.281  impi/2018.5.288 NWChem/7.0.0-Python-3.7.4   # load the modules for NWChem with the dependencies listed first`  
` mpirun nwchem NWChemJob.nw > NWChemJob.out                          # nwchem`  
` exit                                    # exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@Grace ~\]$ **sbatch *jobscript***

### Terra Example Job file

A multinode (2 nodes) multicore (28 cores per node) example: (Updated
Jun. 5, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=NWChemJob                   # Sets the job name to NWChemjob`  
`#SBATCH --time=2:00:00                         # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=56                            # Requests 56 cores`  
`#SBATCH --ntasks-per-node=28                   # Requests 28 cores per node`  
`#SBATCH --mem=56G                              # Requests 56GB of memory per node`  
`#SBATCH --error=NWChemJob.job.e%J              # Sends stderr to NWChemJob.job.e[jobID]`  
`#SBATCH --output=NWChemJob.job.o%J             # Sends stdout to NWChemJob.job.o[jobID]<br \>`  
`cd  $SLURM_SUBMIT_DIR                          # Change to the directory where the job was submitted from`  
` ml purge                                       # purge all module`  
`ml NWChem/7.0.0-intel-2019b-Python-3.7.4       # load the module for NWChem`  
` mpirun nwchem NWChemJob.nw > NWChemJob.out     # run NWChem`  
` exit                                           #exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***
