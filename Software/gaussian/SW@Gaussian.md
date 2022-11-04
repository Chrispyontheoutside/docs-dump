# Gaussian & GaussView 6

**Gaussian is restricted software.**

Usage of this software is restricted to [Laboratory for Molecular
Simulation (LMS)](https://lms.hprc.tamu.edu/) subscribers. If you
believe you are eligible to use Gaussian on our clusters, please email
the HPRC Help Desk with the request and justification.

## Description

Gaussian is a software package used for calculating molecular electronic
structure and properties. Gaussian is used by chemists, chemical
engineers, biochemists and physicists for research in established and
emerging areas of chemical interest. This package includes a wide range
of *ab initio* and semi-empirical methods for energy, gradient,
frequency and property calculations.  
GaussView 6 is the latest version of a graphical interface that is
native to Gaussian. It enables users to create Gaussian input files from
a graphical interface and visualize the calculation results (plot
molecular orbitals and other properties, animate vibrations, visualize
predicted spectra, etc.).  
Homepage: [Gaussian.com](http://gaussian.com/)  
Manual: [Gaussian 16 manual](http://gaussian.com/man/)

Those who have been specifically approved for access will be able to run
GaussView 6 as detailed in the sections below.  
\==Using GaussView 6== To setup your environment to run GaussView 6, you
will need to load a Gaussian module.

Find the versions of Gaussian installed:

`mla gaussian`

Load the module. Replace *GaussianVersion* with the version of Gaussian
you wish to use.

`ml `*`GaussianVersion`*

You should now be able to run GaussView 6 using the command:

`gv`

Note: If OpenGL does not work properly, please use MesaGL instead:

`export USE_MESAGL=1`

MesaGL will cause slower rendering, therefore only use it if needed.

## Running G16

Those who have been specifically approved for access will be able to run
Gaussian as detailed in the sections below.

Gaussian can only run parallel with shared memory, therefore you cannot
use more than 1 node and are limited to a maximum of 48 core on grace,
28 core on Terra and 20 core on Ada.

Below are example job files for Gaussian 16. You can create your own job
files to fit your needs or you may use a script specifically setup to
create and submit Gaussian 16 job files: **qprep**  
Help for qprep can be obtained by running qprep -h

### Terra Example Job file

A multicore (28 core) example: (Last updated Sept. 14, 2020)
```php
#!/bin/bash
##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=GaussianJob         # Sets the job name to GaussianJob
#SBATCH --time=2:00:00                 # Sets the runtime limit to 2 hr
#SBATCH --ntasks=28                    # Requests 28 cores
#SBATCH --ntasks-per-node=28           # Requests 28 cores per node (1 node)
#SBATCH --mem=56G                      # Requests 56GB of memory per node
#SBATCH --error=GaussianJob.job.e%J    # Sends stderr to GaussianJob.job.e[jobID]
#SBATCH --output=GaussianJob.job.o%J   # Sends stdout to GaussianJob.job.o[jobID]

cd $TMPDIR                             # change to the local disk temporary directory

export g16root=/sw/group/lms/sw/g16_B01   # set g16root variable
. $g16root/g16/bsd/g16.profile         # source g16.profile to setup environment for g16

echo -P- $SLURM_NPROCS > Default.Route # set the number of cores for gaussian to use ($SLURM_NPROCS variable is set to the number of core requested by #SBATCH --ntasks)
echo -M- 50GB >> Default.Route         # set the memory for gaussian to use (50GB)

module purge                           # purge all module

g16  < $SLURM_SUBMIT_DIR/GaussianJob.com  > $SLURM_SUBMIT_DIR/GaussianJob.log   # run gaussian

exit                                   #exit when the job is done
```


To submit the job to the queue, use the following command:

[ NetID@terra1 ~]$ **sbatch *jobscript***

### Grace Example Job file

A multicore (48 core) example: (Last updated July 21, 2021)
```
#!/bin/bash
##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=GaussianJob         # Sets the job name to GaussianJob
#SBATCH --time=2:00:00                 # Sets the runtime limit to 2 hr
#SBATCH --ntasks=48                    # Requests 48 cores
#SBATCH --ntasks-per-node=48           # Requests 48 cores per node (always specify 1 node for gaussian jobs)
#SBATCH --mem=360G                      # Requests 360GB of memory per node
#SBATCH --error=GaussianJob.job.e%J    # Sends stderr to GaussianJob.job.e[jobID]
#SBATCH --output=GaussianJob.job.o%J   # Sends stdout to GaussianJob.job.o[jobID]

cd $TMPDIR                             # change to the local disk temporary directory

export g16root=/sw/restricted/lms/sw/Gaussian/g16_C01   # set g16root variable
. $g16root/g16/bsd/g16.profile         # source g16.profile to setup environment for g16

echo -P- $SLURM_NPROCS > Default.Route # set the number of cores for gaussian to use ($SLURM_NPROCS variable is set to the number of core requested by #SBATCH --ntasks)
echo -M- 360GB >> Default.Route         # set the memory for gaussian to use (360GB)

module purge                           # purge all module

g16  < $SLURM_SUBMIT_DIR/GaussianJob.com  > $SLURM_SUBMIT_DIR/GaussianJob.log   # run gaussian

exit                                   #exit when the job is done
```


To submit the job to the queue, use the following command:

[ NetID@grace2 ~$] **sbatch *jobscript***

## Frequently Asked Questions
