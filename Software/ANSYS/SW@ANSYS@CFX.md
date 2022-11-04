# CFX

## Description

ANSYS CFX is a high-performance computational fluid dynamics (CFD) software tool that delivers reliable and accurate solutions quickly and robustly across a wide range of CFD and multi-physics applications. - Homepage: http://www.ansys.com/Products/Fluids/ANSYS-CFX

## Help

* Getting started materials: http://www.ansys.com/academic/free-student-products/support-resources - For example:
    * [Cornell University MOOC][1] for CFD and Mechanical
    * [ANSYS Maxwell Tutorials][2] - Allison Kipple, Northern Arizona University

* [Student Forum][3]. Register [here][4] and discuss simulation with students worldwide    
* Access to advanced material and video - see instructions [here][5]

### Documentation

The PDF documentation for ANSYS release 18.2 is available for our users and can be found at: https://hprc.tamu.edu/softwareDocs/ansys/ 

## Access

ANSYS is open to all HPRC users when used within the terms of our ANSYS license agreement. 

**<span style="color:red"> IMPORTANT NOTE REGARDING THE ANSYS LICENSE: </span>** **(July 12, 2017)**
```php
Use of ANSYS is only permitted for users that are affiliated with Texas A&M at 
College Station.  Users meeting this criteria are permitted to use ANSYS on HPRC 
systems from anywhere in the United States (including Alaska and Hawaii).  Use 
of this software outside the designated area represents a breach of the license 
and any users caught doing so may be subject to account suspension and/or other action.
```

If you have particular concerns about whether specific usage falls within the TAMU HPRC license, please send an email to the HPRC Helpdesk. Usage of ANSYS is restricted by the number of available tokens. To see the number of available tokens, use the [License Checker Tool](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink").

### Loading the module

To see all versions of ANSYS available on our systems: 
```php 
[NetID@cluster ~]$ module spider ANSYS
```
To load a particular version of ANSYS (Example: 17.1): 
```php
[NetID@cluster ~]$ module load ANSYS/19.3
```

### Known Issues

There is a known issue when using the Ansys GUI for any version of Ansys. The Geometry Editor in the Ansys Workbench will not run properly without also loading an NVIDIA module.

To bypass this bug, load the OpenGL/NVIDIA module before running the Ansys Workbench: 
```php
[ netID@cluster ~]$ module load OpenGL/NVIDIA
```
There is a known issue with all Ansys versions on **Terra** that requires unsetting a Slurm environment variable. To prevent this error, please make sure to have the following line in your job script **before** the launch command. 

```php
unset SLURM_GTIDS
```

The same error occurs when using the Ansys GUI in a VNC job on **Terra**. To prevent this error, please use the following command in your VNC job: 

```php
[ netID@terra ~]$ unset SLURM_GTIDS
```

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use non-interactive batch jobs for resource-intensive and/or multiple-core processing. Users are requested to be **<span style="color:darkgreen">responsible</span>** and **<span style="color:darkgreen">courteous to other users</span>** when using software on the login nodes. 
The most important processing limits here are:

* **ONE HOUR** of **PROCESSING TIME** per login session.
* **EIGHT CORES** per login session on the same node or (cumulatively) across all login nodes.

**<span style="color:red"> Anyone found violating the processing limits will have their processes killed without warning. Repeated violation of these limits will result in account suspension.</span>**

**<span style="color:darkgreen">Note </span>**: <span style="color:darkgreen">Your login session will disconnect after</span> **<span style = "color:darkgreen">one hour</span>** <span style="color:darkgreen">of inactivity. </span>

## Usage on the Computer Nodes

Non-interactive batch jobs on the compute nodes allows for resource-demanding processing. Non-interactive jobs have higher limits on the number of cores, amount of memory, and runtime length. 

For instructions on how to create and submit a batch job, please see the appropriate wiki page for each respective cluster: 

  - Terra: [ About Terra Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Grace: [ About Grace Batch Processing](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink")

### Terra Examples

**Example 1:** A serial (single core) CFX Job example: (Last updated February 12, 2018) 
```php
#!/bin/bash

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=CFXJob       # Sets the job name to CFXJob
#SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
#SBATCH --ntasks=1              # Requests 1 core
#SBATCH --ntasks-per-node=1     # Requests 1 core per node (1 node)
#SBATCH --mem=5G                # Requests 5GB of memory per node
#SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

## Load the necessary modules
module purge
module load ANSYS/18.0

## Known error fix
unset SLURM_GTIDS 

## Launch the CFX Solver with proper parameters
cfx5solve -batch -def FileName.def 
```

**Example 2:** A parallel (multiple cores) CFX Job example: (Last updated February 12, 2018) 
```php
#!/bin/bash

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=CFXJob       # Sets the job name to CFXJob
#SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
#SBATCH --ntasks=10             # Requests 10 cores
#SBATCH --ntasks-per-node=10    # Requests 10 cores per node (1 node)
#SBATCH --mem=50G               # Requests 50GB of memory per node
#SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

## Load the necessary modules
module purge
module load ANSYS/18.0
  
## Known error fix
unset SLURM_GTIDS 
  
## Launch the CFX Solver with proper parameters
cfx5solve -batch -def FileName.def -start-method "Intel MPI Local Parallel" -part 10 
```

**Example 3:** A parallel (multiple cores, multiple nodes) CFX Job example: (Last updated February 12, 2018)
```php
#!/bin/bash

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=CFXJob       # Sets the job name to CFXJob
#SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
#SBATCH --ntasks=20             # Requests 20 cores
#SBATCH --ntasks-per-node=10    # Requests 10 cores per node (1 node)
#SBATCH --mem=50G               # Requests 50GB of memory per node
#SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

## Load the necessary modules
module purge
module load ANSYS/18.2
 
## Known error fix
unset SLURM_GTIDS 

## reading this script will set the $CFX_DIST_LIST variable to the compute nodes and the number of cores to use for each node 
source /sw/local/bin/cfx_dist_list.sh
 
## Launch the CFX Solver with proper parameters
cfx5solve -batch -def FileName.def -start-method "Intel MPI Distributed Parallel" -par-dist $CFX_DIST_LIST
```
To submit the batch job, run: (where jobscript is a file that looks like one of the above examples) 

```php
[ NetID@terra ~]$ sbatch jobscript
```

## Usage on VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI) without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are limited to a single node (Terra: 28 cores/64GB). There are fewer VNC nodes than comparable compute nodes.

For more information, including instructions, on using software on the VNC nodes, please visit our [Terra Remote Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page. 



[1]: https://www.edx.org/course/a-hands-on-introduction-to-engineering-simulations
[2]: https://in.nau.edu/clean-energy-research/air-x-simulation/
[3]: https://studentcommunity.ansys.com/
[4]: https://studentcommunity.ansys.com/
[5]: https://studentcommunity.ansys.com/thread/experience-our-new-online-help/
