# ORCA

## Description

ORCA is a flexible, efficient and easy-to-use general purpose for
quantum chemistry with specific emphasis on spectroscopic properties of
open-shell molecules. It features a wide variety of standard quantum
chemical methods ranging from semiempirical methods to DFT to single and
multi-reference correlated ab initio methods. It can also treat
environmental and relativistic effects.

For more information, visit the [ORCA Official
Website](https://orcaforum.kofo.mpg.de/).  
Useful links: [ORCA Input
Library](https://sites.google.com/site/orcainputlibrary/), [ORCA
Tutorials](https://www.orcasoftware.de/tutorials/)

## Access

Access to ORCA is granted to users who are able to show that they have
registered to download ORCA.

### ORCA Registration

First, visit [this link](https://orcaforum.kofo.mpg.de/). This page
requires several pieces of information to complete registration.
Acceptance of an End User License Agreement (EULA) containing the terms
of registration is also required.

Once accepted, several download links will be available.

A registration verification email will also be sent containing a copy of
the EULA. This email will provide proof of registration to HPRC, which
is necessary for use of ORCA on the clusters.

Please send a copy of this email to help@hprc.tamu.edu to get access.

### License Information

The use of ORCA is restricted to academic purposes in an academic
environment, i.e. at schools, universities and colleges. It is
prohibited to use ORCA in collaborations or cooperations with
non-academic partners, including private companies, non-profit and
governmental organisations. This includes third-party funded projects
involving non-academic partners. ORCA is licensed to single users as
well as research groups. For a research group, the research group leader
is responsible for the compliance of his/her group with ORCAs End User
License Agreement. If results obtained with ORCA are published in the
scientific literature, the licensee shall reference the program as "F.
Neese: The ORCA program system (WIREs Comput Mol Sci 2012, 2: 73-78)".
Using specific methods included in ORCA may require citing additional
articles, as described in the manual. The licensee agrees to honor the
request to cite additional papers as appropriate. If a patent is
registered as a result of the use of ORCA, the licensee shall notify the
Max-Planck Institute. The Max-Planck-Institute is entitled to use the
information in the patent registration for marketing purposes and to
publish it for this specific purpose. If you are unsure whether you are
eligible for the academic license, please contact:
orca.license@cec.mpg.de

### Loading the ORCA modules

**Grace Instructions:**

List the versions of ORCA installed:

`mla ORCA`

List the required module dependencies for *ORCAversion*:

`ml spider `*`ORCAversion`*

Finally, load *ORCAversion* with the *dependencies* listed first to
setup your environment to run ORCA:

`ml `*`dependencies`*` `*`ORCAversion`*

**Terra Instructions**:

List the versions of ORCA installed:

`mla ORCA`

Finally, load *ORCAversion* to setup your environment to run ORCA:

`ml `*`ORCAversion`*

### Running ORCA in Parallel

ORCA takes care of communicating with the OpenMPI interface on its own
when needed. ORCA should **NOT** be started with mpirun: e.g. mpirun -np
28 orca *etc.*, like many MPI programs. Use the **\!PalX** keyword in
the inputfile to tell ORCA to start multiple processes. Everything from
PAL2 to PAL8 is recognized. For example, to start a 4-process job, the
input file might look like this:

`! B3LYP def2-SVP Opt PAL4`

or using block input to start a 28-process job:

`! B3LYP def2-SVP Opt`  
`%pal`  
`nprocs 28`  
`end`

### Grace Example Job file

A multicore (48 core) example: (Updated May. 23, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=orcaJob            # Sets the job name to orcaJob`  
`#SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=48                   # Requests 28 cores`  
`#SBATCH --ntasks-per-node=48          # Requests 28 cores per node (1 node)`  
`#SBATCH --mem=360G                    # Requests 360GB of memory per node`  
`#SBATCH --error=orcaJob.job.e%J       # Sends stderr to orcaJob.job.e[jobID]`  
`#SBATCH --output=orcaJob.job.o%J      # Sends stdout to orcaJob.job.o[jobID]<br \>`  
`cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from`  
` ml purge                              # purge all module`  
`ml GCC/8.3.0 OpenMPI/3.1.4 ORCA/4.2.1-shared      # load the module for ORCA`  
` $EBROOTORCA/orca orcaJob.inp  >  orcaJob.out      # run ORCA`  
` exit                                              #exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@Grace ~\]$ **sbatch *jobscript***

### Terra Example Job file

A multicore (28 core) example: (Updated Aug. 16, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=orcaJob            # Sets the job name to orcaJob`  
`#SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=28                   # Requests 28 cores`  
`#SBATCH --ntasks-per-node=28          # Requests 28 cores per node (1 node)`  
`#SBATCH --mem=56G                     # Requests 56GB of memory per node`  
`#SBATCH --error=orcaJob.job.e%J       # Sends stderr to orcaJob.job.e[jobID]`  
`#SBATCH --output=orcaJob.job.o%J      # Sends stdout to orcaJob.job.o[jobID]<br \>`  
`cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from`  
` ml purge                          # purge all module`  
`ml ORCA/5.0.1-gompi-2021a-shared      # load the module for Orca`  
` $EBROOTORCA/orca orcaJob.inp  >  orcaJob.out      # run ORCA`  
` exit                                              #exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***

A multinode (56 core) example: (Updated Aug. 16, 2021)

`#!/bin/bash`  
`##NECESSARY JOB SPECIFICATIONS`  
`#SBATCH --job-name=orcaJob            # Sets the job name to orcaJob`  
`#SBATCH --time=2:00:00                # Sets the runtime limit to 2 hr`  
`#SBATCH --ntasks=56                   # Requests 28 cores`  
`#SBATCH --ntasks-per-node=28          # Requests 28 cores per node (2 node)`  
`#SBATCH --mem=56G                     # Requests 56GB of memory per node`  
`#SBATCH --error=orcaJob.job.e%J       # Sends stderr to orcaJob.job.e[jobID]`  
`#SBATCH --output=orcaJob.job.o%J      # Sends stdout to orcaJob.job.o[jobID]<br \>`  
`cd  $SLURM_SUBMIT_DIR                 # Change to the directory where the job was submitted from`  
` ml purge                          # purge all module`  
`ml ORCA/5.0.1-gompi-2021a-shared      # load the module for Orca`  
` $EBROOTORCA/orca orcaJob.inp  >  orcaJob.out      # run ORCA`  
` exit                                              #exit when the job is done `  

To submit the job to the queue, use the following command:

\[ NetID@terra1 ~\]$ **sbatch *jobscript***  
  
For further instructions on how to create and submit a batch job, please
see the appropriate wiki page for each respective cluster:

  - Terra: [ About Terra Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Grace: [ About Grace Batch Processing](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink")

## Using xTB with ORCA

ORCA 4.2.1 now supports the semiempirical quantum mechanical methods
GFNn-xTB with an IO-based interface to the
[xtb](https://xtb-docs.readthedocs.io/) binary. The otool\_xtb wrapper
script has been added to the directory that contains the ORCA binaries.

To use ORCA with xTB, you will need to load both the ORCA and xtb
modules.

**Grace** module load example with xtb:

`ml GCC/8.3.0 OpenMPI/3.1.4 ORCA/4.2.1-shared xtb/6.2.3`

**Terra** module load example with xtb:

`ml ORCA/4.2.1-gompi-2019b-shared xtb/6.2.3-foss-2019b`

## Using CREST with xTB

Conformer-Rotamer Ensemble Sampling Tool
([CREST](https://xtb-docs.readthedocs.io/en/latest/crest.html/)) is an
utility/driver program for the xtb program. CREST Version 2.9 has been
installed on grace and terra and is available by loading the xtb module.

**Grace** module load example with xtb:

`ml GCC/8.3.0  OpenMPI/3.1.4 xtb/6.2.3`

**Terra** module load example with xtb:

`ml xtb/6.2.3-foss-2019b`
