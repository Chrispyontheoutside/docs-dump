# tamulauncher

**tamulauncher** provides a convenient way to run a large number of
serial or multithreaded commands without the need to submit individual
jobs or a Job array. tamulauncher takes as arguments a text file
containing all commands that need to be executed and tamulauncher will
execute the commands concurrently. The number of concurrently executed
commands depends on the batch requirements. When tamulauncher is run
interactively the number of concurrently executed commands is limited to
at most 8. tamulauncher is available on grace and terra. There is no
need to load any module. tamulauncher has been successfully tested to
execute over 100K commands.

*tamulauncher is preferred over Job Arrays to submit a large number of
individual jobs, especially when the run times of the commands are
relatively short. It allows for better utilization of the nodes, puts
less burden on the batch scheduler, and lessens interference with jobs
of other users on the same node.*

### Synopsis

    [ NetID@ ~]$ tamulauncher --help
       Usage: /sw/local/bin/tamulauncher [options] FILE
    
       This script will execute commands in FILE concurrently. 
    
       OPTIONS:
    
         --commands-pernode | -p <n> 
                Set the number of concurrent processes per node.
    
         --norestart
                Do not restart.
    
         --status <commands file>
                Prints number of finished commands and exits.  
    
         --list <commands file>
                Prints detailed list of all finished commands and exits.
    
         --remove-logs <commands file>
                Removes the log directory and exits
    
         --version | -v
                Prints version and exits.
    
         --help | -h | ?
                Shows this message and exits.

### Commands file

The commands file is a regular text file containing all the commands
that need to be executed. Every line contains one command. A command can
be a user-compiled program, a Linux command, a script (e.g. bash,
Python, Perl, etc), a software package, etc. Commands can also be
compounded using the Linux semi-colon operator. In general, any command
that will work when typed in a bash shell will work when executed using
tamulauncher. Below is an example of a commands file; it illustrates a
commands file can contain any combination of commands (although in
practice it's mostly a repetition of the same command with varying input
parameters). Many times a commands file can be generated automatically.

    ./prog1 125
    ./prog2 "aa" 3 
    mkdir testcase1 ; cd testcase1; ./myprog
    ./prog1 100
        :
        :
        :
    time ./prog3 
    python mypython.py
    ./prog1 141 ; ./prog4 > OUTPUT
    ./prog5 < myinput

### Dynamic release of resources

tamulauncher will automatically release resources whenever they become
idle. Resources will be released on per-node basis. This feature is
especially useful in cases where the majority of requested cores/nodes
are idle, taking up valuable resources, while only a few cores are
processing the last few commands.

**NOTE** You might see some slurm error messages such as "srun: error:
<NODE>: task 7: Killed". These messages can be safely ignored.

**NOTE:** This is an experimental feature we are still improving on. For
that reason, as well as well as some needed changes to calculation of
SUs, the number of SUs charged will not be adjusted at this time.
However, it will help to make the cluster less congested.

## Examples

The following sections show two simple examples how to use tamulauncher.
The first examples shows how to run serial commands and the second
example shows how to run multi-threaded (OpenMP) commands.

### Example 1: Running serial commands

    #!/bin/bash
    
    #SBATCH --export=NONE               
    #SBATCH --get-user-env=L             
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=demo-tamulauncher
    #SBATCH --output=demo-tamulauncher.%j
    #SBATCH --time=07:00:00            
    #SBATCH --ntasks=480                            
    #SBATCH --mem=4096M                  
          
    tamulauncher commands.in

In the above example, tamulauncher will extract the requirements
specified in the SLURM script and distribute all the commands over the
480 tasks.

### Example 2: Running multi-threaded (OpenMP) commands

The next example shows how to run a bunch of OpenMP executables, where
every command will use 4 threads

    #!/bin/bash
    
    #SBATCH --export=NONE               
    #SBATCH --get-user-env=L             
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=demo-tamulauncher
    #SBATCH --output=demo-tamulauncher.%j
    #SBATCH --time=07:00:00            
    #SBATCH --ntasks=100                          
    #SBATCH --cpus-per-task=4
    #SBATCH --mem=4096M                  
          
    
    export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
    tamulauncher commands.in

In the above example, tamulauncher will extract the requirements
specified in the SLURM script and distribute all the commands over the
100 tasks. The SLURM **--cpus-per-task** option will make sure 4 cores
are reserved for every task and every command can use up to 4 threads.

## Automatic Restart

tamulauncher keeps track of all commands that have been executed. When
you start a tamulauncher job it will check for a log (located in
directory *.tamulauncher-log*) from a previous run and if that is the
case, it will continue executing commands that did not finish during the
previous run. This is especially useful when a tamulauncher job was
killed because it ran out of wall time or there was a system problem. To
turn off the automatic restart option, use the *'norestart* flag in your
tamulauncher command, e.g.

`  tamulauncher --norestart commands.in`

Using this option tamulauncher will just wipe all the log files and it
will start as if it was a first run.

**NOTE:** tamulauncher keeps a log for every unique commands file. If
you make any changes to the commands file, tamulauncher will assume it's
a different commands file and will create a new log directory. This also
means multiple tamulauncher runs can be executed in the same directory.

## Monitoring runs

To see how many commands have been executed use the **--status** flag in
tamulauncher:

`  [ NetID@ ~]$ `**`tamulauncher   --status   `<command file>**

This will show a one-line summary with the number of commands executed
and the total number of commands for the tamulauncher run on
*<command file>*.

To see a full listing of all finished commands use the **--list** flag
in tamulauncher:

`  [ NetID@ ~]$ `**`tamulauncher   --list   `<command file>**

This will show a list of all commands that have finished executing,
including index in the commands file, total run-time time, and exit
status for the tamulauncher run on *<command file>*.

## Clearing the log

To clear the log for a particular tamulauncher run, use the
**--remove-logs** flag.

`  [ NetID@ ~]$ `**`tamulauncher   --remove-logs 
 `<command file>**

This will clear the logs for the latest tamulauncher run on commands
file <command file>. **NOTE:** don't clear the logs while tamulauncher
is still running on that particular <commands file>.
