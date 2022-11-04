# Comsol

## Description

COMSOL Multiphysics is a cross-platform finite element analysis, solver
and multiphysics simulation software. It allows conventional
physics-based user interfaces and coupled systems of partial
differential equations (PDEs). COMSOL provides an IDE and unified
workflow for electrical, mechanical, fluid, and chemical applications.
An API for Java and LiveLink for MATLAB may be used to control the
software externally, and the same API is also used via the Method
Editor.

Once a model is built in Comsol GUI, the next step is to compute the
model for a solution, which is often time-consuming. A job script must
be created to run the model in batch so that you can control wall time,
memory, and other cluster resources for your simulation. This tutorial
illustrates how to create Comsol LSF batch scripts on Ada.

All solvers in Comsol can run in parallel in one of three parallel
modes: shared memory mode, distributed mode, or hybrid mode. By default,
a Comsol solver runs in shared memory mode. This is the same as OpenMP
where the parallelism is limited by total number of CPU cores available
on one compute node in a cluster.

## Access

Comsol is restricted software that is only limited to users and groups
who have a license. You can choose one of the following to get access:

1.  Purchase your own license (If you choose this route, you can either
    ask us to host the license server or you can host the server by
    yourself.)
2.  Ask for permission to use the license server maintained by the
    school of engineering.

The contact person is:

` Mitch Wittneben`  
` 979-845-5235`  
` mwittneben@tamu.edu`

## A Complete Batch Job Example

**Note: xxx represents a Comsol version. You need to pick the version
you need to access.**

**Example 1a (Terra)**: Solving a model in shared memory mode using 28
cores on one Terra cluster node.

` #!/bin/bash`  
` #SBATCH --job-name=comsol          #Set the job name to "Comsol"`  
` #SBATCH --time=01:30:00            #Set the wall clock limit to 1hr and 30min`  
` #SBATCH --ntasks=28                #Request 28 tasks`  
` #SBATCH --ntasks-per-node=28       #Request 28 tasks/cores per node`  
` #SBATCH --mem=56G                  #Request 56 GB of memory per node`  
` #SBATCH --output=comsol.%j         #Send stdout/err to "comsol.[jobID]"`  
` ml Comsol/xxx `  
` `  
` comsol -np 28 batch -inputfile in.mph -outputfile out.mph`

Save the above example to a file and run "sbatch file" to submit this
job.

## Running Comsol in Different Parallel Mode

Assuming other things are the same as in Example 1, we will show
additional examples running in different parallel modes by changing the
number of cores and the Comsol command line parameters.

### Shared Memory Mode

**Example 2a (Terra)**: Solving a model in shared memory mode using 14
cores on one Terra cluster node. This is similar as Example 1b

` #!/bin/bash`  
` #SBATCH --job-name=comsol          #Set the job name to "Comsol"`  
` #SBATCH --time=01:30:00            #Set the wall clock limit to 1hr and 30min`  
` #SBATCH --ntasks=14                #Request 14 tasks`  
` #SBATCH --ntasks-per-node=14       #Request 14 tasks/cores per node`  
` #SBATCH --mem=28G                  #Request 28 GB of memory per node`  
` #SBATCH --output=comsol.%j         #Send stdout/err to "comsol.[jobID]"`  
` ml Comsol/xxx `  
  
` comsol -np 14 batch -inputfile in.mph -outputfile out.mph`

### Distributed Mode

Comsol solvers can also run in distributed mode by checking the
"distributed computing" checkbox of the solver when building the model.
In this mode, the solver runs on multiple nodes and uses MPI for
communication. Except PARDISO, all solvers support distributed mode.
However, PARDISO also has a check box for distributed computing. If
selected, the actual solver used is MUMPS.

**Example 3a (Terra)**: Solving a model in distributed mode on two Terra
cluster nodes with a total of 56 cores

` #!/bin/bash`  
` #SBATCH --job-name=comsol          #Set the job name to "Comsol"`  
` #SBATCH --time=01:30:00            #Set the wall clock limit to 1hr and 30min`  
` #SBATCH --ntasks=56                #Request 56 tasks`  
` #SBATCH --ntasks-per-node=28       #Request 28 tasks/cores per node`  
` #SBATCH --mem=56G                  #Request 56 GB of memory per node`  
` #SBATCH --output=comsol.%j         #Send stdout/err to "comsol.[jobID]"`  
` ml Comsol/xxx `  
` `  
` comsol -simplecluster -inputfile input.mph -outputfile output.mph`

### Hybrid Mode

Either mode has its pros and cons. Shared mode utilizes CPU cores better
than distributed mode but can only run on one cluster node, while
distributed mode can utilize more than one physical cluster node. It is
usually best to run a solver in a way to take advantage of both modes.
This can be done easily at the command line through fine tuning of the
options -nn, -nnhost, -np.

### Parametric Sweep

Comsol models configured with parametric sweep can also benefit from
parallel computing in different ways. A model configured with parametric
sweep needs to run under a range of parameters or combinations of
parameters, and each set of parameters can be calculated independently.
Once a model with parametric sweep node created in the Comsol GUI, it
must also be configured with cluster sweep to distribute the parameters
to be processed in parallel.

## Common problems

1\. Disk quota exceeded in home directory

By default, COMSOL stores all temporary files in your home directory.
For large models, you are likely to get "Disk quota exceeded" error due
to huge amount of temporary files dumped into your home directory. To
resolve this issue, you need to redirect temporary files to your scratch
directory.

`  comsol -tmpdir /scratch/user/username/cosmol/tmp -recoverydir /scratch/user/username/comsol/recovery -np 20 -inputfile input.mph -outputfile outpu.mph`

2\. Out of Memory

If you receive the "Out of Memory" error, most likely the Java heap has
an inadequate size. The default Java heap size for Comsol is 2G. You can
change the value by following three steps:

-   **1) load the comsol module**

`ml Comsol/version`

-   **2) copy the Comsol setup file to your home directory**

If you are running one core Comsol job, copy comsolbatch.ini

`cp $EBROOTCOMSOL/bin/glnxa64/comsolbatch.ini $HOME/comsol.ini`

If you are running cluster Comsol job, copy comsolclusterbatch.ini

`cp $EBROOTCOMSOL/bin/glnxa64/comsolclusterbatch.ini $HOME/comsol.ini`

-   **3) edit the local setup file and increase Xmx**

`sed -i "s/-Xmx.*/-Xmx8196m/" $HOME/comsol.ini     (here we increase the heap size to 8G)`

-   **4) add '-comsolinifile $HOME/comsol.ini' at the command line.**

`comsol -comsolinifile $HOME/comsol.ini  ...        (... represent other command line options)`

