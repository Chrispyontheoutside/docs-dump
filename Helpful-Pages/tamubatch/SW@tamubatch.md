# tamubatch

**tamubatch** is an automatic batch job submission script on Terra and
Grace that allows you to submit batch job files without batch
parameters. tamubatch takes a job file of executable commands and
directly adds parameters to the job file so the user does not have to
enter parameters every time. The user can specify specific batch
commands with the use of flags or they may use tamubatch's default batch
parameters.

### Synopsis

    [ NetID@ ~]$ tamubatch -help
    
    OPTIONS:
    
     SUBMISSION FLAGS:
    
      --walltime | -W <0:00>
            Sets the walltime for the current job in format 0:00.
        Default is 30 minutes
    
      --GPU | -gpu
        selects the gpu node to run the current job.
    
      --cores | -n <n>
            Sets the total number of cores for the current job.
        Default is one Core
    
      --cores-per-node | -R <n>
            Sets the number of cores per compute node.
        Default is the number of cores requested from the --cores flag (if specified) with a 
            maximum of 48 cores per node on Grace and 28 cores per node on Terra.
    
      --total-memory | -M <n>MB/G
            Sets the overall memory limit for the current job. Must specify MB or G
        Default is <4000MB on grace, 2000MB on terra> * Number of cores.
    
      --project-account | -P <Account Number>
            Sets the account to charge for the current job.
    
      --extras | -x "<all other LSF/SLURM flags>"
            Extra batch submission features for Users.
    
    
     ALL OTHER FLAGS:
    
      --command | -command "<bash commands>"
            Intended for Rapid prototyping
    
      --download | -download
            Generates script for download. Will not submit a job if flag is called. 
    
      --help | -h | -help
             Shows this message and exits.

### batch file

The batch file is a regular text file with the commands needed to be
executed by the cluster. These commands can be linux commands, cluster
commands, etc. Below is an example of commands that could potentially be
found in batch job files.

    #my_job_file
    
    echo "Hello"
    ml
    ml purge
    cd /scratch/user/directory
    ./my_script

### Examples

The following are examples of calls to tamubatch.

**Example 1: default submission**

    [ NetID@ ~]$ tamubatch my_job_file 

In the above example, tamubatch will identify the job file
(my\_job\_file) and then submit the job to the cluster with default
parameters. The default parameters are 1 core and 1 core per node. On
Grace, the default amount of memory is 400MB (4G). On Terra, the default
amount of memory is 2000MB (2.0G).

**Example 2: job submission with flags**

    [ NetID@ ~]$ tamubatch my_job_file -W 1:00 -n 20 -R 20 -M 50G

In the above example, tamubatch will set the wall time to one hour, the
number of cores to 20, the number of cores per node to 20, and the total
amount of memory for the job as 50G. tamubatch will then submit the job
(my\_job\_file) directly to the cluster.

**Example 3: job submission with GPU node and extra batch parameters**

    [ NetID@ ~]$ tamubatch my_job_file -gpu -W 5:00 -n 40 -R 20 -M 80G -x "--mail-type=ALL --mail-user=netid@tamu.edu"

After setting the number of cores, the number of cores per node, and the
memory in the example above, tamubatch will select the gpu node to run
the current job (my\_job\_file). tamubatch will then include extra batch
parameters in the job submission. In this specific example, the user
will be alerted through email when their batch job starts to run and
when their batch job is complete.

**NOTE:** the -x flag is used to add any additional batch scheduler flag
on either Grace and Terra.

**Example 4: job submission with commands**

    [ NetID@ ~]$ tamubatch my_job_file -W 1:00 -n 20 -R 20 -M 50G -command "echo hello; cd /user/net-id/"

Tamubatch will insert the same batch parameters as Example 2. Tamubatch
will then add the commands entered using the command flag to the end of
the batch job file (my\_job\_file). It will then submit the job to the
clusters.

A visual representation can be found in [this
video](https://www.youtube.com/watch?v=sP7GnQNvMVo) on our YouTube
channel.
