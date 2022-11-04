# OpenFOAM

  - Access

You must load the OpenFOAM module first, and then sourcing its bashrc
file, before using any OpenFOAM commands. There are multiple versions of
OpenFOAM installed on our clusters. Their module name has the form
<i>OpenFOAM/version-tool\_chain</i>, where <i>version</i> is the version
of the OpenFOAM the module file provides, and <i>tool\_chain</i> is the
compiler used for building the OpenFOAM. Once you decide which module to
use, please run these two commands:

    module load OpenFOAM/version-tool_chain
    source $FOAM_BASH

  - An LSF Batch Example

<!-- end list -->

    #BSUB -J openfoam-test       # sets the job name to openfoam-test.
    #BSUB -L /bin/bash           # uses the bash login shell to initialize the job's execution environment.
    #BSUB -W 5:00                # sets to 5 hours the job's runtime wall-clock limit.
    #BSUB -n 20                  # assigns 20 core for execution.
    #BSUB -R "span[ptile=20]"    # assigns 20 core per node.
    #BSUB -R "rusage[mem=2700]"  # reserves ~2.7GB per process/CPU for the job 
    #BSUB -M 2700            # sets to ~2.7GB the per process enforceable memory limit.
    #BSUB -o openfoam.out.%J          # directs the job's standard output to openfoam.out.jobid 
    
    
    ## Load the necessary modules
    module purge
    module load OpenFOAM/4.1-intel-2017A-Python-2.7.12
    source $FOAM_BASH
    
    ## 
    blockMesh
    setFields
    mpirun interFoam -parallel [options]
    reconstructPar
