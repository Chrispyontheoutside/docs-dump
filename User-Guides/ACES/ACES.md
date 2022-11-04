# ACES Phase I

## Hardware Summary

| Component:           | Quantity | Description                                                                                        |
| -------------------- | -------- | -------------------------------------------------------------------------------------------------- |
| Graphcore IPU        | 16       | 16 Colossus GC200 IPUs and dual AMD Rome CPU server on a 100 GbE RoCE fabric                       |
| Intel FPGA PAC D5005 | 2        | FPGA SOC with Intel Stratix 10 SX FPGAs, 64 bit quad-core Arm Cortex-A53 processors, and 32GB DDR4 |
| Intel Optane SSDs    | 8        | 3 TB of Intel Optane SSDs addressable as memory using MemVerge Memory Machine.                     |

## Graphcore IPUs

From one of FASTER login nodes, ssh into poplar1 system.

    [username@faster1 ~]$ ssh poplar1

### Set up the Poplar SDK environment

In this step, set up several environment variables to use the Graphcore
tools and Poplar graph programming framework.
```
[username@poplar1 ~]$ source /opt/gc/poplar/poplar_sdk-ubuntu_18_04-[ver]/poplar-ubuntu_18_04-[ver]/enable.sh 
[username@poplar1 ~]$ source /opt/gc/poplar/poplar_sdk-ubuntu_18_04-[ver]/popart-ubuntu_18_04-[ver]/enable.sh
```
**\[ver\]** indicates the version number of the package.

**Example commands with an existing version on FASTER:**

    source  /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/poplar-ubuntu_18_04-2.5.0+4748-e94d646535/enable.sh
    source  /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/popart-ubuntu_18_04-2.5.1+4748-e94d646535/enable.sh

    mkdir -p /localdata/$USER/tmp
    export TF_POPLAR_FLAGS=--executable_cache_path=/localdata/$USER/tmp`  
    export POPTORCH_CACHE_DIR=/localdata/$USER/tmp
    # export POPLAR_LOG_LEVEL=INFO
    # export POPLIBS_LOG_LEVEL=INFO

### Set up environments of frameworks for IPU

#### PyTorch (Poptorch)

##### Set up PyTorch (Poptorch) for IPU

The local home dir is small (300G total). You can store large files in /localdata/username (or use localdata symlink from your home dir). /localdata has 3.5TB available.

    [username@poplar1 ~]$ cd localdata
    [username@poplar1 localdata]$ virtualenv -p python3 poptorch_test
    [username@poplar1 localdata]$ source poptorch_test/bin/activate
    [username@poplar1 localdata]$ python -m pip install -U pip
    [username@poplar1 localdata]$ python -m pip install <sdk_path>/poptorch_x.x.x.whl
For <code><sdk_path>/poptorch_x.x.x.whl, you can use /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/poptorch-2.5.0+62288_0f4af0bf32_ubuntu_18_04-cp36-cp36m-linux_x86_64.whl</code>, which exists on FASTER

##### Clone a copy of the Graphcore tutorials repository and change the directory to mnist

    [username@poplar1 localdata]$ git clone https://github.com/graphcore/tutorials.git
    [username@poplar1 localdata]$ cd tutorials/simple_applications/pytorch/mnist/

##### Install the dependencies and run the model

    [username@poplar1 mnist]$ pip install -r requirements.txt
    [username@poplar1 mnist]$ python mnist_poptorch.py

#### TensorFlow 1

##### Set up TensorFlow 1 for IPU
The local home dir is small (300G total). You can store large files in /localdata/NetID (or use localdata symlink from your home dir). /localdata has 3.5TB available.

    [username@poplar1 ~]$ cd localdata
    [username@poplar1 localdata]$ virtualenv venv_tf1 -p python3.6
    [username@poplar1 localdata]$ source venv_tf1/bin/activate
    [username@poplar1 localdata]$ python -m pip install <sdk_path>/tensorflow_x.x.x.whl

For <code><sdk_path>/tensorflow_x.x.x.whl, you can use /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/tensorflow-1.15.5+gc2.5.1+193128+c9005c133f4+amd_znver1-cp36-cp36m-linux_x86_64.whl</code>, which exists on FASTER

##### Clone a copy of the Graphcore tutorials repository and change the directory to mnist

    [username@poplar1 localdata]$ https://github.com/graphcore/tutorials.git
    [username@poplar1 localdata]$ cd tutorials/simple_applications/tensorflow/mnist/

##### Run the model

    [username@poplar1 localdata]$ python mnist.py

#### TensorFlow 2

##### Set up TensorFlow 2 for IPU

The local home dir is small (300G total). You can store large files in /localdata/NetID (or use localdata symlink from your home dir). /localdata has 3.5TB available.

    [username@poplar1 ~]$ cd localdata
    [username@poplar1 localdata]$ virtualenv venv_tf2 -p python3.6
    [username@poplar1 localdata]$ source venv_tf2/bin/activate
    [username@poplar1 localdata]$ python -m pip install <sdk_path>/tensorflow_x.x.x.whl

For <code><sdk_path>/tensorflow_x.x.x.whl, you can use /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/tensorflow-2.5.2+gc2.5.1+193132+4673d3afb3b+amd_znver1-cp36-cp36m-linux_x86_64.whl</code>, which exists on FASTER

##### Clone a copy of the Graphcore tutorials repository and change the directory to tensorflow2/keras/completed_demos

    [username@poplar1 localdata]$ https://github.com/graphcore/tutorials.git
    [username@poplar1 localdata]$ cd tutorials/tutorials/tensorflow2/keras/completed_demos/

##### Run the model

    [username@poplar1 completed_demos]$ python completed_demo_ipu.py

    source  /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/poplar-ubuntu_18_04-2.5.0+4748-e94d646535/enable.sh` 
    source  /opt/gc/poplar/poplar_sdk-ubuntu_18_04-2.5.1+1001-64add8f33d/popart-ubuntu_18_04-2.5.1+4748-e94d646535/enable.sh

    mkdir -p /localdata/$USER/tmp  
    export TF_POPLAR_FLAGS=--executable_cache_path=/localdata/$USER/tmp  
    export POPTORCH_CACHE_DIR=/localdata/$USER/tmp  
    # export POPLAR_LOG_LEVEL=INFO  
    # export POPLIBS_LOG_LEVEL=INFO

