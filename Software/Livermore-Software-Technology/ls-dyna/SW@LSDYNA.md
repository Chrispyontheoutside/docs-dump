# LS-DYNA

LS-DYNA is a general-purpose finite element program capable of
simulating complex real world problems. - Homepage:
<http://www.lstc.com/products/ls-dyna>

## Documentation

<font color=teal>**Note:** You will need to be within the TAMU firewall
in order to view these documents. You will need to either be on campus
OR connect using VPN. Information on the TAMU VPN can be found
[here](https://u.tamu.edu/KB0010938). </font>

  - LS-DYNA R8.0:
      - [Volume
        I](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_I_R8.0.pdf)
      - [Volume II (Material
        Models)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_II_R8.0.pdf)
      - [Volume III (Multi-Physics
        Solvers)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_III_R8.0.pdf)
  - LS-DYNA R9.0:
      - [Volume
        I](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_I_R9.0.pdf)
      - [Volume II (Material
        Models)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_II_R9.0.pdf)
      - [Volume III (Multi-Physics
        Solvers)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_III_R9.0.pdf)
  - LS-DYNA R10.0:
      - [Volume
        I](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_I_R10.0.pdf)
      - [Volume II (Material
        Models)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_II_R10.0.pdf)
      - [Volume III (Multi-Physics
        Solvers)](https://hprc.tamu.edu/softwareDocs/lsdyna/LS-DYNA_Manual_Volume_III_R10.0.pdf)

<!-- end list -->

  - [LS-DYNA Theory
    Manual](https://hprc.tamu.edu/softwareDocs/lsdyna/ls-dyna_theory_manual_2006.pdf)

### Online Resources

  - [LS-DYNA support site](https://www.dynasupport.com/)
  - [LS-DYNA Examples](https://www.dynaexamples.com/)
  - [Modeling guidelines document (MGD) from the LS-DYNA Aerospace
    Working Group](http://awg.lstc.com/tiki/tiki-index.php?page=MGD)
  - [LS-DYNA Tutorials and Topical Presentations from the LS-DYNA
    Aerospace Working
    Group](http://awg.lstc.com/tiki/tiki-index.php?page=LSTC+Tutorials+and+Topic+Presentations)
  - [The history of LS-DYNA by David
    Benson](https://www.d3view.com/wp-content/uploads/2007/06/benson.pdf)
  - [Time integration, explicit and Implicit time integration schemes by
    Suri
    Bala](https://www.d3view.com/wp-content/uploads/2007/04/timeintegration_v1.pdf)

## Access

<font color=teal>**LS-DYNA is ONLY available to any users within an
academic department which has purchased their own license**</font>. We
host the license on behalf of the licensed department(s).

### Loading the Module

To see all versions of LS-DYNA available on Ada:

`[NetID@cluster ~]$ module spider LS-DYNA`

To load a particular version of LS-DYNA on Ada (Example: R9.1.0):

`[NetID@cluster ~]$ module load LS-DYNA/R9.1.0`

To show the program names for a particular version of LS-DYNA:

``` 
 [NetID@cluster ~]$ module help LS-DYNA/R9.1.0

----------------------------------------------------- Module Specific Help for "LS-DYNA/R9.1.0" -----------------------------------------------------
  LS-DYNA is a general-purpose finite element program capable of simulating complex real world problems. - Homepage: http://www.lstc.com/products/ls-dyna/
    
  Sets up environment for LS-DYNA 
  Version                        Precision      Command  
  OpenMP OR Serial               Single         ls-dyna_smp_s 
  OpenMP OR Serial               Double         ls-dyna_smp_d 
  MPP (Intel MPI)                Single         ls-dyna_mpp_s 
  MPP (Intel MPI)                Double         ls-dyna_mpp_d 
  Test inputs for LS-DYNA are available in the following directory: /software/tamusc/LS-DYNA/examples 
```

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

### Ada Example

<font color=teal>A double precision SMP example with 20 cores on a
single node:</font>

    #BSUB -J LSDYNAJob1        # sets the job name to LSDYNAJob1
    #BSUB -L /bin/bash         # uses the bash login shell to initialize the job's execution environment
    #BSUB -W 48:00             # sets to 48 hours the job's runtime wall-clock limit
    #BSUB -n 20                # assigns 20 cores for execution.
    #BSUB -R "span[ptile=20]"  # assigns 20 cores per node.
    #BSUB -R "rusage[mem=1500]"  # reserves 1500MB per process/CPU for the job
    #BSUB -M 1500              # sets to 1500MB (~1.5GB) the per process enforceable memory limit.
    #BSUB -o stdout1.%J        # directs the job's standard output to stdout1.jobid
    
    
    ## Load the necessary modules
    module load LS-DYNA/R9.1.0
    
    ## Run LS-DYNA with the proper parameters.  
    ## The number of threads MUST be specified using both the OMP_NUM_THREADS variable and the ncpu option.
    export OMP_NUM_THREADS=20
    ls-dyna_smp_d ncpu=20 I=InputFile O=OutputFile MEMORY=300m D=d3dump

<font color=teal>A double precision MPP example with 40 cores across two
nodes:</font>

    #BSUB -J LSDYNAJob1        # sets the job name to LSDYNAJob1
    #BSUB -L /bin/bash         # uses the bash login shell to initialize the job's execution environment
    #BSUB -W 48:00             # sets to 48 hours the job's runtime wall-clock limit
    #BSUB -n 40                # assigns 40 cores for execution.
    #BSUB -R "span[ptile=20]"  # assigns 20 cores per node.
    #BSUB -R "rusage[mem=2500]"  # reserves 2500MB per process/CPU for the job
    #BSUB -M 2500              # sets to 2500MB (~2.5GB) the per process enforceable memory limit.
    #BSUB -o stdout1.%J        # directs the job's standard output to stdout1.jobid
    
    
    ## Load the necessary modules
    module load LS-DYNA/R9.1.0
    
    ## Run LS-DYNA with the proper parameters
    mpirun ls-dyna_mpp_d I=InputFile O=OutputFile MEMORY=300m D=d3dump

To submit the batch job, run:

`[NetID@ada1 ~]$ bsub < jobscript`

### Terra Example

<font color='teal'>A double precision SMP example using 28 cores on a
single node:</font>

    #!/bin/bash
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=lsdyna      #Set the job name to "lsdyna"
    #SBATCH --time=01:30:00        #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks-per-node=28   #Request 28 tasks per node
    #SBATCH --ntasks=28            #Request 20 tasks/cores (total)
    #SBATCH --mem=50000M           #Request 50GB per node
    #SBATCH --output=stdout.%j     #Send stdout/err to "lsdyna.[jobID]"
    
    module load LS-DYNA/R9.1.0
    
    ## The number of threads MUST be specified using both the OMP_NUM_THREADS variable and the ncpu option.
    export OMP_NUM_THREADS=28
    ls-dyna_smp_d i=main.k ncpu=28 memory=500m memory2=200m

<font color='teal'>A double precision MPP example using 56 cores across
two nodes:</font>

    #!/bin/bash
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=lsdyna      #Set the job name to "lsdyna"
    #SBATCH --time=01:30:00        #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks-per-node=28   #Request 28 tasks per node
    #SBATCH --ntasks=56            #Request 20 tasks/cores (total)
    #SBATCH --mem=50000M           #Request 50GB per node
    #SBATCH --output=stdout.%j     #Send stdout/err to "lsdyna.[jobID]"
    
    module load LS-DYNA/R9.1.0
    
    # launch MPI program using the hydra launcher
    mpirun -n 56  ls-dyna_mpp_d i=main.k memory=500m memory2=200m

### Memory Specification

The LS-DYNA command line option MEMORY specifies memory per node with a
base unit words. The argument can be specified in words or megawords
(denoted by m). For single precision LS-DYNA, a word is 4 bytes and a
megaword is 4 MB. For double precision, a word is 8 bytes and a megaword
is 8MB.

Example: (Single Precision)

    MEMORY=300m     #300 megawords = 300 megawords * 4 MB = 1200 MB (~1.2GB)
    MEMORY=600      #600 words = 600 words * 4 B = 2400 KB

Example: (Double Precision)

    MEMORY=300m     #300 megawords = 300 megawords * 8 MB = 2400 MB (~2.4GB)
    MEMORY=600      #600 words = 600 words * 8 B = 4800 KB

### Checking Input Before Running

If there are no licenses currently available, or if you would not like
to check out licenses. There is a way to initialize your model and check
for errors without using any licenses. This can be done with the mcheck
command option.

Example:

    #BSUB -J LSDYNAJob1        # sets the job name to LSDYNAJob1
    #BSUB -L /bin/bash         # uses the bash login shell to initialize the job's execution environment
    #BSUB -W 48:00             # sets to 48 hours the job's runtime wall-clock limit
    #BSUB -n 40                # assigns 40 cores for execution.
    #BSUB -R "span[ptile=20]"  # assigns 20 cores per node.
    #BSUB -R "rusage[mem=2500]"  # reserves 2500MB per process/CPU for the job
    #BSUB -M 2500              # sets to 2500MB (~2.5GB) the per process enforceable memory limit.
    #BSUB -o stdout1.%J        # directs the job's standard output to stdout1.jobid
    
    
    ## Load the necessary modules
    module load LS-DYNA/R7.1.2
    
    ## Run LS-DYNA with the proper parameters
    mpirun ls-dyna_mpp_d I=InputFile O=OutputFile MEMORY=300m mcheck=1

## Related Software

The following software is also available on our clusters for use with
LS-DYNA:

  - [ LS-OPT](/kb3/Software/Livermore-Software-Technology/ls-opt/SW@LS-OPT/ "wikilink"): A standalone Design Optimization
    and Probabilistic Analysis package with an interface to LS-DYNA.
  - [ LS-PREPOST](/kb3/Software/Livermore-Software-Technology/ls-prepost/SW@LS-PREPOST/ "wikilink"): An advanced pre and
    post-processor for LS-DYNA.
  - LS-TASC: A Topology and Shape Computation tool. Developed for
    engineering analysts who need to optimize structures, LS-TaSC works
    with both the implicit and explicit solvers of LS-DYNA. LS-TaSC
    handles topology optimization of large non-linear problems,
    involving dynamic loads and contact conditions.

## More Information

To find more information on LS-DYNA, please consult the LS-DYNA manuals
located at <http://www.dynasupport.com/manuals>.
