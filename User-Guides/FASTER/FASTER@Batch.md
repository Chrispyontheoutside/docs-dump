# FASTER Batch Processing: Slurm


## Introduction

The batch system is a load distribution implementation that ensures
convenient and fair use of a shared resource. Submitting jobs to a batch
system allows a user to reserve specific resources with minimal
interference to other users. All users are required to submit
resource-intensive processing to the compute nodes through the batch
system - <font color=red> attempting to circumvent the batch system is
not allowed.</font>

On FASTER, **Slurm** is the batch system that provides job management.
Jobs written in other batch system formats must be translated to Slurm
in order to be used on FASTER. The [ Batch Translation
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
directive*. For each batch system, this directive is different. On
FASTER (Slurm) this directive is **\#SBATCH**.  
<font color=teal> For every line of resource specifications, this
directive **must** be the first text of the line, and **all
specifications must come before any executable lines**.</font> An
example of a resource specification is given below:

`#SBATCH --jobname=MyExample  #Set the job name to "MyExample"`

Note: Comments in a job file also begin with a **\#** but Slurm
recognizes **\#SBATCH** as a directive.  
A list of the most commonly used and important options for these job
files are given in the following section of this wiki. Full job file
examples are given [ below](/kb3/User-Guides/FASTER/FASTER@Batch/#job-file-examples "wikilink").

### Basic Job Specifications

Several of the most important options are described below. These basic
options are typically all that is needed to run a job on FASTER.


**Basic FASTER (Slurm) Job Specifications**

| Specification          | Option                      | Example               | Example-Purpose                               |
| ---------------------- | --------------------------- | --------------------- | --------------------------------------------- |
| Wall Clock Limit       | \--time=\[hh:mm:ss\]        | \--time=05:00:00      | Set wall clock limit to 5 hours 00 min        |
| Job Name               | \--job-name=\[SomeText\]    | \--job-name=mpiJob    | Set the job name to "mpiJob"                  |
| Total Task/Core Count  | \--ntasks=\[\#\]            | \--ntasks=96          | Request 96 tasks/cores total                  |
| Tasks per Node I       | \--ntasks-per-node=\#       | \--ntasks-per-node=48 | Request exactly (or max) of 48 tasks per node |
| Memory Per Node        | \--mem=value\[K|M|G|T\]     | \--mem=360G           | Request 360 GB per node                       |
| Combined stdout/stderr | \--output=\[OutputName\].%j | \--output=mpiOut.%j   | Collect stdout/err in mpiOut.\[JobID\]        |



<font color=teal> It should be noted that Slurm divides processing
resources as such: Nodes -\> Cores/CPUs -\> Tasks

A user may change the number of tasks per core. For the purposes of this
guide, each core will be associated with exactly a single task. </font>


||Additional FASTER (Slurm) Job <br>**<font color=red>Warning</font>**: these options are NOT COMPATIBLE with OpenMPI ||
| ------------ | :----: | ----------------------------------- |
| Reset Env I  | \--export=NONE    | Do not propagate environment to job |
| Reset Env II | \--get-user-env=L | Replicate the login environment     |



Example batch file template for an MPI job. Notice that the Reset Env
options have been omitted, so this example can work with OpenMPI.

 
    #!/bin/bash 
    #                                                    
    ##NECESSARY JOB SPECIFICATIONS                                  
    #SBATCH --job-name=mpiJob                                      
    #SBATCH --time=5:00                                            
    #SBATCH --ntasks=96                                             
    #SBATCH --ntasks-per-node=48                                    
    #SBATCH --mem=360G                                             
    #SBATCH --output=mpiOut.%j                                     

    ## YOUR COMMANDS BELOW    
`  `

### Optional Job Specifications

A variety of optional specifications are available to customize your
job. The table below lists the specifications which are most useful for
users of FASTER.


**Optional FASTER/Slurm Job Specifications**

| Specification             | Option                         | Example                        | Example-Purpose                           |
| ------------------------- | ------------------------------ | ------------------------------ | ----------------------------------------- |
| Set Allocation            | \--account=\#\#\#\#\#\#        | \--account=274839              | Set allocation to charge to 274839        |
| Email Notification I      | \--mail-type=\[type\]          | \--mail-type=ALL               | Send email on all events                  |
| Email Notification II     | \--mail-user=\[address\]       | \--mail-user=howdy@tamu.edu    | Send emails to howdy@tamu.edu             |
| Specify Queue             | \--partition=\[queue\]         | \--partition=gpu               | Request only nodes in gpu subset          |
| Specify General Resource  | \--gres=\[resource\]:\[count\] | \--gres=gpu:1                  | Request one GPU per node                  |
| Specify A100 GPU Resource | \--gres=gpu:\[a100\]:\[count\] | \--gres=gpu:a100:1             | Request one a100 GPU per node             |
| Specify T4 GPU Resource   | \--gres=gpu:t4:\[count\]       | \--gres=gpu:t4:4               | Request four T4 GPUs per node             |
| Submit Test Job           | \--test-only                   |                                | Submit test job for Slurm validation      |
| Request Temp Disk         | \--tmp=M                       | \--tmp=10240                   | Request at least 10 GB in temp disk space |
| Request License           | \--licenses=\[LicenseLoc\]     | \--licenses=nastran@slurmdb:12 |                                           |



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
<caption><strong>Alternative Memory/Core/Node Specifications</strong></caption>
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
settings that most FASTER users do not need. These options are beyond
the scope of this guide.

If you wish to explore the advanced job options, see the [ Advanced
Documentation](/kb3/User-Guides/FASTER/FASTER@Batch/#advanced-documentation "wikilink").

### Environment Variables

All the nodes enlisted for the execution of a job carry most of the
environment variables the login process created: **HOME, SCRATCH, PWD,
PATH, USER,** etc. In addition, Slurm defines new ones in the
environment of an executing job. Below is a list of most commonly used
environment variables.

**Basic Slurm Environment Variables**

| Variable            | Usage                  | Description            |
| ------------------- | ---------------------- | ---------------------- |
| Job ID              | $SLURM\_JOBID          | Batch job ID assigned by Slurm.|
| Job Name            | $SLURM\_JOB\_NAME      | The name of the Job.|
| Queue               | $SLURM\_JOB\_PARTITION | The name of the queue the job is dispatched from.|
| Submit Directory    | $SLURM\_SUBMIT\_DIR    | The directory the job was submitted from.|
| Temporary Directory | $TMPDIR                | This is a directory assigned locally on the compute node for the job located at **/work/job.$SLURM\_JOBID**. Use of **$TMPDIR** is recommended for jobs that use many small temporary files. |


**Note:** To see all relevant Slurm environment variables for a job, add
the following line to the **executable section** of a job file and
submit that job. All the variables will be printed in the output file.

`env | grep SLURM`

### Clarification on Memory, Core, and Node Specifications

Memory Specifications are <font color=teal>IMPORTANT</font>.  
For examples on calculating memory, core, and/or node specifications on
FASTER: [ Specification
Clarification](/kb3/User-Guides/FASTER/FASTER@Batch/#clarification-on-memory-core-and-node-specifications/ "wikilink").

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
    ml intel/2020b   # Load the intel/2020b module
    ml               # List all currently loaded modules
      
    ./myProgram.o    # Run "myProgram.o"

For information on the module system or specific software, visit our [
Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page and our [ Software](SW "wikilink")
page.

## Job Submission

Once you have your job file ready, it is time to submit your job. You
can submit your job to slurm with the following command:

`[NetID@FASTER1 ~]$ `**`sbatch   `*`MyJob.slurm`***` `  
`Submitted batch job 3606`

## Job Monitoring and Control Commands

After a job has been submitted, you may want to check on its progress or
cancel it. Below is a list of the most used job monitoring and control
commands for jobs on FASTER.

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
    Cluster: FASTER
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

Several examples of Slurm job files for FASTER are listed below. For
translating Ada (LSF) job files, the [ Batch Job Translation
Guide](/kb3/Helpful-Pages/Batch-Translation/HPRC@Batch_Translation/ "wikilink") provides some reference.

<font color=purple>NOTE: Job examples are NOT lists of commands, but are
a template of the contents of a job file. These examples should be
pasted into a text editor and submitted as a job to be tested, not
entered as commands line by line. </font>

There are several optional parameters available for jobs on FASTER. In
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
    #SBATCH --ntasks-per-node=64         #Request 64 tasks/cores per node
    #SBATCH --mem=248M                   #Request 248G (248GB) per node
    #SBATCH --output=Example_SNMC_CPU.%j #Redirect stdout/err to file
    #SBATCH --partition=cpu              #Specify partition to submit job to 
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address 
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 3:**</span> A multi core,
multi node job  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=Example_MNMC_CPU  #Set the job name to Example_MNMC_CPU
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr 30min
    #SBATCH --nodes=2                    #Request 2 nodes
    #SBATCH --ntasks-per-node=64         #Request 64 tasks/cores per node
    #SBATCH --mem=248G                   #Request 248G (248GB) per node
    #SBATCH --output=Example_MNMC_CPU.%j #Redirect stdout/err to file
    #SBATCH --partition=cpu              #Specify partition to submit job to
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456            #Set billing account to 123456
    ##SBATCH --mail-type=ALL             #Send email on all job events
    ##SBATCH --mail-user=email_address   #Send all emails to email_address
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 4:**</span> A serial GPU job
(single node, single core)  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=Example_SNSC_GPU  #Set the job name to Example_SNSC_GPU
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr 30min
    #SBATCH --ntasks=1                   #Request 1 task
    #SBATCH --mem=248G                   #Request 248G (248GB) per node
    #SBATCH --output=Example_SNSC_GPU.%j #Redirect stdout/err to file
    #SBATCH --partition=gpu              #Specify partition to submit job to
    #SBATCH --gres=gpu:a100:1            #Specify GPU(s) per node, 1 A100 GPU
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456            
    #Set billing account to 123456
    ##SBATCH --mail-type=ALL             #Send email on all job events
    ##SBATCH --mail-user=email_address   #Send all emails to email_address
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 5:**</span> A serial GPU job
(single node, multiple core) 

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=Example_SNMC_GPU  #Set the job name to Example_SNMC_GPU
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr 30min
    #SBATCH --nodes=1                    #Request 1 nodes
    #SBATCH --ntasks-per-node=32         #Request 32 tasks/cores per node
    #SBATCH --mem=248G                   #Request 248G (248GB) per node
    #SBATCH --output=Example_SNMC_GPU.%j #Redirect stdout/err to file
    #SBATCH --partition=gpu              #Specify partition to submit job to
    #SBATCH --gres=gpu:a100:10           #Specify GPU(s) per node, 10 a100 GPU
      
    ##OPTIONAL JOB SPECIFICATIONS 
    ##SBATCH --account=123456            #Set billing account to 123456
    ##SBATCH --mail-type=ALL             #Send email on all job events
    ##SBATCH --mail-user=email_address   #Send all emails to email_address
      
    #First Executable Line

<span style="font-size:120%;">**Example Job 6:**</span> A parallel GPU
job (multiple node, multiple core)  

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS`  
    #SBATCH --job-name=Example_MNMC_GPU  #Set the job name to Example_MNMC_GPU
    #SBATCH --time=01:30:00              #Set the wall clock limit to 1hr 30min
    #SBATCH --nodes=2                    #Request 2 nodes
    #SBATCH --ntasks-per-node=32         #Request 32 tasks/cores per node
    #SBATCH --mem=248G                   #Request 248G (248GB) per node
    #SBATCH --output=Example_MNMC_GPU.%j #Redirect stdout/err to file
    #SBATCH --partition=gpu              #Specify partition to submit job to
    #SBATCH --gres=gpu:a100:1            #Specify GPU(s) per node, 1 A100 gpu 
      
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456            #Set billing account to 123456
    ##SBATCH --mail-type=ALL             #Send email on all job events
    ##SBATCH --mail-user=email_address   #Send all emails to email_address
      
    #First Executable Line

See more specialized job files (if available) at the [ HPRC Software
page](/kb3/Software/SW/ "wikilink")

## Batch Queues

Upon job submission, **Slurm** sends your jobs to appropriate batch
queues. These are (software) service stations configured to control the
scheduling and dispatch of jobs that have arrived in them. Batch queues
are characterized by all sorts of parameters. Some of the most important
are:

1.  The total number of jobs that can be concurrently running (number of
    run slots)
2.  The wall-clock time limit per job
3.  The type and number of nodes it can dispatch jobs to

These settings control whether a job will remain idle in the queue or be
dispatched quickly for execution.

<font color=teal>The current queue structure is: (**updated on January
11, 2021**). </font>

| Queue Name  | Max Nodes per Job (assoc's cores)\* | Max GPUs | Max Duration | Max Jobs in Queue\* | Charge Rate (per node-hour)      |
| ----------- | ----------------------------------- | -------- | ------------ | ------------------- | -------------------------------- |
| development | 1 nodes (64 cores)\*                | 10       | 1 hr         | 1\*                 | 64 Service Unit (SU) + GPUs used |
| CPU         | 128 nodes (8,192 cores)\*           | 0        | 48 hrs       | 50\*                | 64 Service Unit (SU)             |
| GPU         | 128 nodes (8,192 cores)\*           | 10       | 48 hrs       | 50\*                | 64 Service Unit (SU) + GPUs used |

### Checking queue usage

The following command can be used to get information on queues and their
nodes.

    [NetID@FASTER1 ~]$ sinfo

Example output: 

    PARTITION        AVAIL  TIMELIMIT    JOB_SIZE    NODES(A/I/O/T)   CPUS(A/I/O/T)  
    short*           up     2:00:00      1-32        32/763/5/800     1496/36664/240/38400   

Note: A/I/O/T stands for Active, Idle, Offline, and Total

### Checking node usage

The following command can be used to generate a list of nodes and their
corresponding information, including their CPU usage.

    [NetID@FASTER1 ~]$ pestat

Example output: 

    Hostname       Partition     Node      Num_CPU    CPUload    Memsize    Freemem    Joblist
                                 State     Use/Tot               (MB)       (MB)       JobId User ...
    c001          short*         idle      0   48     0.01       368640     365067 

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
