# Optistruct

## Description

OptiStruct is an industry proven, modern structural analysis solver for
linear and nonlinear problems under static and dynamic loadings. -
Homepage: <http://www.altairhyperworks.com/product/OptiStruct>

### Documentation

We have documentation available for the following versions of Optistruct

  - [Optistruct Documentation from
    Hyperworks 2017](https://hprc.tamu.edu/softwareDocs/hyperworks/2017/hwsolvers/hwsolvers.htm?ug_altair_optistruct.htm)

## Access

Optistruct is included with Hyperworks.

To see all versions of Hyperworks available on Ada:

` [ netID@cluster ~]$ `**`module   spider   Hyperworks`**

To load a particular version of Hyperworks on Ada (Example: 2017):

` [ netID@cluster ~]$ `**`module   load   Hyperworks/2017`**

## Using Optistruct Solvers

This section covers using the Optistruct Solvers in batch jobs.

### SMP Mode

First, you should run a check to determine estimated memory and disk
requirements for your Optistruct input:

` ml Hyperworks/2017 `  
` optistruct -check test.fem`

Look at the **in-core** solution memory and disk space information in
the resulting output (has a .out suffix). An in-core solution will
attempt to run the solver in memory as much as possible and minimize
disk use.

    MEMORY ESTIMATION INFORMATION :
    -------------------------------                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                
     Solver Type is:  Sparse-Matrix Solver                                                                                                                                                                                                                                                                      
                      Direct Method                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                
     Current Memory (RAM)                                    :    1337 MB                                                                                                                                                                                                                                       
     Estimated Minimum Memory (RAM) for Minimum Core Solution:    1875 MB                                                                                                                                                                                                                                       
     Recommended Memory (RAM) for Minimum Core Solution      :    1875 MB                                                                                                                                                                                                                                       
     Estimated Minimum Memory (RAM) for Out of Core Solution :    2527 MB                                                                                                                                                                                                                                       
     Recommended Memory (RAM) for Out of Core Solution       :    2734 MB                                                                                                                                                                                                                                       
     Recommended Memory (RAM) for In-Core Solution           :   11739 MB   <-------------                                                                                                                                                                                                                      
     (Note: Minimum Core Solution Process is Activated.)                                                                                                                                                                                                                                                        
     (Note: The Minimum Memory Requirement is limited by Output Module.)
    
    DISK SPACE ESTIMATION INFORMATION :                                                                                                                                                                                                                                                                         
    -----------------------------------                                                                                                                                                                                                                                                                         
                                                                                                                                                                                                                                                                                                                
     Estimated Disk Space for Output Data Files              :     412 MB                                                                                                                                                                                                                                       
     Estimated Scratch Disk Space for In-Core Solution       :    1718 MB   <-------------                                                                                                                                                                                                                      
     Estimated Scratch Disk Space for Out of Core Solution   :   14962 MB                                                                                                                                                                                                                                       
     Estimated Scratch Disk Space for Minimum Core Solution  :   15821 MB 

The above information shows that estimate requirements of 12 GB of
memory and 2 GB of disk space for an in-core solution.

The following example is a job script for running Optistruct in SMP mode
with 12 threads on Ada based on the above estimates. **The number of
threads to use in SMP mode for the best performance may vary per input
file but should not exceed 20 threads on Ada.**

    #BSUB -J optistruct          # Set the job name to "optistruct"
    #BSUB -L /bin/bash           # Uses the bash login shell to initialize the job's execution environment.                                                                                                                                                                                                     
    #BSUB -W 2:00                # Set the wall clock limit to 2hr                                                                                                                                                                                                                                              
    #BSUB -n 12                  # Request 12 cores                                                                                                                                                                                                                                                             
    #BSUB -R "span[ptile=12]"    # Request 12 cores per node.                                                                                                                                                                                                                                                   
    #BSUB -R "rusage[mem=1200]"  # Request 1200MB per process (CPU) for the job which results in about 14 GB of memory for this job                                                                                                                                                                             
    #BSUB -M 1200                # Set the per process enforceable memory limit to 1200MB.                                                                                                                                                                                                                      
    #BSUB -o optistruct.%J       # Send stdout and stderr to "optistruct.[jobID]"                                                                                                                                                                                                                               
                                                                                                                                                                                                                                                                                                                
    ml Hyperworks/2017                                                                                                                                                                                                                                                                                          
                                                                                                                                                                                                                                                                                                                
    # run optistruct in SMP mode with 12 threads with the in-core solution (completely in memory)                                                                                                                                                                                                               
    optistruct -nt 12 -core IN test2.fem
