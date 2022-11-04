# Terra Compiling and Running 


## A Note on Terra Usage

<font color=teal> This page used a lot of information written for Ada.

The majority of the content on this page is applicable to Terra. Some
modifications to modules, directories, or other non-major concepts may
be needed. </font>

## Getting Started

### Toolchain selection

For developing code on Terra we recommend using the **intel** software
stack (which is often referenced as a "toolchain" here at HPRC), which
includes the Intel compilers (icc/icpc/ifort), the Intel Math Kernel
Library (MKL), and the Intel MPI. **A note for Terra Users:** the Intel
compilers are the only compilers able to compile programs for the Phi
co-processors.

We highly recommend users select a particular toolchain and stick with
modules that use it. At present, we support the following toolchains:

  - **intel** - described above
  - **iomkl** - which substitutes OpenMPI for Intel's MPI
  - **foss** - which is entirely Free and Open-Source Software
    (GCC/OpenMPI/BLAS/LAPACK/etc)

<font color=teal>Detailed information about each of the currently
supported toolchain releases can be found on our [
Toolchains](/kb3/Software/useful-tools/SW@Toolchains/ "wikilink") page.</font>  
Toolchains, like software packages on our clusters, are organized with
the [ Modules System](/kb3/Software/useful-tools/SW@Modules/ "wikilink"). You can load a toolchain
with the following command:

`[ netID@cluster ~]$ module load `*`[toolchain Name]`*   

<font color=teal>**Important Note:** Do **NOT** mix modules from different toolchains. Remember to **ALWAYS** purge all modules when switching toolchains.</font>  

