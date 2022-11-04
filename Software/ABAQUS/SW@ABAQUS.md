# Abaqus

## Description

Finite Element Analysis software for modeling, visualization, and
best-in-class implicit and explicit dynamics FEA. - Homepage:
<http://www.3ds.com/products-services/simulia/products/abaqus/>

### Documentation

We have documentation available for the following versions of ABAQUS:

  - [ABAQUS 2016](https://hprc.tamu.edu/softwareDocs/abaqus/v2016/)
  - [ABAQUS 2017](https://hprc.tamu.edu/softwareDocs/abaqus/2017)
  - [ABAQUS 2018](https://hprc.tamu.edu/softwareDocs/abaqus/2018)
  - [ABAQUS 2021](https://hprc.tamu.edu/softwareDocs/abaqus/2021)

<font color=red>**Note:** The search functions are currently not working
for all Abaqus documentation versions.</font>

<font color=teal>**Note:** You will need to be within the TAMU firewall
in order to view these documents. You will need to either be on campus
OR connect using VPN. Information on the TAMU VPN can be found
[here](https://u.tamu.edu/KB0010938). </font>

### Knowledge Base

TAMU ABAQUS users can also access the Knowledge Base at
<https://www.3ds.com/support/knowledge-base/> under the Simulia
brand/category for technical questions about ABAQUS.

You can also create an account at <https://swym.3ds.com/#community:73>
to get access to more resources, including the full software
documentation, tutorials, training and tips, eSeminars, articles and
papers.

### Tutorials

  - [Using Abaqus CAE to build and simulate models using finite element
    methods](https://hprc.tamu.edu/files/events/usermeetings/RCWeek2017/workshops/AcademicWorkshopOne-Abaqus-final.pdf)
  - [Using TOSCA to optimize a part’s physical shape and material
    properties](https://hprc.tamu.edu/files/events/usermeetings/RCWeek2017/workshops/AcademicWorkshopTwo-Tosca-final.pdf)

## Access

Abaqus is open to all HPRC users when used within the terms of our
license agreement. If you have particular concerns about whether
specific usage falls within the TAMU HPRC license, please send an email
to the HPRC Helpdesk.

### Loading the Module

To see all versions of Abaqus available on Ada:

`[NetID@cluster ~]$ `**`module   spider   ABAQUS`**

To load a particular version of Abaqus use: (Example: 2017)

`[NetID@cluster ~]$ `**`module   load   ABAQUS/2017`**

<font color=teal>**Note:** New versions of software become available
periodically. Version numbers may change.</font>

### License Tokens

Usage of Abaqus is restricted by the number of available tokens. One
instance of Abaqus cae requires one (1) cae token. An Abaqus job
requires tokens based on the number of cores the job will use. The
formula for calculating licenses that are needed is:

` int(5 * (cores)^0.422)`

To see the number of available tokens, use the [ License Checker
Tool](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink").

### Known Issues

#### Terra Multinode Usage

Abaqus 6.14 uses a MPI library (IBM Platform MPI 9.1.2) that will most
likely not work with **Terra's** interconnect fabric (Intel Omni-Path).
If parallel Abaqus usage is needed, the following options are available:

1.  Ideally, use Abaqus 2016 or 2017 on Terra. Both versions have been
    modified to support Terra's Omni-Path fabric for multi-node jobs.
2.  If Abaqus 6.14 is **needed** (eg. resuming from a previous 6.14
    simulation) on Terra, these jobs must be limited to a **single
    node** (at most 28 cores). In this case, do not use the
    *mp\_mode=mpi* option.
3.  If Abaqus 6.14 is **needed** with multiple nodes, these jobs most
    likely must be run on Ada instead.

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use
non-interactive batch jobs for resource-intensive and/or multiple-core
processing. Users are requested to be
<font color=teal>**responsible**</font> and <font color=teal>**courteous
to other users**</font> when using software on the login nodes.

The most important processing limits here are:  
\* **ONE HOUR** of **PROCESSING TIME** per login session.

  - **EIGHT CORES** per login session on the same node or (cumulatively)
    across all login nodes.

<font color=red size=3>**Anyone found violating the processing limits
will have their processes killed without warning. Repeated violation of
these limits will result in account suspension.**</font>  
<font color=teal>**Note:** Your login session will disconnect after
**one hour** of inactivity.</font>

## Usage on the Compute Nodes

Non-interactive batch jobs on the compute nodes allows for
resource-demanding processing. Non-interactive jobs have higher limits
on the number of cores, amount of memory, and runtime length.

For instructions on how to create and submit a batch job, please see the
appropriate wiki page for each respective cluster:

  - Terra: [ About Terra Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Grace: [ About Grace Batch Processing](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink")

### Terra Example
A **single-core** example with a user subroutine: (Last updated March 24, 2017)

```php
#!/bin/bash

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=AbaqusJob    # Sets the job name to AbaqusJob
#SBATCH --time=2:00:00          # Sets the runtime limit to 2 hr
#SBATCH --ntasks=1              # Requests 1 core
#SBATCH --ntasks-per-node=1     # Requests 1 core per node (1 node)
#SBATCH --mem=5G                # Requests 5GB of memory per node
#SBATCH --output=AbaqusJob.o%J  # Sends stdout and stderr to AbaqusJob.o[jobID]

## Load the module
module purge
module load ABAQUS/2017

## Launch Abaqus with proper parameters 
abaqus memory="5GB" cpus=1 job=jobname input=inputfile.inp user=filename.for
```


A **multi-core (10 core), single-node example**, with no user subroutine: **(Last updated June 14, 2017)**

```php
#!/bin/bash
##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
#SBATCH --export=NONE
#SBATCH --get-user-env=L

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=AbaqusJob    # Sets the job name to AbaqusJob
#SBATCH --time=2:00:00          # Sets the runtime limit to 2 hr
#SBATCH --ntasks=10             # Requests 10 cores
#SBATCH --ntasks-per-node=10    # Requests 10 cores per node (1 node)
#SBATCH --mem=50G               # Requests 50GB of memory per node
#SBATCH --output=AbaqusJob.o%J  # Sends stdout and stderr to AbaqusJob.o[jobID]

## Load the module
module purge
module load ABAQUS/2017

# setup host list for ABAQUS
slurm_setup_abaqus.sh
 
## Launch Abaqus with proper parameters 
abaqus memory="50GB" cpus=$SLURM_NTASKS job=jobname input=inputfile.inp 
```

A **multi-core (56 core), multi-node** example, with no user subroutine: **(Last updated June 14, 2017)**

```php
#!/bin/bash
##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
#SBATCH --export=NONE
#SBATCH --get-user-env=L

##NECESSARY JOB SPECIFICATIONS
#SBATCH --job-name=AbaqusJob    # Sets the job name to AbaqusJob
#SBATCH --time=2:00:00          # Sets the runtime limit to 2 hr
#SBATCH --ntasks=56             # Requests 56 cores
#SBATCH --ntasks-per-node=28    # Requests 28 cores per node (1 node)
#SBATCH --mem=50G               # Requests 50GB of memory per node
#SBATCH --output=AbaqusJob.o%J  # Sends stdout and stderr to AbaqusJob.o[jobID]

## Load the module
module purge
module load ABAQUS/2017

# setup host list for ABAQUS
slurm_setup_abaqus.sh
 
## Launch Abaqus with proper parameters 
abaqus memory="50GB" cpus=$SLURM_NTASKS job=jobname input=inputfile.inp mp_mode=mpi 
```

To submit the batch job run: (where jobscript is an ASCII English Text file that looks like one of the above examples)

```php
[ NetID@terra ~]$ sbatch jobscript
```

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.

### Running the ABAQUS GUI

TAMU OnDemand:

  - **Step 1:** Go to <https://portal.hprc.tamu.edu/> and select a
    cluster.  
  - **Step 2:** At the top of page, select 'Interactive Apps' and choose
    Abaqus/CAE.  
  - **Step 3:** Fill in the appropriate job parameters and select
    'Launch' to run the GUI.

Using VNC Script:  
While in a VNC job, use **abaqus cae** (with vglrun) to start the ABAQUS
GUI.

`[NetID@gpu ~]$ `**`vglrun   abaqus   cae`**

### Running the ABAQUS GUI on a login node

GUI use via a login node requires X11 forwarding to be enabled.

  -   - You can launch the GUI of certain applications from the login
        nodes. Keep in mind the Acceptable Use Policy while running on
        the login nodes. These limitations include:
          - **ONE HOUR** of PROCESSING TIME per login session.
          - **EIGHT CORES** per login session on the same node or
            (cumulatively) across all login nodes
      - A detailed guide for launching GUI's from the Login nodes can be
        found for each OS here:
        [Linux](/kb3/Helpful-Pages/Access/HPRC@Access/#access-from-linuxunix/)
        [MacOSX](/kb3/Helpful-Pages/Access/HPRC@Access/#access-from-macosX/)
        [Windows](/kb3/Helpful-Pages/Access/HPRC@Access/#access-from-windows/)

## Frequently Asked Questions

<span style="font-size:140%;">**Q: What versions of ABAQUS are available
and which should I use?**</span>  
**A:** You can see which versions of ABAQUS we have available by using
the **module spider** command as shown [
above](/kb3/Software/ABAQUS/SW@ABAQUS/#loading-the-module "wikilink"). If you do not need to
use a specific version of ABAQUS, we generally recommend that you use
the newest version that we provide. Remember that it is always
recommended to load a specific version of a module instead of the
default version. This is because default versions will change which
might cause problems in the future. It is always best to know exactly
which module you are using.

<span style="font-size:140%;">**Q: I am having a hard time setting up
batch job to run with Abaqus 6.14 version on Terra. What am I
missing?**</span>  
**A:** Abaqus 6.14 uses a MPI library (IBM Platform MPI 9.1.2) most
likely will not work with Terra's interconnect fabric (Intel Omni-Path).
Your options are:

  - **Option 1:** Ideally, use Abaqus 2016 or 2017 on Terra. Both
    versions have been modified to support Terra's Omni-Path fabric for
    multi-node jobs.

<!-- end list -->

  - **Option 2:** If you need to use Abaqus 6.14 (eg. resuming from a
    previous 6.14 simulation) on Terra, you will need to limit your job
    to a single node (at most 28 cores). In this case, do not use the
    mp\_mode=mpi option.

<!-- end list -->

  - **Option 3:** If you need to use Abaqus 6.14 with multiple nodes and
    will be resuming a previous 6.14 simulation, you will probably need
    to use the Ada cluster instead.

<span style="font-size:140%;">**Q: How do I open the ABAQUS
GUI?**</span>  
**A:** Using the ABAQUS GUI (or almost any GUI on our clusters) for
anything more than light editing requires the use of a VNC job. For
information on how to use a VNC job, please see our [ Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/ "wikilink") page.  

  - **Step 1:** Go to <https://portal.hprc.tamu.edu/> and select a
    cluster.  

<!-- end list -->

  - **Step 2:** At the top of page, select 'Interactive Apps' and choose
    ABAQUS/CAE.  

<!-- end list -->

  - **Step 3:** Fill in the appropriate job parameters and select
    'Launch' to run the GUI.

<font color=teal>**Note:** We always recommend that you do not submit
jobs with the ABAQUS GUI unless they take only seconds to run. Using the
GUI to submit jobs can cause a lot of issues and often takes much longer
than running a job non-interactively. </font>

<span style="font-size:140%;">**Q: What is the difference between an
interactive and a non-interactive job?**</span>  
**A:** An interactive job is one which is done in the GUI with
interaction from the user (even if only to start the job). A
non-interactive job is a job that the user gives to the cluster, most
often with a job file, which is then scheduled and run by the batch
system without the GUI or any further interaction from the user. A
non-interactive job often runs faster while using less resources and can
more easily be customized to meet the user's needs. A non-interactive
job uses the ABAQUS solver and creates exactly the same files as it
would if the GUI were used. You will also still be able to view the
results of the analysis as though the job were run with the GUI.

<span style="font-size:140%;">**Q: How do I submit a non-interactive
job?**</span>  
**A:** You will need a batch job file and your ABAQUS input file (.inp)
in order to submit a job. Examples of ABAQUS job files are given [
above](/kb3/Software/ABAQUS/SW@ABAQUS/#usage-on-the-compute-nodes "wikilink"). Please use
these only as guidelines, you will need to customize some requirements
to meet your needs.

  - **Step 1:** Generate the ABAQUS input file (.inp). This can be done
    in the GUI by first creating a job and then, in the top toolbar,
    going to **Job-\>Write Input-\>JobName**.
  - **Step 2:** Create a batch job file with the appropriate parameters.
  - **Step 3:** Submit the job

Use **bsub** on Ada:

`[NetID@ada1 ~]$ `**`bsub   <   `*`jobscript`***

Use **sbatch** on Terra:

`[NetID@terra1 ~]$ `**`sbatch   `*`jobscript`***

<span style="font-size:140%;">**Q: How much memory do I need?**</span>  
**A:** ABAQUS has a datacheck feature which will estimate how much
memory is needed to complete a certain job.

  - **Step 1:** Load the ABAQUS module.
  - **Step 2:** Run the datacheck command with the proper parameters. A
    data file (.dat) will be created.

`[NetID@cluster ~]$ `**`abaqus   datacheck   job=`*`jobname`***

  - **Step 3:** Look in the (.dat) file, there will be a section titled
    "MEMORY ESTIMATE" as shown below. The value labled "MEMORY TO
    MINIMIZE I/O" is the total amount of memory that your job will need.
    This is only an estimate and it is recommended to request at least
    slightly over the value found here.

```php
                M E M O R Y   E S T I M A T E
   
   PROCESS      FLOATING PT       MINIMUM MEMORY        MEMORY TO
                OPERATIONS           REQUIRED          MINIMIZE I/O
               PER ITERATION         (MBYTES)           (MBYTES)
   
       1          4.60E+6             10336              75311
```

<span style="font-size:140%;">**Q: How do I set the memory?**</span>  
**A:** There are two main ways that you can set the memory for ABAQUS.

  - **Setting the memory for an ABAQUS job. (Recommended for use with
    ALL non interactive jobs)**
      - To use more than the default memory in an ABAQUS job, add the
        memory parameter to your ABAQUS launch command in your batch job
        file. Remember, this is TOTAL memory, not memory per core.

**`abaqus   memory="`*`5000mb`*`"   job=`*`jobname`*` 
 input=`*`inputfile`***

  - **Setting the memory in an ABAQUS environment file. (Recommended for
    use with the GUI)**
      - In order to use more memory with the ABAQUS GUI, you will need
        to create an ABAQUS environment file (.env) which can be placed
        in either your home directory or current working directory.
      - **Step 1:** Create an ABAQUS environment file titled
        **abaqus\_v6.env** in your $HOME directory or the current
        working directory (or both).
      - **Step 2:** Add an entry to the environment file for memory with
        the memory parameter. Remember this is TOTAL memory, not memory
        per core.

**`memory="`*`5000mb`*`"`**

**Note:** ABAQUS checks for environment settings in three places. In
order, these are: the installation directory, a user's HOME directory,
and the current working directory. The settings that take precedence are
the LAST settings that ABAQUS checks. For example: If you have an
environment file in your home directory AND the current working
directory, the settings specified in the current working directory are
the ones that will be used. Any settings specified in an ABAQUS launch
command will take precedence over all environment file settings. **If no
memory is specified, the default value is 2GB.**

<span style="font-size:140%;">**Q: How many cores should I
use?**</span>  
**A:** ABAQUS is a software that is not the best when it comes to
parallelization. Unless you have written your code specifically to be
parallelized, ABAQUS generally will not parallelize well. It is possible
that you could experience some speed up from running your job on
multiple cores, and it is worth trying if your code is thread-safe.
However, if you are running a small job (which takes less than 2 hours
to complete), it is probably not worth the trouble of submitting on
multiple cores. If you have a job that will run for longer, you might
see a significant difference when using multiple cores. In general, for
smaller jobs, use fewer cores, and for larger jobs, use more cores.  
<font color=teal>**Note:** Do not try to run your job on multiple cores
if ANY part of your code is not thread safe. </font>

<span style="font-size:140%;">**Q: How long will my job take?**</span>  
If you are using a single core, in general, you can expect that an
ABAQUS job on Ada will take approximately the same time as it would on a
regular workstation. As stated above, ABAQUS generally does not
parallelize well. If you are using multiple cores, you might experience
some speed up, but it is hard to say how much as it depends largely on
your job and code.

<span style="font-size:140%;">**Q: How do I use ABAQUS to do**</span>  
**A:** Although we have some experience with running ABAQUS, we are, for
the most part, NOT ABAQUS experts. We can only provide minimal help when
it comes to using the software. If you have a problem with the software
not behaving how you expect it to, please refer to the ABAQUS
documentation linked [ above](/kb3/Software/ABAQUS/SW@ABAQUS/#documentation "wikilink").
Please feel free to contact us with your questions, but keep in mind
that we are NOT ABAQUS experts.
