# Terra Batch Processing: Slurm

## Introduction

The batch system is a load distribution implementation that ensures
convenient and fair use of a shared resource. Submitting jobs to a batch
system allows a user to reserve specific resources with minimal
interference to other users. All users are required to submit
resource-intensive processing to the compute nodes through the batch
system - <font color=red> attempting to circumvent the batch system is
not allowed.</font>

On Terra, **Slurm** is the batch system that provides job management.
Jobs written in other batch system formats must be translated to Slurm
in order to be used on Terra. The [ Batch Translation
Guide](/kb3/Helpful-Pages/Batch-Translation/HPRC@Batch_Translation/ "wikilink") offers some assistance for
translating between batch systems that TAMU HPRC has previously used.

## Building Job Files

While not the only method of submitted programs to be executed, job
files fulfill the needs of most users.

The general idea behind job files follows:

  - Make resource requests
  - Add your commands and/or scripting
  - Submit the job to the batch system

In a job file, resource specification options are preceded by a *script
directive*. For each batch system, this directive is different. On Terra
(Slurm) this directive is **\#SBATCH**.  
<font color=teal> For every line of resource specifications, this
directive **must** be the first text of the line, and **all
specifications must come before any executable lines**.</font> An
example of a resource specification is given below:

`#SBATCH --jobname=MyExample  #Set the job name to "MyExample"`