More information on using the Modules System can be found on our [Modules System](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

### Using the intel toolchain

After initializing the compiler environment, you can use the "man"
command to obtain a complete list of the available compilation options
for the language you plan to use. The following three commands will
provide information on the C, C++, and Fortran compilers, respectively.

`[ netID@cluster ~]$ `**`man   icc`**  
`[ netID@cluster ~]$ `**`man   icpc`**  
`[ netID@cluster ~]$ `**`man   ifort`**

Each compiler requires appropriate file name extensions. These
extensions are meant to identify files with different programming
language contents, thereby enabling the compiler script to hand these
files to the appropriate compiling subsystem: preprocessor, compiler,
linker, etc. See table below for valid extensions for each language.

| Extension                | Compiler       | Description                                                                                                   |
| ------------------------ | -------------- | ------------------------------------------------------------------------------------------------------------- |
| .c                       | icc            | C source code passed to the compiler.                                                                         |
| .C, .CC, .cc, .cpp, .cxx | icpc           | C++ source code passed to the compiler.                                                                       |
| .f, .for, .ftn           | ifort          | Fixed form Fortran source code passd to the compiler.                                                         |
| .fpp                     | ifort          | Fortran fixed form source code that can be preprocessed by the Intel Fortran preprocessor fpp.                |
| .f90                     | ifort          | Free form Fortran 90/95 source code passed to the compiler.                                                   |
| .F                       | ifort          | Fortran fixed form source code, will be passed to preprocessor (fpp) and then passed to the Fortran compiler. |
| .o                       | icc/icpc/ifort | Compiled object file--generated with the -c option--passed to the linker.                                     |

Basic Valid File Extensions

**Note:** The icpc command ("C++" compiler) uses the same compiler
options as the icc ("C" compiler) command. Invoking the compiler using
icpc compiles '.c', and '.i' files as C++. Invoking the compiler using
icc compiles '.c' and '.i' files as C. Using icpc always links in C++
libraries. Using icc only links in C++ libraries if C++ source is
provided on the command line.

## Compiling

### Invoking the compiler

To compile your program and create an executable you need to invoke the
correct compiler. The default output file name is **a.out** but this can
be changed using the *-o* compiler flag. All compilers are capable of
preprocessing, compiling, assembling, and linking. See table below for
the correct compiler commands for the different languages.

| Language | Compiler | Syntax                                                       |
| -------- | -------- | ------------------------------------------------------------ |
| C        | icc      | icc ***\[c compiler\_flags\]*** file1 \[ file2 \]...         |
| C++      | icpc     | icpc ***\[c++ compiler\_flags\]*** file1 \[ file2 \]...      |
| F90      | ifort    | ifort ***\[fortran compiler\_flags\]*** file1 \[ file2 \]... |
| F77      | ifort    | ifort ***\[fortran compiler\_flags\]*** file1 \[ file2 \]... |

In the table above, **fileN** is an appropriate source file, assembly
file, object file, object library, or other linkable file.

### Basic compiler flags

The next sections introduce some of the most common compiler flags.
These flags are accepted by all compilers (icc/icpc/ifort) with some
notable exceptions. For a full description of all the compiler flags
please consult the appropriate man pages.

<table>
<thead>
<tr class="header">
<th><p>Flag</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>-help [category]</p></td>
<td><p>Displays all available compiler options or category of compiler options categories.</p></td>
</tr>
<tr class="even">
<td><p>-o <file></p></td>
<td><p>Specifies the name for an output file. For an executable, name of output file will be <file> instead of a.out</p></td>
</tr>
<tr class="odd">
<td><p>-c</p></td>
<td><p>Only compile the file, linking phase will be skipped</p></td>
</tr>
<tr class="even">
<td><p>-L &ltdir&gt</p></td>
<td><p>Tells the linker to search for libraries in directory &ltdir&gt ahead of the standard library directories.</p></td>
</tr>
<tr class="odd">
<td><p>-l <strong>&ltname&gt</strong></p></td>
<td><p>Tells the linker to search for library named lib<strong>name</strong>.so or lib<strong>name</strong>.a</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Optimization flags

The default optimization level for Intel compilers is -O2 (which enables
optimizations like inlining, constant/copy propagation, loop
unrolling,peephole optimizations, etc). The table below shows some
addional commonly used optimization flags that can be used to improve
run time.

| Flag               | Description                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| \-O3               | Performs -O2 optimizations and enables more aggressive loop transformations.                                      |
| \-xHost            | Tells the compiler to generate vector instructions for the highest instruction set available on the host machine. |
| \-fast             | Convenience flag. In linux this is shortcut for -ipo, -O3, -no-prec-div, -static, and -xHost                      |
| \-ip               | Perform inter-procedural optimization within the same file                                                        |
| \-ipo              | Perform inter-procedural optimization between files                                                               |
| \-parallel         | enable automatic parallelization by the compiler (very conservative)                                              |
| \-opt-report=\[n\] | generate optimization report. n represent the level of detail (0 ..3, 3 being most detailed)                      |
| \-vec-report\[=n\] | generate vectorization report. n represents the level of detail (0..7 , 7 being most detailed)                    |

**NOTE:** there is no guarantee that using a combination of the flags
above will provide additional speedup compared to -O2. In some rare
cases (e.g. floating point imprecision) using flags like -fast might
result in code that might produce incorrect results.

<font color=teal>**Large Memory Nodes on Terra:** These 48 nodes have
128GB of memory. </font>

### Debugging flags

The table below shows some compiler flags that can be useful in
debugging your program.

| Flag        | Description                                                                                                                                                                                                                 |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \-g         | Produces symbolic debug information in the object file.                                                                                                                                                                     |
| \-warn      | Specifies diagnostic messages to be issued by the compiler.                                                                                                                                                                 |
| \-traceback | Tells the compiler to generate extra information in the object file to provide source file traceback information when a severe error occurs at run time.                                                                    |
| \-check     | Checks for certain conditions at run time (e.g. uninitialized variables, array bounds). Note, since the resulting code includes additional run time checks it may affect run time significantly. THIS IS AN IFORT ONLY FLAG |
| \-fpe0      | throw exception for invalid, overflow, divide by zero. THIS IS AN IFORT ONLY FLAG                                                                                                                                           |

### Flags affecting floating point operations

Some optimization might affect how floating point arithmetic is
performed. This might result in round off errors in certain cases. The
table below shows a number of flags to instruct the compiler how to deal
with floating point operations:

| Flag                    | Description                                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------------------- |
| \-fp-model precise      | disable optimizations that are not value safe on floating point data (See man page for other options)   |
| \-fltconsistency        | enables improved floating-point consistency. This might slightly reduce execution speed.                |
| \-fp-speculation=strict | tells the compiler to disable speculation on floating-point operations (See man page for other options) |

### Examples

Several examples of compile commands are listed below.  
<span style="font-size:120%;">**Example 1:**</span> Compile program
consisting of c source files and an object file.

`[ netID@cluster ~]$ `**`icc   `*`objfile.o   subroutine.c 
 main.c`***` `

<span style="font-size:120%;">**Example 2:**</span> Compile and link
source files and an object file, rename the output myprog.x

`[ netID@cluster ~]$ `**`icc -o `*`myprog.x   subroutine.c 
 myobjs.o   main.c`***

<span style="font-size:120%;">**Example 3:**</span> Compile and link
source file and library libmyutils.so residing in directory mylibs

`[ netID@cluster ~]$ `**`icc -L `*`mylibs   -lmyutils   main.c`***

<span style="font-size:120%;">**Example 4:**</span> Compile and link
program with aggressive optimization enabled, uses latest vector
instructions, and print optimization report.

`[ netID@cluster ~]$ `**`icc -fast -xHost -opt-report -o `*`myprog.x myprog.c`***

## OpenMP Programs

### Compiling OpenMP code

To compile program containing OpenMP parallel directives the following
flags can be used to create multi-threaded versions:

| Flag            | Description                                                |
| --------------- | ---------------------------------------------------------- |
| \-qopenmp       | Enables parallelizer to generate multi-threaded code.      |
| \-qopenmp-stubs | Enables compilation of OpenMP programs in sequential mode. |

**Examples:**

`[ netID@cluster ~]$ `**`icc   -qopenmp   -o   `*`myprog.x 
 myprog.c`***  
`[ netID@cluster ~]$ `**`ifort   -qopenmp   `*`myprog.x 
 myprog.f90`***  
`[ netID@cluster ~]$ `**`ifort   -qopenmp-stubs   -o 
 `*`myprog.x   myprog.f90`***

### Running OpenMP code

The table below shows some of the more common environmental variables
that can be used to affect OpenMP behavior at run time.

| Environment Variable| Example| Example-Purpose| Default value |
| ------------- | ------------- | ------------- | ------------- |
| OMP\_NUM\_THREADS=n\[,m\]\*  | OMP\_NUM\_THREADS=8       | Sets the maximum number of threads per nesting level to 8.                                                                                   | 1             |
| OMP\_STACKSIZE=\[B\|K\|M\|G\]   | OMP\_STACKSIZE=8M         | Sets the size for the private stack of each worker thread to 8MB. Possible values for type are **B(Bytes), K(KB), M(MB)**, and **G(GB)**.    | 4M            |
| OMP\_SCHEDULE=type\[,chunk\] | OMP\_SCHEDULE=DYNAMIC     | Sets the default run-time schedule type to DYNAMIC. Possible values for type are **STATIC, DYNAMIC, GUIDED**, and **AUTO**.                  | STATIC        |
| OMP\_DYNAMIC                 | OMP\_DYNAMIC=true         | Enable dynamic adjustment of number of threads.                                                                                              | false         |
| OMP\_NESTED                  | OMP\_NESTED=true          | Enable nested OpenMP regions.                                                                                                                | false         |
| OMP\_DISPLAY\_ENV=val        | OMP\_DISPLAY\_ENV=VERBOSE | Instruct the OpenMP runtime to display OpenMP version and environmental variables in verbose form. Possible values are TRUE, FALSE, VERBOSE. | FALSE         |

### Examples

**Example 1:** set number of threads to 8 and set the stack size for
workers thread to 16MB. Note; insufficient stack size is a common reason
of run-time crashes of OpenMP programs.

`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`8`***  
`[ netID@cluster ~]$ `**`export   OMP_STACKSIZE=`*`16M`***  
`[ netID@cluster ~]$ `***`./myprog.x`***

**Example 2:** enable nested parallel regions and set the number of
threads to use for first nesting level to 4 and second nesting level to
2

`[ netID@cluster ~]$ `**`export   OMP_NESTED=`*`true`***  
`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`4,2`***  
`[ netID@cluster ~]$ `***`./myprog.x`***

**Example 3:** set maximum number of threads to use to 16, but let run
time decide how many threads will actually be used in order to optimize
the use of system resources

`[ netID@cluster ~]$ `**`export   OMP_DYNAMIC=`*`true`***  
`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`16`***  
`[ netID@cluster ~]$ `***`./myprog.x`***

**Example 4:** change the default scheduling type to dynamic with chunk
size of 100.

`[ netID@cluster ~]$ `**`export 
 OMP_SCHEDULE=`*`"dynamic,100"`***  
`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`16`***  
`[ netID@cluster ~]$ `**`./`*`myprog.x`***

### Advanced OpenMP

The following tables shows some more advanced environmental variables
that can be used to control where OpenMP threads will actually be placed

| Env var         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Default value |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| KMP\_AFFINITY   | binds OpenMP threads to physical threads.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |               |
| OMP\_PLACES     | Defines an ordered list of places where threads can execute. Every place is a set of hardware (HW) threads. Can be defined as an explicit list of places described by nonnegative numbers or an abstract name. Abstract name can be 'threads' (every place consists of exactly one hw thread), 'cores' (every place contains all the HW threads of the core), 'socket' (every places contains all the HW threads of the socket)                                                                                                              | 'threads'     |
| OMP\_PROC\_BIND | Sets the thread affinity policy to be used for parallel regions at the corresponding nesting level. Acceptable values are true, false, or a comma separated list, each element of which is one of the following values: master (all threads will be bound to same place as master thread), close (all threads will be bound to successive places close to place of master thread), spread (all threads will be distributed among the places evenly). NOTE: if both OMP\_PROC\_BIND and KMP\_AFFINITY are set the latter will take precedence | 'false'       |

**Example 1:** Suppose node with two sockets, each with 8 cores.
Program, with nesting level 2, put outer level threads on different
sockets, inner level threads on same socket as master.

`[ netID@cluster ~]$ `**`export   OMP_NESTED=`*`true`***  
`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`2,8`***  
`[ netID@cluster ~]$ `**`export   OMP_PLACES=`*`"sockets"`***  
`[ netID@cluster ~]$ `**`export 
 OMP_PROC_BIND=`*`"spread,master"`***  
`[ netID@cluster ~]$ `**`./`*`myprog.x`***

## MPI Programs

There are currently two MPI stacks installed on ADA; OpenMPI and Intel
MPI. The recommended MPI stack for software development is the Intel MPI
software stack and most of this section will focus on this MPI stack.

### Intel MPI

To use the Intel MPI environment you need to load the Intel module. This
can be done with the following command:

`[ netID@cluster ~]$ `**`module   load   intel/2017A`**

<font color=teal>**Note:** It is no longer possible to load the default
intel module. You must specify a version you are loading for the sake of
consistency and clarity. More information about finding and loading
modules can be found on our [ Modules Systems](/kb3/Software/useful-tools/SW@Modules/ "wikilink")
page. </font>

#### Compiling MPI Code

To compile MPI code a MPI compiler wrapper is used. The wrapper will
call the appropriate underlying compiler with additional linker flags
specific for MPI programs. The Intel MPI software stack has wrappers for
Intel compilers as well as wrappers for gnu compilers. Any argument not
recognized by the wrapper will be passed to the underlying compiler.
Therefore, any valid compiler flag (Intel or gnu) will also work when
using the mpi wrappers

The following table shows the most commonly used MPI wrappers used by
Intel MPI.

| MPI Wrapper | Compiler | Language | Example                            |
| ----------- | -------- | -------- | ---------------------------------- |
| mpiicc      | icc      | C        | mpiicc <compiler_flags\> prog.c     |
| mpicc       | gcc      | C        | mpicc <compiler_flags\> prog.c      |
| mpiicpc     | icpc     | C++      | mpiicpcp <compiler_flags\> prog.cpp |
| mpicxx      | g++      | C++      | mpicxx <compiler_flags\> prog.cpp   |
| mpiifort    | ifort    | Fortran  | mpiifort <compiler_flags\> prog.f90 |
| mpif90      | gfortran | Fortran  | mpif90 <compiler_flags\> prog.f90   |

To see the full compiler command of any of the mpi wrapper scripts use
the \*\*-show\*\* flag. This flag does not actually call the compiler,
it only prints the full compiler command and exits. This can be useful
for debugging purposes and/or when experiencing problems with any of the
compiler wrappers

**Example:** Show the full compiler command for the mpiifort wrapper
script

    [ netID@cluster ~]$ mpiifort -show   
    ifort -I/software/easybuild/software/impi/4.1.3.049/intel64/include -I/software/easybuild/software/impi/4.1.3.049/intel64/include  
    -L/software/easybuild/software/impi/4.1.3.049/intel64/lib -Xlinker --enable-new-dtags -Xlinker -rpath -Xlinker   
    /software/easybuild/software/impi/4.1.3.049/intel64/lib -Xlinker -rpath -Xlinker 
    -opt/intel/mpi-rt/4.1 -lmpigf -lmpi -lmpigi -ldl -lrt -lpthread

#### Running MPI Code

Running MPI code requires an MPI launcher. The latter will setup the
environment and start the requested number of MPI tasks on the needed
nodes.  
Use the following command to launch an MPI program where
*\[mpi\_flags\]* are options passed to the mpi launcher, *<executable>*
is the name of the mpi program and *\[executable params\]* are optional
parameters for the mpi program. (We continue to assume here use of the
Intel MPI stack.):

` [ netID@cluster ~]$ mpirun `*`[mpi_flags]   `<executable>` 
 [executable   params]`**`''`

<font color=teal> **Note:** <executable\> must be on the **$PATH** otherwise the launcher will not be able to find the executable.</font>

For a list of the most common *mpi\_flags* See table below. This table
shows only a very small subset of all flags. To see a full listing type
**mpirun --help**

| Flag                | Description|
| ------------------- | ------------------- |
| \-np <n\>            | The number of mpi tasks to start.|
| \-n <n\>             | The number of mpi tasks to start (same as -np).|
| \-perhost <n\>       | Places <n> consecutive (MPI) processes on each host/node.|
| \-ppn <n\>           | Stands for Process (i.e., task) Per Node (same as -perhost)|
| \-hostfile <file\>   | The name of the file that contains the list of host/node names the launcher will place tasks on. |
| \-f <file\>          | Same as -hostfile|
| \-hosts {host list} | comma separated list of specific host/node names.|
| \-help              | Shows list of available flags and options|

#### Hybrid MPI/OpenMP Code

To compile hybrid mpi/OpenMP programs (i.e. MPI programs that also
contain OpenMP directives) invoke the appropriate mpi wrapper and add
the **-openmp** flag to enable processing of OpenMP primitives.

Running a hybrid program is very similar to running a pure mpi program.
To control the number of OpenMP threads to use per task the
**OMP\_NUM\_THREADS** environmental variable can be set.

##### Advanced: mapping tasks and threads

Explicitly mapping mpi tasks to processors can result in significantly
better performance.This is especially true for hybrid MPI/OpenMP
programs where both mpi tasks and OpenMP threads are being mapped on the
available cores on a node. The Intel MPI stack provides a way to control
the pinning of MPI tasks using the environmental variable *'
I\_MPI\_PIN\_DOMAIN*'.

`[ netID@cluster ~]$ `*`export   I_MPI_PIN_DOMAIN=`*`<domain>`

where *<domain>* can have the following values; **node, socket, core,
cache1, cache2, cache3**. The domain tells where to pin the tasks. For
example "**socket**" will pin the tasks on different sockets. To map the
OpenMP threads the affinity setting for OpenMP will be used.

<font color=teal>**NOTE:** the above syntax is just one way to describe
the pinning. Please visit the [Process
Pinning](https://software.intel.com/en-us/node/528816) documentation or
the Intel MPI reference (see [ Further Information
](/kb3/Software/Intel-Cluster-Suite/MPI/SW@MPI/#further-information "wikilink") section for link) for
alternative ways to pin tasks using the **I\_MPI\_PIN\_DOMAIN**
environmental variable.</font>

#### Examples

In this section are various examples for compiling and running MPI
programs with the Intel toolchain.

**Example 1:** Compile MPI program written in C, and name it
mpi\_prog.x. Use the underlying Intel compiler with -O3 optimization

`[ netID@cluster ~]$ `**`mpiicc   -o   `*`mpi_prog.x`*`   -O3 
 `*`mpi_prog.c`***

**Example 2:** Same as Example 1, but this time use underlying gnu
Fortran compiler.

`[ netID@cluster ~]$ `**`mpif90   -o   `*`mpi_prog.x 
 mpi_prog.f90`***` `

**Example 3:** Run mpi program on local host using 4 tasks

`[ netID@cluster ~]$ `**`mpirun   -np   `*`4 
 mpi_prog.x`***` `

**Example 4:** Run mpi program on a specific host, using 4 tasks

`[ netID@cluster ~]$ `**`mpirun   -np   `*`4`*`   -hosts 
 `*`login1   mpi_prog.x`***` `

**Example 5:** Run mpi program on two different hosts, using 4 tasks
using host file, assign tasks in round robin fashion

`[ netID@cluster ~]$ `**`mpirun   -np   `*`4`*`   -perhost 
 `*`1`*`   -hostfile   `*`mylist   mpi_prog.x`***` `

where *mylist* is a file that contains the following lines:

`login1`  
`login2`

<font color=teal>**Note:** If you don't specify *-pernode* all the tasks
will be started on *login1*, even though the hostfile contains multiple
entries.</font>  
**Example 6:** Run 4 different programs concurrently using mpirun (MPMD
style program)

`[ netID@cluster ~]$` **`mpirun -np `*`1   prog1.x`*` : -np `*`1 
 prog2.x`*` : -np `*`1   prog3.x`*` : -np `*`1 
 prog4.x`***

<font color=teal>**Note:** For executing a large number of serial (or OpenMP) programs we recommend using the [tamulauncher](/kb3/Software/tamulauncher/SW@tamulauncher/ "wikilink") utility.</font>

**Example 7:** Compile MPI fortran program named hybrid.f90 that also
contains OpenMP primitives, use underlying Intel Fortran compiler

`[ netID@cluster ~]$ `**`mpiifort   -openmp   -o 
 `*`hybrid.x   hybrid.f90`***

**Example 8:** Run the hybrid program named hybrid.x, use 8 tasks and
every task will use 2 threads in its OpenMP regions.

`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`2`***  
`[ netID@cluster ~]$ `**`mpirun   -np   `*`8   ./hybrid.x`***

**Example 9:** run hybrid mpi/OpenMP program using 2 tasks and 10
threads, pin the tasks to different sockets, map all OpenMP threads
within the socket

`[ netID@cluster ~]$ `**`export   I_MPI_PIN_DOMAIN=`*`socket`***  
`[ netID@cluster ~]$ `**`export   OMP_NUM_THREADS=`*`10`***  
`[ netID@cluster ~]$ `**`export   OMP_PLACES=`*`"socket"`***  
`[ netID@cluster ~]$ `**`export   OMP_PROC_BIND=`*`"master"`***  
`[ netID@cluster ~]$ `**`mpirun   -np   `*`2   ./hybrid.x`***

#### Further Information

For a detailed description of the Intel MPI stack, please visit the
[Intel MPI Developer Reference
Manual](https://software.intel.com/en-us/mpi-developer-reference-linux).
This site contains detailed information about the mpi compiler wrappers,
in depth discussion about mpirun and it options, as well as tuning your
application for best performance and pinning tasks.

### OpenMPI

Using OpenMPI is very similar to using Intel MPI. There are a few minor
differences. To use OpenMPI you will need to load one of the OpenMPI
modules. ADA has OpenMPI versions build with Intel compilers as well as
gnu compilers. The underlying compiler depends on the loaded OpenMPI
module

**Example 1:** Load OpenMPI version 1.8.4 with gnu as underlying
compiler

`[ netID@cluster ~]$ `**`module   load 
 OpenMPI/1.8.4-GCC-4.9.2`**

To see a list of all available OpenMPI versions type:

`[ netID@cluster ~]$ `**`module   spider   openmpi`**

#### Compiling

The table below shows the various mpi compiler wrappers. The names will
be the same regardless of the underlying compiler.

| MPI wrapper | Language | Example                          |
| ----------- | -------- | -------------------------------- |
| mpicc       | C        | mpicc <compiler_flags\> prog.c    |
| mpic++      | C++      | mpic++ <compiler_flags\> prog.cpp |
| mpif90      | Fortran  | mpif90 <compiler_flags\> prog.f90 |

to see the complete compiler command use the **-show** flag.

#### Running

To launch a mpi program you will use the **mpirun** command. This
command is very similar to the Intel MPI **mpirun** launcher discussed
above. However, some of the flags are different for OpenMPI. The table
below shows some of the more common flags.

| Flag               | Description|
| ------------------ | ------------------ |
| \-np <n\>           | The number of mpi tasks to start.                                                                |
| \-npernode <n\>     | Places <n\> (MPI) processes per node on each allocated node.                                      |
| \-npersocket <n\>   | Places <n\> (MPI) processes per socket on each allocated node                                     |
| \-hostfile <file\>  | The name of the file that contains the list of host/node names the launcher will place tasks on. |
| \-host {host list} | comma separated list of specific host/node names.                                                |

To see all the available options and flags (including short
descriptions) use the following command:

`[ netID@cluster ~]$ `**`mpirun   -help`**

## CUDA Programming

### Access

In order to compile, run, and debug CUDA programs, a CUDA module must be
loaded:

`[ netID@terra3 ~]$ `**`module   load   CUDA/8.0.44`**

<font color=teal>For more information on the modules system, please see
our [ Modules System](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.</font>

### Compiling CUDA C/C++ with NVIDIA nvcc

The compiler **nvcc** is the NVIDIA CUDA C/C++ compiler. The command
line for invoking it is:

`[ netID@terra3 ~]$ `**`nvcc   `*`[options]`*`   -o 
 `*`cuda_prog.exe   file1   file2   ...`***

where file1, file2, ... are any appropriate source, assembly, object,
object library, or other (linkable) files that are linked to generate
the executable file cuda\_prog.exe.

The CUDA devices on Terra are dual-GPU K80s. K80 GPUs are compute
capability 3.7 devices. When compiling your code, you need to specify:

`[ netID@terra3 ~]$ `**`nvcc   -arch=compute_37   -code=sm_37 
 ...`**

By default, nvcc will use gcc to compile your source code. However, it
is better to use the Intel compiler by adding the flag **-ccbin=icc** to
your compile command.

<font color=teal>For more information on **nvcc**, please refer to the
[online
manual](http://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc).</font>

### Running CUDA Programs

Only <font color=red>**one login node**</font> (terra3) on Terra is
installed with one dual-GPU K80. To find out load information of the
device, please run the NVIDIA system management interface program
**nvidia-smi**. This command will tell you on which GPU device your code
is running on, how much memory is used on the device, and the GPU
utilization.

    [ netID@terra3 ~]$ nvidia-smi  
    Fri Feb 10 11:44:30 2017     
    +-----------------------------------------------------------------------------+  
    | NVIDIA-SMI 367.48                 Driver Version: 367.48                    |  
    |-------------------------------+----------------------+----------------------+  
    | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |  
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |  
    |===============================+======================+======================|  
    |   0  Tesla K80           On   | 0000:83:00.0     Off |                  Off |  
    | N/A   27C    P8    26W / 149W |      0MiB / 12205MiB |      0%      Default |  
    +-------------------------------+----------------------+----------------------+  
    |   1  Tesla K80           On   | 0000:84:00.0     Off |                  Off |  
    | N/A   32C    P8    29W / 149W |      0MiB / 12205MiB |      0%      Default |  
    +-------------------------------+----------------------+----------------------+  
                                                                                     
    +-----------------------------------------------------------------------------+  
    | Processes:                                                       GPU Memory |  
    |  GPU       PID  Type  Process name                               Usage      |  
    |=============================================================================|  
    |  No running processes found                                                 |  
    +-----------------------------------------------------------------------------+

You can test your CUDA program on the login node **as long as you abide
by the rules stated in [Computing
Environment](/kb3/User-Guides/Terra/Terra@Computing_Environment/ "wikilink")**. For production
runs, you should submit a batch job to run your code on the compute
nodes. Terra has 48 compute nodes each with one dual-GPU K80 and 128GB
(host) memory. In order to be placed on GPU nodes with available GPUs, a
job needs to request them with the following two lines in a job file.

`#SBATCH --gres=gpu:1                 #Request 1 GPU`  
`#SBATCH --partition=gpu              #Request the GPU partition/queue`

### Debugging CUDA Programs

CUDA programs must be compiled with "-g -G" to force O0 optimization and
to generate code with debugging information. To generate debugging code
for K80, compile and link the code with the following:

`[ netID@terra3 ~]$ `**`nvcc   -g   -G   arch=compute_37 
 -code=sm_37   cuda_prog.cu   -o   `*`cuda_prog.out`***

<font color=teal>For more information on **cuda-gdb**, please refer to
its [online manual](http://docs.nvidia.com/cuda/cuda-gdb).</font>

## Misc

### GNU gcc and Intel C/C++ Interoperability

C++ compilers are interoperable if they can link object files and
libraries generated by one compiler with object files and libraries
generated by the second compiler, and the resulting executable runs
successfully. Some GNU gcc\* versions are not interoperable, some
versions are interoperable. By default, the Intel compiler will generate
code that is interoperable with the version of gcc it finds on your
system.

The Intel(R) C++ Compiler options that affect GNU gcc\* interoperability
include:

  - \-cxxlib
  - \-gcc-name
  - \-gcc-version
  - \-gxx-name
  - \-fabi-version
  - \-no-gcc (see gcc Predefined Macros for more information)

The Intel(R) C++ Compiler is interoperable with GNU gcc\* compiler
versions greater than or equal to 3.2. See the Intel(R) C++ Compiler
Documentation for more information at the [Intel Software
Documentation](https://software.intel.com/en-us/intel-software-technical-documentation)
page.
