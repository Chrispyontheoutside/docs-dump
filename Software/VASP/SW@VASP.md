# VASP

**VASP is restricted software.**

Usage of this software is restricted only to those determined eligible
by the license holder. If you believe you are eligible to use VASP on
our clusters, please email the HPRC Help Desk with the request and
justification.

VASP [homepage](https://www.vasp.at/)

The Vienna Ab initio Simulation Package (VASP) is a computer program for
atomic scale materials modelling, e.g. electronic structure calculations
and quantum-mechanical molecular dynamics, from first principles.

VASP is installed on Grace and is accessed through the [ hierarchical
module](/kb3/User-Guides/Grace/Grace@QuickStart/#finding-software "wikilink") system:

To list the versions of VASP installed on Grace use the command:

`mla vasp`

To list the required module dependencies for *vaspversion* use the
command:

`ml spider `*`vaspversion`*

Finally, load the required dependencies and the desired VASP version to
setup your environment to run vasp:

`ml `*`dependencies`*` `*`vaspversion`*

Sample VASP Job file for Grace:

`#!/bin/bash`  
`#SBATCH -J JobName               #Job Name (JobName)`  
`#SBATCH -t 1:00:00               #Wall time h:m:s (1 hour)`  
`#SBATCH -N 2                     #Number of nodes (2 nodes)`  
`#SBATCH --ntasks-per-node=48     #Cores per node (48 cores per node)`  
`#SBATCH --mem=324G               #Memory per node (324 GB of memory per node)`  
`#SBATCH -o JobName.o%j           #standard output file (JobName.o`*`jobnumber`*`)`  
`#SBATCH -e JobName.e%j           #standard error file (JobName.e`*`jobnumber`*`)`  
  
`ml purge                         # purge all modules to start with a clean environment`  
  
`# load the appropriate vasp module with the dependencies listed first (ie intel/2020a)`  
`ml intel/2020a vasp/5.4.4.pl2-vtst-wannier-beef`  
`  `  
`ml list                          # list the modules currently loaded to have a record of the loaded modules`  
  
`export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so`  
`srun vasp_std                       # run the standard version of vasp (vasp_std)`

## AFLOW

[Automatic FLOW for Materials Discovery](http://aflow.org/)

To load AFLOW module on Grace:

`ml GCC/10.2.0 AFLOW/3.2.11 `