Note: Comments in a job file also begin with a **\#** but Slurm
recognizes **\#SBATCH** as a directive.  
A list of the most commonly used and important options for these job
files are given in the following section of this wiki. Full job file
examples are given [ below](/kb3/User-Guides/Terra/Terra@Batch/#job-file-examples "wikilink").

### Basic Job Specifications

Several of the most important options are described below. These basic
options are typically all that is needed to run a job on Terra.

| Specification          | Option                      | Example               | Example-Purpose                               |
| ---------------------- | --------------------------- | --------------------- | --------------------------------------------- |
| Reset Env I            | \--export=NONE              |                       | Do not propagate environment to job           |
| Reset Env II           | \--get-user-env=L           |                       | Replicate the login environment               |
| Wall Clock Limit       | \--time=\[hh:mm:ss\]        | \--time=05:00:00      | Set wall clock limit to 5 hour 0 min          |
| Job Name               | \--job-name=\[SomeText\]    | \--job-name=mpiJob    | Set the job name to "mpiJob"                  |
| Total Task/Core Count  | \--ntasks=\[\#\]            | \--ntasks=56          | Request 56 tasks/cores total                  |
| Tasks per Node I       | \--ntasks-per-node=\#       | \--ntasks-per-node=28 | Request exactly (or max) of 28 tasks per node |
| Memory Per Node        | \--mem=value\[K|M|G|T\]     | \--mem=32G            | Request 32 GB per node                        |
| Combined stdout/stderr | \--output=\[OutputName\].%j | \--output=mpiOut.%j   | Collect stdout/err in mpiOut.\[JobID\]        |

Basic Terra (Slurm) Job Specifications

<font color=teal> It should be noted that Slurm divides processing
resources as such: Nodes -\> Cores/CPUs -\> Tasks

A user may change the number of tasks per core. For the purposes of this
guide, each core will be associated with exactly a single task. </font>

![Note|link=](/kb3/assets/images/OOjs_UI_icon_lightbulb-yellow.png "Note|link=") **Note**
To submit batch scripts using non-Intel MPI toolchains, you must omit
the **Reset Env I** and **Reset Env II** parameters from your batch
script:

        #INCOMPATIBLE WITH OpenMPI/NON-INTEL MPI                        #COMPATIBLE WITH OpenMPI/NON-INTEL MPI
        #!/bin/bash                                                     
        ##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION                     ##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
        #SBATCH --export=NONE    #Do not propagate environment          ##SBATCH --export=NONE    #Do not propagate environment OMIT THIS
        #SBATCH --get-user-env=L #Replicate login environment           ##SBATCH --get-user-env=L #Replicate login environment  OMIT THIS
        
        ##NECESSARY JOB SPECIFICATIONS                                  ##NECESSARY JOB SPECIFICATIONS
        #SBATCH --job-name=jobname                                      #SBATCH --job-name=jobname
        #SBATCH --time=5:00                                             #SBATCH --time=5:00
        #SBATCH --ntasks=56                                             #SBATCH --ntasks=56
        #SBATCH --ntasks-per-node=28                                    #SBATCH --ntasks-per-node=28
        #SBATCH --mem=32G                                               #SBATCH --mem=32G
        #SBATCH --output=example.%j                                     #SBATCH --output=example.%j
        
        ## YOUR COMMANDS BELOW                                          ## YOUR COMMANDS BELOW

### Optional Job Specifications

A variety of optional specifications are available to customize your
job. The table below lists the specifications which are most useful for
users of Terra.

| Specification               | Option                         | Example                        | Example-Purpose                           |
| --------------------------- | ------------------------------ | ------------------------------ | ----------------------------------------- |
| Set Allocation              | \--account=\#\#\#\#\#\#        | \--account=274839              | Set allocation to charge to 274839        |
| Email Notification I        | \--mail-type=\[type\]          | \--mail-type=ALL               | Send email on all events                  |
| Email Notification II       | \--mail-user=\[address\]       | \--mail-user=howdy@tamu.edu    | Send emails to howdy@tamu.edu             |
| Specify Queue               | \--partition=\[queue\]         | \--partition=gpu               | Request only nodes in gpu subset          |
| Specify General Resource    | \--gres=\[resource\]:\[count\] | \--gres=gpu:1                  | Request one GPU per node                  |
| Specify a specific gpu type | \--gres=gpu:\[type\]:\[count\] | \--gres=gpu:v100:1             | Request v100 gpu: type=k80 or v100        |
| Submit Test Job             | \--test-only                   |                                | Submit test job for Slurm validation      |
| Request Temp Disk           | \--tmp=M                       | \--tmp=10240                   | Request at least 10 GB in temp disk space |
| Request License             | \--licenses=\[LicenseLoc\]     | \--licenses=nastran@slurmdb:12 |                                           |

Optional Terra/Slurm Job Specifications

### Alternative Specifications

The job options within the above sections specify resources with the
following method:

  - Cores and CPUs are equivalent
  - 1 Task per 1 CPU desired
  - **You specify:** desired number of **tasks** (equals number of CPUs)
  - **You specify:** desired number of **tasks per node** (equal or less
    than the 28 cores per compute node)
  - **You get:** total nodes equal to *\#ofCPUs/\#ofTasksPerNodes*
  - **You specify:** desired Memory per node

Slurm allows users to specify resources in units of Tasks, CPUs,
Sockets, and Nodes.

There are many overlapping settings and some settings may (quietly)
overwrite the defaults of other settings. A good understanding of Slurm
options is needed to correctly utilize these methods.

<table>
<caption>Alternative Memory/Core/Node Specifications</caption>
<thead>
<tr class="header">
<th><p>Specification</p></th>
<th><p>Option</p></th>
<th><p>Example</p></th>
<th><p>Example-Purpose</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Node Count</p></td>
<td><p>--nodes=[min[-max]]</p></td>
<td><p>--nodes=4</p></td>
<td><p>Spread all tasks/cores across 4 nodes</p></td>
</tr>
<tr class="even">
<td><p>CPUs per Task</p></td>
<td><p>--cpus-per-task=#</p></td>
<td><p>--cpus-per-task=4</p></td>
<td><p>Require 4 CPUs per task (default: 1)</p></td>
</tr>
<tr class="odd">
<td><p>Memory per CPU</p></td>
<td><p>--mem-per-cpu=MB</p></td>
<td><p>--mem-per-cpu=2000</p></td>
<td><p>Request 2000 MB per CPU<br />
<font color=purple>NOTE: If this parameter is less than 1024, SLURM will misinterpret it as 0</font> |- &lt;!--</p></td>
</tr>
<tr class="even">
<td><p>Memory per Node (All, Multi)</p></td>
<td><p>--mem=0</p></td>
<td></td>
<td><p>Request the least-max available memory for any node across all nodes |- YANG SAYS NO SOUP FOR YOU--&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Tasks per Node II</p></td>
<td><p>--tasks-per-node=#</p></td>
<td><p>--tasks-per-node=5</p></td>
<td><p>Equivalent to Tasks per Node I</p></td>
</tr>
<tr class="even">
<td><p>Tasks per Socket</p></td>
<td><p>--ntasks-per-socket=#</p></td>
<td><p>--ntasks-per-socket=6</p></td>
<td><p>Request max of 6 tasks per socket</p></td>
</tr>
<tr class="odd">
<td><p>Sockets per Node</p></td>
<td><p>--sockets-per-node=#</p></td>
<td><p>--sockets-per-node=2</p></td>
<td><p>Restrict to nodes with at least 2 sockets</p></td>
</tr>
</tbody>
</table>

If you want to make resource requests in an alternative format, you are
free to do so. <font color=teal>Our ability to support alternative
resource request formats may be limited.</font>

### Using Other Job Options

Slurm has facilities to make advanced resources requests and change
settings that most Terra users do not need. These options are beyond the
scope of this guide.

If you wish to explore the advanced job options, see the [ Advanced
Documentation](/kb3/User-Guides/Terra/Terra@Batch/#advanced-documentation "wikilink").

### Environment Variables

All the nodes enlisted for the execution of a job carry most of the
environment variables the login process created: **HOME, SCRATCH, PWD,
PATH, USER,** etc. In addition, Slurm defines new ones in the
environment of an executing job. Below is a list of most commonly used
environment variables.

| Variable            | Usage                  | Description                                                                                                                                                                                  |
| ------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Job ID              | $SLURM\_JOBID          | Batch job ID assigned by Slurm.                                                                                                                                                              |
| Job Name            | $SLURM\_JOB\_NAME      | The name of the Job.                                                                                                                                                                         |
| Queue               | $SLURM\_JOB\_PARTITION | The name of the queue the job is dispatched from.                                                                                                                                            |
| Submit Directory    | $SLURM\_SUBMIT\_DIR    | The directory the job was submitted from.                                                                                                                                                    |
| Temporary Directory | $TMPDIR                | This is a directory assigned locally on the compute node for the job located at **/work/job.$SLURM\_JOBID**. Use of **$TMPDIR** is recommended for jobs that use many small temporary files. |

Basic Slurm Environment Variables

**Note:** To see all relevant Slurm environment variables for a job, add
the following line to the **executable section** of a job file and
submit that job. All the variables will be printed in the output file.

`env | grep SLURM`

### Clarification on Memory, Core, and Node Specifications

Memory Specifications are <font color=teal>IMPORTANT</font>.  
For examples on calculating memory, core, and/or node specifications on
Terra: [ Specification
Clarification](/kb3/User-Guides/Terra/Terra@Batch/#clarification-on-memory-core-and-node-specifications/ "wikilink").

### Executable Commands

After the resource specification section of a job file comes the
executable section. This executable section contains all the necessary
UNIX, Linux, and program commands that will be run in the job.  
Some commands that may go in this section include, but are not limited
to:

  - Changing directories
  - Loading, unloading, and listing modules
  - Launching software

An example of a possible executable section is below:

    cd $SCRATCH      # Change current directory to /scratch/user/[netID]/
    ml purge         # Purge all modules
    ml intel/2016b   # Load the intel/2016b module
    ml               # List all currently loaded modules
      
    ./myProgram.o    # Run "myProgram.o"

For information on the module system or specific software, visit our [
Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page and our [ Software](/kb3/Software/SW/ "wikilink")
page.


### Usable Memory for Batch Jobs

While nodes on Terra have either 64GB or 128GB of RAM, some of this
memory is used to maintain the software and operating system of the
node. In most cases, excessive memory requests will be automatically
rejected by SLURM.

The table below contains information regarding the approximate limits of
Terra memory hardware and our suggestions on its use.

<table>
<caption>Memory Limits of Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>64GB Nodes</p></th>
<th><p>128GB Nodes</p></th>
<th><p>96GB KNL Nodes (68 core)</p></th>
<th><p>96GB KNL Nodes (72 core)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Node Count</p></td>
<td><p>256</p></td>
<td><p>48</p></td>
<td><p>8</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>Number of Cores</p></td>
<td><p>28 Cores (2 sockets x 14 core)</p></td>
<td><p>68 Cores</p></td>
<td><p>72 Cores</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory Limit<br />
Per Core</p></td>
<td><p>2048 MB<br />
2 GB</p></td>
<td><p>4096 MB<br />
4 GB</p></td>
<td><p>1300 MB<br />
1.25 GB</p></td>
<td><p>1236 MB<br />
1.20 GB</p></td>
</tr>
<tr class="even">
<td><p>Memory Limit<br />
Per Node</p></td>
<td><p>57344 MB<br />
56 GB</p></td>
<td><p>114688 MB<br />
112 GB</p></td>
<td><p>89000 MB<br />
84 GB</p></td>
<td><p>89000 MB<br />
84 GB</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

SLURM may queue your job for an excessive time (or indefinitely) if
waiting for some particular nodes with sufficient memory to become free.

### Recommended Settings for Large Jobs

For jobs larger than 1000 cores, the following settings are recommended
for reducing the MPI startup time for jobs on Terra:

    export I_MPI_SLURM_EXT=on
    export I_MPI_HYDRA_PMI_CONNECT=alltoall

## Job Submission

Once you have your job file ready, it is time to submit your job. You
can submit your job to slurm with the following command:

`[NetID@Terra1 ~]$ `**`sbatch   `*`MyJob.slurm`***` `  
`Submitted batch job 3606`

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/dQzBZJpoU64" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## Job Monitoring and Control Commands

After a job has been submitted, you may want to check on its progress or
cancel it. Below is a list of the most used job monitoring and control
commands for jobs on Terra.

<table>
<caption>Job Monitoring and Control Commands</caption>
<thead>
<tr class="header">
<th><p>Function</p></th>
<th><p>Command</p></th>
<th><p>Example</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Submit a job</p></td>
<td><p>sbatch [script_file]</p></td>
<td><p>sbatch FileName.job</p></td>
</tr>
<tr class="even">
<td><p>Cancel/Kill a job</p></td>
<td><p>scancel [job_id]</p></td>
<td><p>scancel 101204</p></td>
</tr>
<tr class="odd">
<td><p>Check status of a single job</p></td>
<td><p>squeue --job [job_id]</p></td>
<td><p>squeue --job 101204</p></td>
</tr>
<tr class="even">
<td><p>Check status of all<br />
jobs for a user</p></td>
<td><p>squeue -u [user_name]</p></td>
<td><p>squeue -u User1</p></td>
</tr>
<tr class="odd">
<td><p>Check CPU and memory efficiency for a job<br />
(Use only on finished jobs)</p></td>
<td><p>seff [job_id]</p></td>
<td><p>seff 101204</p></td>
</tr>
</tbody>
</table>

Here is an example of the seff command provides for a finished job:

    % seff 12345678
    Job ID: 12345678
    Cluster: Terra
    User/Group: username/groupname
    State: COMPLETED (exit code 0)
    Nodes: 16
    Cores per node: 28
    CPU Utilized: 1-17:05:54
    CPU Efficiency: 94.63% of 1-19:25:52 core-walltime
    Job Wall-clock time: 00:05:49
    Memory Utilized: 310.96 GB (estimated maximum)
    Memory Efficiency: 34.70% of 896.00 GB (56.00 GB/node)

## Job File Examples

Several examples of Slurm job files for Terra are listed below. For
translating Ada (LSF) job files, the [ Batch Job Translation
Guide](/kb3/Helpful-Pages/Batch-Translation/HPRC@Batch_Translation/ "wikilink") provides some reference.

<font color=purple>NOTE: Job examples are NOT lists of commands, but are
a template of the contents of a job file. These examples should be
pasted into a text editor and submitted as a job to be tested, not
entered as commands line by line. </font>

There are several optional parameters available for jobs on Terra. In
the examples below, they are commented out/ignored via \#\#. If you wish
to include these values as parameters for your jobs, please change it to
a singular \# and adjust the parameter value accordingly.

<span style="font-size:120%;">**Example Job 1:**</span> A serial job
(single core, single node)  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=JobExample1       #Set the job name to "JobExample1"
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=1                   #Request 1 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=Example1Out.%j      #Send stdout/err to "Example1Out.[jobID]"
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 2:**</span> A multi core,
single node job  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=JobExample2       #Set the job name to "JobExample2"
    #SBATCH --time=6:30:00               #Set the wall clock limit to 6hr and 30min
    #SBATCH --nodes=1                    #Request 1 node
    #SBATCH --ntasks-per-node=8          #Request 8 tasks/cores per node
    #SBATCH --mem=8G                     #Request 8GB per node 
    #SBATCH --output=Example2Out.%j      #Send stdout/err to "Example2Out.[jobID]" 
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address 
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 3:**</span> A multi core,
multi node job  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=JobExample3       #Set the job name to "JobExample3"
    #SBATCH --time=1-12:00:00            #Set the wall clock limit to 1 Day and 12hr
    #SBATCH --ntasks=8                   #Request 8 tasks
    #SBATCH --ntasks-per-node=2          #Request 2 tasks/cores per node
    #SBATCH --mem=4096M                  #Request 4096MB (4GB) per node 
    #SBATCH --output=Example3Out.%j      #Send stdout/err to "Example3Out.[jobID]"
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address 
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 4:**</span> A serial GPU
job  

    #!/bin/bash`

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=JobExample4       #Set the job name to "JobExample4"
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=1                   #Request 1 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=Example4Out.%j      #Send stdout/err to "Example4Out.[jobID]"
    #SBATCH --gres=gpu:1                 #Request 1 GPU per node cam be 1 or 2
    #SBATCH --partition=gpu              #Request the GPU partition/queue
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address 
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 5:**</span> A parallel GPU
job  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS`  
    #SBATCH --job-name=JobExample5       #Set the job name to "JobExample5"
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=28                   #Request 1 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=Example5Out.%j      #Send stdout/err to "Example5Out.[jobID]"
    #SBATCH --gres=gpu:2                 #Request 2 GPU per node can be 1 or 2
    #SBATCH --partition=gpu              #Request the GPU partition/queue
      
    ##OPTIONAL JOB SPECIFICATIONS`  
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 6:**</span> A serial KNL job
(single core, single node)  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS`  
    #SBATCH --job-name=JobExample6       #Set the job name to "JobExample6"
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=1                   #Request 1 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=Example6Out.%j      #Send stdout/err to "Example6Out.[jobID]"
      
    ##OPTIONAL JOB SPECIFICATIONS`  
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address
      
    #SBATCH --partition=knl               #Request the KNL nodes
      
    #First Executable Line

See more specialized job files (if available) at the [ HPRC Software
page](/kb3/Software/SW/ "wikilink")

## Queues

Upon job submission, [**Slurm**](https://slurm.schedmd.com/) sends your
jobs to appropriate batch queues. These are (software) service stations
configured to control the scheduling and dispatch of jobs that have
arrived in them. Batch queues are characterized by all sorts of
parameters. Some of the most important are:

1.  The total number of jobs that can be concurrently running (number of
    run slots)
2.  The wall-clock time limit per job
3.  The type and number of nodes it can dispatch jobs to

These settings control whether a job will remain idle in the queue or be
dispatched quickly for execution.

<font color=teal>The current queue structure is: (**updated on January
29, 2020**). </font>

<table>
<thead>
<tr class="header">
<th><p>Queue</p></th>
<th><p>Job Max Cores / Nodes</p></th>
<th><p>Job Max Walltime</p></th>
<th><p>Compute Node Types</p></th>
<th><p>Per-User Limits Across Queues</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>short</p></td>
<td><p>448 cores / 16 nodes</p></td>
<td><p>30 min / 2 hr</p></td>
<td><p>64 GB nodes (256)</p></td>
<td><p>1800 Cores per User</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>medium</p></td>
<td><p>1792 cores / 64 nodes</p></td>
<td><p>1 day</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>long</p></td>
<td><p>896 cores / 32 nodes</p></td>
<td><p>7 days</p></td>
<td><p>64 GB nodes (256)</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>xlong</p></td>
<td><p>448 cores / 16 nodes</p></td>
<td><p>21 days</p></td>
<td><p>64 GB nodes (256)</p></td>
<td><p>448 cores per User</p></td>
<td><p>For jobs needing to run longer than 7 days. <strong>Submit jobs to this partition with the --partition xlong option.</strong></p></td>
</tr>
<tr class="odd">
<td><p>gpu</p></td>
<td><p>1344 cores / 48 nodes</p></td>
<td><p>3 days</p></td>
<td><p>128 GB nodes with GPUs (48)</p></td>
<td></td>
<td><p>For jobs requiring a GPU or more than 64 GB of memory.</p></td>
</tr>
<tr class="even">
<td><p>vnc</p></td>
<td><p>28 cores / 1 node</p></td>
<td><p>12 hours</p></td>
<td><p>128 GB nodes with GPUs (48)</p></td>
<td></td>
<td><p>For jobs requiring remote visualization.</p></td>
</tr>
<tr class="odd">
<td><p>knl</p></td>
<td><p>68 cores / 8 nodes<br />
72 cores / 8 nodes</p></td>
<td><p>7 days</p></td>
<td><p>96 GB nodes with KNL processors (8)</p></td>
<td></td>
<td><p>For jobs requiring a KNL.</p></td>
</tr>
</tbody>
</table>

### Checking queue usage

The following command can be used to get information on queues and their
nodes.

    [NetID@terra1 ~]$ sinfo

Example output: 

    PARTITION        AVAIL  TIMELIMIT    JOB_SIZE    NODES(A/I/O/T)   CPUS(A/I/O/T)  
    short*           up     2:00:00      1-16        244/12/0/256     5333/1835/0/7168   

Note: A/I/O/T stands for Active, Idle, Offline, and Total

### Checking node usage

The following command can be used to generate a list of nodes and their
corresponding information, including their CPU usage.

    [NetID@terra1 ~]$ pestat

Example output: 

    Hostname       Partition      Node   Num_CPU   CPUload   Memsize  Freemem       Joblist                            
                                 State   Use/Tot                (MB)     (MB)    JobId User ...  
    knl-0101             knl    drain$         0        68     0.00*    88000             0   


### Checking bad nodes
The following command can be used to view a current list of bad nodes on the machine:

    [NetID@FASTER1 ~]$ bad_nodes.sh

The following output is just an example output and users should run 
bad_nodes.sh not see a current list.

#### Example output:

    % bad_nodes.sh 
    REASON                                                       USER             TIMESTAMP            STATE        NODELIST
    The system board OCP1 PG voltage is outside of range.        root             2022-07-11T14:38:07  drained      fc152
    FPGA preparation in progress                                 root             2022-07-12T15:57:01  drained*     fc[125-126]
    investigating memverge license issue                         francis          2022-08-09T14:15:05  drained      fc032
    investigating unknown memverge issue                         francis          2022-08-09T14:15:19  drained      fc033
    fabric 1 hardware failure                                    francis          2022-08-15T13:52:10  drained*     fc[001-006,008,039-040]


### Checkpointing

Checkpointing is the practice of creating a save state of a job so that,
if interrupted, it can begin again without starting completely over.
This technique is especially important for long jobs on the batch
systems, because each batch queue has a maximum walltime limit.

A checkpointed job file is particularly useful for the gpu queue, which
is limited to 2 days walltime due to its demand. There are many cases of
jobs that require the use of gpus and must run longer than two days,
such as training a machine learning algorithm.

Users can change their code to implement save states so that their code
may restart automatically when cut off by the wall time limit. There are
many different ways to checkpoint a job file depending on the software
used, but it is almost always done at the application level. It is up to
the user how frequently save states are made depending on what kind of
fault tolerance is needed for the job, but in the case of the batch
system, the exact time of the 'fault' is known. It's just the walltime
limit of the queue. In this case, only one checkpoint need be created,
right before the limit is reached. Many different resources are
available for checkpointing techniques. Some examples for common
software are listed below.

## Advanced Documentation

This guide only covers the most commonly used options and useful
commands.

For more information, check the man pages for individual commands or the
[Slurm Manual](https://slurm.schedmd.com/).