Graphcore Documentation can be found at
<https://docs.graphcore.ai/en/latest/>

## Liqid PCIe Card with Intel Optane SSDs

Submit a standard batch job or interactive job to the memverge partition

    srun --partition=memverge --time=24:00:00 --pty bash

Sample job file:

    #!/bin/bash
    
    ##NECESSARY JOB SPECIFICATIONS  
    #SBATCH --job-name=Example           #Set the job name to Example  
    #SBATCH --time=24:00:00              #Set the wall clock limit to 24 hrs  
    #SBATCH --nodes=1                    #Request 1 nodes  
    #SBATCH --ntasks-per-node=64         #Request 64 tasks/cores per node  
    #SBATCH --mem=248G                   #Request 248G (248GB) per node  
    #SBATCH --output=Example.%j          #Redirect stdout/err to file  
    #SBATCH --partition=memverge         #Specify the MemVerge partition  
    
    #lines required to setup the environment for your code  
    
    # add the mm command in front of your executable to run with memory machine  
    mm executable


Sample job file to run with singularity

    #!/bin/bash  
    
    ##NECESSARY JOB SPECIFICATIONS`  
    #SBATCH --job-name=Example           #Set the job name to Example  
    #SBATCH --time=24:00:00              #Set the wall clock limit to 24 hrs  
    #SBATCH --nodes=1                    #Request 1 nodes  
    #SBATCH --ntasks-per-node=64         #Request 64 tasks/cores per node  
    #SBATCH --mem=248G                   #Request 248G (248GB) per node  
    #SBATCH --output=Example.%j          #Redirect stdout/err to file  
    #SBATCH --partition=memverge         #Specify the MemVerge partitionexport SINGULARITY_BIND='/var/log/memverge,/etc/memverge,/opt/memverge,/var/memverge'  
    
    # Required directories and libraries for memverge memory machine  
    export SINGULARITY_BIND='/var/log/memverge,/etc/memverge,/opt/memverge,/var/memverge'  
    
    for lib in \  
    libblkid.so.1 \  
    libcrypto.so.1.1 \  
    libc.so.6 \  
    libdaxctl.so.1 \  
    libdl.so.2 \  
    libgcc_s.so.1 \  
    libkmod.so.2 \  
    liblzma.so.5 \  
    libmount.so.1 \  
    libm.so.6 \  
    libndctl.so.6 \  
    libpcre2-8.so.0 \  
    libprotobuf-c.so.1 \  
    libpthread.so.0 \  
    librt.so.1 `  
    libselinux.so.1 \  
    libssl.so.1.1 \  
    libstdc++.so.6 \  
    libudev.so.1 \  
    libuuid.so.1 \  
    libz.so.1 \  
    ; do export  SINGULARITY_BIND=$SINGULARITY_BIND,/lib64/$lib:/lib/$lib ; done  
    
    # run your singularity container command, included the mm command for memverge memory machine  
    singularity exec filename.sif mm executable

## Intel FPGA PAC D5005

The FPGA nodes support both an older OpenCL development workflow, as well as a newer Intel oneAPI workflow.

### Access

To access the Intel FPGA PAC D5005, submit an interactive job to the FPGA partition from one of the FASTER login nodes:

    srun --partition=fpga --time=24:00:00 --pty bash

### Getting Started

Once the session starts, you need to load the environment variables to access and interact with the FPGA on the node:

    $ source /opt/intel/oneapi/setvars.sh
        :: initializing oneAPI environment ...
        -bash: BASH_VERSION = 4.2.46(2)-release
        args: Using "$@" for setvars.sh arguments: 
        :: advisor -- latest
        :: ccl -- latest
        :: compiler -- latest
        :: dal -- latest
        :: debugger -- latest
        :: dev-utilities -- latest
        :: dnnl -- latest
        :: dpcpp-ct -- latest
        :: dpl -- latest
        :: intelfpgadpcpp -- latest
        :: intelpython -- latest
        :: ipp -- latest
        :: ippcp -- latest
        :: ipp -- latest
        :: mkl -- latest
        :: mpi -- latest
        :: tbb -- latest
        :: vpl -- latest
        :: vtune -- latest
        :: oneAPI environment initialized ::

Telemetry for the FPGA can be viewed using the 'fpgainfo' command:

    $ fpgainfo
    FPGA information utility
    Usage:
            fpgainfo [-h] [-B <bus>] [-D <device>] [-F <function>] [-S <socket-id>] {errors,power,temp,fme,port,bmc}
                    -h,--help           Print this help
                    -B,--bus            Set target bus number
                    -D,--device         Set target device number
                    -F,--function       Set target function number
                    -S,--socket-id      Set target socket number
    Subcommands:
    Print and clear errors
            fpgainfo errors [-h] [-c] {all,fme,port}
                    -h,--help           Print this help
                    -c,--clear          Clear all errors
                    --force             Retry clearing errors 64 times
                                        to clear certain error conditions
    Print power metrics
            fpgainfo power [-h]
                    -h,--help           Print this help
    Print thermal metrics
            fpgainfo temp [-h]
                    -h,--help           Print this help
    Print FME information
            fpgainfo fme [-h]
                    -h,--help           Print this help
    Print accelerator port information
            fpgainfo port [-h]
                    -h,--help           Print this help
    Print all Board Management Controller sensor values
            fpgainfo bmc [-h]
                    -h,--help           Print this help


For continuous monitoring, utilize this command in conjunction with the 'watch' command.

To run a status check on the FPGA, run:

    $ aocl diagnose

This will display information about the libraries and initialization status of the FPGA device.

If the device shows as "Unitialized", it can be initialized with a standard image with:

    $ aocl initialize acl0 pac_s10
        aocl initialize: Running initialize from /opt/intel/oneapi/intelfpgadpcpp/latest/board/intel_s10sx_pac/linux64/libexec
        Program succeed.

If the node has multiple FPGA devices, they can be viewed with:

    $ aocl list-devices
        --------------------------------------------------------------------
        Device Name:
        acl0
        
        BSP Install Location:
        /opt/intel/oneapi/intelfpgadpcpp/latest/board/intel_s10sx_pac
        
        Vendor: Intel Corp
        
        Physical Dev Name   Status            Information
        
        pac_ed00000         Passed            Intel PAC Platform (pac_ed00000)
                                            PCIe 29:00.0
                                            USM not supported
        
        DIAGNOSTIC_PASSED
        --------------------------------------------------------------------

The user can then target the correct device when running their code or initializing the device.

### Example

#### oneAPI Samples

The README.md in each directory contains information for compiling and
running.

    $ git clone <https://github.com/oneapi-src/oneAPI-samples.git>  
    $ cd oneAPI-samples/DirectProgramming/DPC++FPGA/Tutorials

#### Example 1: fpga_compile
Navigate to the "fpga_compile" example under "Getting Started" within the oneAPI samples repository:

    $ cd GettingStarted
    $ cd fpga_compile

Create a build directory for configuration files:

    $ mkdir build
    $ cd build

Configure the program to compile for the Intel S10 SX PAC (Intel PAC D5005):

    $ cmake .. -DFPGA_BOARD=intel_s10sx_pac:pac_s10

Once the configuration completes, there will be several make options available:

**Compilation Types**

|Command	|Device Image Type	| Compilation Duration |	Description|
|-----------------|-------------|----------|------------|
|make fpga_emu	| FPGA Emulator| 	Seconds|	Compile for emulation (compiles quickly, targets emulated FPGA device). Allows user to validate design, but does not represent actual performance of code on hardware.|
|make report|	Optimization Report	|Minutes	|Generate the optimization report. The FPGA device code is partially compiled for hardware. The compiler generates an optimization report that describes the structures generated on the FPGA, identifies performance bottlenecks, and estimates resource utilization.|
|make fpga	|FPGA Hardware	|Hours	|Compile for FPGA hardware (takes longer to compile, targets FPGA device). Compiles the actual bitstream for running the program on hardware.|


The recommended workflow is to compile a program for emulation prior to compiling for hardware execution. This does not actually compile the program to run on the FPGA itself, but rather on the CPU via a virtual FPGA emulation device. This allows a user to validate the correctness of their design while benefiting from the short compile times of CPU compilation. The optimization report assists the user in improving different aspects of their design before moving onto hardware compilation.

![](/kb3/assets/images/500px-Oneapi_fpga_development.png)

### Resources

|**Resource**	|**Description**|
|---------------|---------------|
|FPGA Optimization Guide for Intel® oneAPI Toolkits |    The FPGA Optimization Guide for Intel® oneAPI Toolkits provides guidance on leveraging the functionalities of SYCL* to optimize a design.|
|Intel® FPGA Programmable Acceleration Card D5005 Data Sheet	|   This datasheet for the Intel® FPGA PAC shows electrical, mechanical, compliance, and other key specifications. This datasheet assists data center operators and system integrators to properly deploy the Intel® FPGA PAC into their servers. It also documents the FPGA power envelope, connectivity speeds to memory, and network connectivity, so that accelerator function unit (AFU) developers can properly design and test their IP.|
|Intel® Quartus® Prime Pro Edition User Guide: Scripting	|   Detailed guide for running Quartus programs on the command line.|
|Intel® Stratix® 10 FPGAs & SoC FPGA	|   Assorted documentation for the Stratix 10 FPGA family, including pinouts and device schematics.|
|Intel® Stratix® 10 FPGA Developer Center|	Provides various resources to complete an Intel® FPGA design on the Stratix 10 architecture.|

### Support

Please report any issues encountered on the FPGAs to help@hprc.tamu.edu, and include information about actions taken and/or commands run prior to the error so the HPRC team may reproduce and resolve the issue.