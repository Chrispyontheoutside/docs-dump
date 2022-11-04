# Workbench

## Description 

ANSYS Workbench simulation software enables organizations to confidently predict how their products will operate in the real world. - Homepage: http://www.ansys.com/Products/Platform

## Help

Getting started materials: http://www.ansys.com/academic/free-student-products/support-resources - For example:

* [Cornell University MOOC][1] for CFD and Mechanical

* [ANSYS Maxwell Tutorials][2] - Allison Kipple, Northern Arizona University

[Student Forum.][3] Register [here][4] and discuss simulation with students worldwide

Access to advanced material and video - see instructions [here][5]

### Documentation

The PDF documentation for ANSYS release 18.2 is available for our users and can be found at: https://hprc.tamu.edu/softwareDocs/ansys/

## Access

ANSYS is open to all HPRC users when used within the terms of our ANSYS license agreement.

**<span style="color:red"> IMPORTANT NOTE REGARDING THE ANSYS LICENSE:</span> (July 12, 2017)** 

```php
Use of ANSYS is only permitted for users that are affiliated with Texas A&M at 

College Station.  Users meeting this criteria are permitted to use ANSYS on HPRC 

systems from anywhere in the United States (including Alaska and Hawaii).  Use 

of this software outside the designated area represents a breach of the license 

and any users caught doing so may be subject to account suspension and/or other action.
```

If you have particular concerns about whether specific usage falls within the TAMU HPRC license, please send an email to the HPRC Helpdesk. Usage of ANSYS is restricted by the number of available tokens. To see the number of available tokens, use the [ License Checker Tool](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink").

### Loading the Module

To see all versions of ANSYS available on Ada:

```php
[ netID@cluster ~]$ module spider ANSYS
```

To load a particular version of Ansys on Ada (Example: 19.3):

```php
[ netID@cluster ~]$ module load ANSYS/19.3
```

### Known Issues
There is a known issue when using the Ansys GUI for any version of Ansys. The Geometry Editor in the Ansys Workbench will not run properly without also loading an NVIDIA module.

To bypass this bug, load the **OpenGL/NVIDIA** module before running the Ansys Workbench:

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

### Terra Example

**Example 1**: A serial (single core) TurboGrid Job example: (Last updated March 24, 2017)

```php
#!/bin/bash

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=WorkbenchJob # Sets the job name to WorkbenchJob
#SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
#SBATCH --ntasks=1              # Requests 1 core
#SBATCH --ntasks-per-node=1     # Requests 1 core per node (1 node)
#SBATCH --mem=5G                # Requests 5GB of memory per node
#SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

## Load the necessary modules
module purge
module load ANSYS/19.3

## Known error fix
unset SLURM_GTIDS 

## Launch the solver with proper parameters
runwb2 -R fileName.wbjn -B
```

To submit the batch job, run: (where jobscript is a file that looks like one of the above examples)

```php
[ NetID@terra ~]$ sbatch jobscript
```

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI) without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are limited to a single node (Terra: 28 cores/64GB). There are fewer VNC nodes than comparable compute nodes.

For more information, including instructions, on using software on the VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.

### Running the ANSYS Workbench GUI

While in a VNC job, use runwb2 (with vglrun) to start the ANSYS GUI:

```php
[netID@gpu ~]$ vglrun runwb2
```

### ANSYS Workbench GUI Quick Start Guide

For moderately detailed instructions on launching the ANSYS Workbench GUI for the first time, please see the [ ANSYS Workbench Quick Start
Guide](/kb3/Software/ANSYS/SW@ANSYS@Workbench@QuickStart/ "wikilink").


[1]: https://www.edx.org/course/hands-introduction-engineering-cornellx-engr2000x-0
[2]: https://nau.edu/CEFNS/Engineering/Mechanical/Research-and-Labs/Energy/Education/Air-X-Simulation/
[3]: https://studentcommunity.ansys.com/
[4]: https://studentcommunity.ansys.com/
[5]: https://studentcommunity.ansys.com/thread/experience-our-new-online-help/
