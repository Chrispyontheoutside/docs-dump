# LAMMPS

## Description

LAMMPS is a classical molecular dynamics code, and an acronym for
Large-scale Atomic/Molecular Massively Parallel Simulator from Sandia
National Laboratories. - Homepage: <http://lammps.sandia.gov/>

**Documentation:** <http://lammps.sandia.gov/doc/Manual.html>

## Access

LAMMPS is open to all HPRC users.

### Loading the Module

To see all versions of LAMMPS available:

`[ netID@cluster ~]$ `**`module   spider   LAMMPS`**

<font color=teal>**NOTE:** HPRC typically only installs the stable
releases of LAMMPS on the clusters.</font>

To load a particular version of LAMMPS (Example: 17Nov2016-intel-2017A):

`[ netID@cluster ~]$ `**`module   load 
 LAMMPS/17Nov2016-intel-2017A`**

<font color=teal>**NOTE:** On Terra, The normal LAMMPS program is called
lmp\_linux. The GPU-enabled LAMMPS program is called lmp\_gpu.</font>

<font color=teal>**NOTE:** On Grace, The normal LAMMPS program is called
lmp. </font>

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

### Ada Examples

On Ada, to submit a batch job, run:

`[NetID@ada1 ~]$ `**`bsub   <   `*`jobscript`***

#### MPI Job Example

    #!/bin/bash
    
    #BSUB -J lammps                   # Set the job name to "lammps"
    #BSUB -W 1:00                     # Set the wall clock limit to 1hr
    #BSUB -n 40                       # Request 40 tasks 
    #BSUB -R "span[ptile=20]"         # Request 20 tasks per node
    #BSUB -M 2500                     # Set effective memory limit to 2500 MB per task
    #BSUB -R "rusage[mem=2500]"       # Reserve 2500 MB of memory per task
    #BSUB -o lammps.%J                # Send stdout/err to "lammps.[jobID]"
    
    ml LAMMPS/17Nov2016-intel-2017A
    
    mpirun -np 40 lmp_linux -in in.input

#### GPU Job Example

    #!/bin/bash
    
    #BSUB -J lammps_gpu               # Set the job name to "lammps_gpu"
    #BSUB -W 1:00                     # Set the wall clock limit to 1hr
    #BSUB -n 40                       # Request 40 tasks 
    #BSUB -R "span[ptile=20]"         # Request 20 tasks per node
    #BSUB -M 2500                     # Set effective memory limit to 2500 MB per task
    #BSUB -R "rusage[mem=2500]"       # Reserve 2500 MB of memory per task
    #BSUB -o lammps_gpu.%J            # Send stdout/err to "lammps_gpu.[jobID]"
    #BSUB -R "select[gpu]"            # Use only gpu nodes for this job
    
    ml LAMMPS/17Nov2016-intel-2017A
    
    # these extra arguments enable the gpu suffix for various styles AND tell LAMMPS to use two GPUs per node
    mpirun -np 40 lmp_gpu -sf gpu -pk gpu 2 -in in.input

### Terra Examples

On Terra, to submit a batch job, run:

`[NetID@terra1 ~]$ `**`sbatch   `*`jobscript`***

#### MPI Job Example

    #!/bin/bash
    
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=lammps        # Set the job name to "lammps"
    #SBATCH --time=01:30:00          # Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=56              # Request 56 tasks
    #SBATCH --ntasks-per-node=28     # Request 28 task per node
    #SBATCH --mem=40G                # Request 40GB per node
    #SBATCH --output=lammps.%j       # Send stdout/err to "lammps.[jobID]"
    
    ml LAMMPS/17Nov2016-intel-2017A
    
    mpirun lmp_linux -in inputfile

#### GPU Job Example

<font color=teal>**NOTE:** GPU jobs should be submitted to the gpu
partition and MUST specify how many GPUs are required per node.</font>

    #!/bin/bash
    
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=lammps_gpu    # Set the job name to "lammps_gpu"
    #SBATCH --time=01:30:00          # Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=56              # Request 56 tasks
    #SBATCH --ntasks-per-node=28     # Request 28 task per node
    #SBATCH --mem=40G                # Request 40GB per node
    #SBATCH --output=lammps_gpu.%j   # Send stdout/err to "lammps_gpu.[jobID]"
    #SBATCH --gres=gpu:2             # Request 2 GPUs per node
    #SBATCH --partition=gpu          # Submit job to the gpu queue
    
    ml LAMMPS/17Nov2016-intel-2017A
    
    # these extra arguments enable the gpu suffix for various styles AND tell LAMMPS to use two GPUs per node
    mpirun lmp_gpu -sf gpu -pk gpu 2 -in inputfile

### Grace Examples

On Grace, to submit a batch job, run:

`[NetID@grace1 ~]$ `**`sbatch   `*`jobscript`***

#### MPI Job Example

    #!/bin/bash
    
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=lammps        # Set the job name to "lammps"
    #SBATCH --time=01:30:00          # Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=56              # Request 56 tasks
    #SBATCH --ntasks-per-node=28     # Request 28 task per node
    #SBATCH --mem=40G                # Request 40GB per node
    #SBATCH --output=lammps.%j       # Send stdout/err to "lammps.[jobID]"
    
    ml GCC/8.3.0 OpenMPI/3.1.4
    ml LAMMPS/3Mar2020-Python-3.7.4-kokkos
    
    mpirun lmp -in inputfile
