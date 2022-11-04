# Numerical Libraries

### MKL

The Intel Math Kernel Library (MKL) is a library of optimized and
threaded math routines such as BLAS, LAPACK, sparse solvers, fast
fourier transforms, vector math, and more for all the latest Intel
architectures. This page will show you how to use MKL on terra, with
examples to demonstrate its common use.

#### Environment

Before using the MKL library, you need to load the MKL module file:

    module load imkl/2017.1.132-iompi-2017A

This command loads the default MKL library and all the modules that
**imkl** depends on or is associated with, including **icc**, **ifort**,
and **impi**. It sets the $MKLROOT environment variable that will be
used in our examples.

The Intel MKL library can be used by various compilers, including the
Intel compilers, the GNU compilers, and the PGI compilers. However, the
options required by each brand of compilers are different. Our
discussion below is based on the Intel compilers.

#### How To Link

Linking to the MKL library can be much involved if all possible usage
senarios are considered. In this user guide, we focus only on dynamic
linking using the -mkl compiler option, with consideration of the
commonly used BLAS95/LAPACK95 static libraries.

General forms of linking to the MKL library using the -mkl flag, with
options of linking to the MKL BLAS95/LAPACK95 Fortran libraries, are as
follows:

    ifort myprog.f   -mkl[=lib] [options] [-lmkl_blas95_lp64] [-lmkl_lapack95_lp64] ...
    icc   myprog.c   -mkl[=lib] [options] ...
    icpc  myprog.cpp -mkl[=lib] [options] ...

The flag **-mkl\[=lib\]** tells the compiler to link to certain parts of
MKL, where **lib** can be one of three values shown in the table.

<table>
<thead>
<tr class="header">
<th><p>Value</p></th>
<th><p>Meaning</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>parallel</p></td>
<td><p>Tells the compiler to link using the threaded part of MKL. This is the default if the option is specified with no lib.(<strong>-mkl=parallel</strong> is equivalent to <strong>-mkl</strong>)<br />
The threaded part of MKL includes multithreaded BLAS, LAPACK, FFT, etc. The environment variable <strong>OMP_NUM_THREADS</strong> must be set to control the number of threads at run time for the threaded MKL library.</p></td>
</tr>
<tr class="even">
<td><p>sequential</p></td>
<td><p>Tells the compiler to link using the non-threaded part of MKL, which includes sequential BLAS, LAPACK, FFT, etc.</p></td>
</tr>
<tr class="odd">
<td><p>cluster</p></td>
<td><p>Tells the compiler to link using the cluster part and the sequential part of MKL. The cluster part of MKL includes distributed FFT (DCFT), ScaLAPACK, and other sub-libraries for distributed computing. The Intel MPI library is required when -mkl=cluster.</p></td>
</tr>
</tbody>
</table>

Dynamic linking is the preferred way of linking to the MKL library. In
most cases, the **-mkl** flag provides all that you need.

**Example 1** Link to the sequential part of MKL.

    ifort example.f -mkl=sequential -o example.exe

**Example 2** Link to the threaded part of MKL.

    icc example.c -mkl=parallel -o example.exe

**Example 3** Link to the cluster part of MKL, being it DCFT or
ScaLAPACK. For this to compile, you must load the intel/mpi module
first.

    mpiifort example.f -mkl=cluster -o example.exe

When **-mkl=cluster** is used, the non-cluster part of MKL linked will
be sequential. If we want to use the cluster part of MKL and the
threaded part of MKL at the same time, we have to link each and every
library explicitly.

**Example 4** Link to ScaLAPACK and the threaded part of MKL.

    mpiicpc example.cpp -openmp -I${MKLROOT}/composrxe/mkl/include  \
    -L$(MKLROOT}/composerxe/mkl/lib -lmkl_scalapack_lp64 -lmkl_intel_lp64 \
    -lmkl_intel_thread -lmkl_core -lmkl_blacs_intelmpi_lp64 -lpthread -o example.exe

#### Link with BLAS95/LAPACK95

Dynamic linking to the right part of the MKL library has been made easy
with the **-mkl** flag. However, not all commonly used libraries are
shared libraries and hence cannot be linked dynamically. More
specifically, the MKL BLAS Fortran95 and LAPACK Fortran 95 libraries are
static and have no dynamic counterparts. These libraries must be stated
explicitly at the command line for linking. Again, the **-mkl** flag can
work with the BLAS95/LAPACK95 libraries to make things much easier.

**Example 5** Link to the sequential part of MKL and BLAS95.

    ifort example.f -mkl=sequential -lmkl_blas95_lp64 -o example.exe

**Example 6** Link to the threaded part of MKL and LAPACK95.

    ifort example.f -mkl -lmkl_lapack95_lp64 -o example.exe

Linking a code with a static library must place the code before the
static library to allow symbols from the static library referenced in
the code to be resolved correctly, as shown in the examples above. To
allow arbitrary orders between the library and the source code, we can
use **-Wl,--start-group archives -Wl,--end-group**. The flag **-Wl**
tells the compiler to pass the linker option following the comma to the
linker. **--start-group** and **--end-group** are linker options to
enclose the archives in between (can be libraries, source codes, and
object files) as a group, and these files will be searched repeatedly
until no new undefined references are created.

**Example 7** Link to the threaded part of MKL and LAPACK95 in arbitrary
order. Notice that the source file is placed after the static library.

    ifort -mkl -Wl,--start-group -lmkl_lapack95_lp64 example.f -Wl,--end-group -o example.exe 

#### ScaLAPACK

The MKL library implemens routines from the ScaLAPACK package for
distributed-memory architectures. ScaLAPACK solves dense and banded
linear systems, least square problems, eigenvalue problems, and singular
value problems. It is built on top of BLAS, LAPACK, and BLACS (Basic
Linear Algebra Communication Subprograms). The latter includes a set of
routines that support a linear algebra oriented messages passing
interface for a large range of distributed memory platforms. Except a
few supporting utility routines that are implemented in C, majority of
ScaLAPACK routines are implemented in Fortran 77.

Before calling a ScaLAPACK routine, the processor grid has to be set up
by the programmer and all global matrices must be distributed manually
on the process grid. In ScaLAPACK, block cyclic distribution is used for
dense matrices and block distribution is used for banded matrices.

In general, four basic steps are required to call a ScaLAPACK routine.

1.  Initialize the process grid  
2.  Distribute the matrix on the process grid  
3.  Call ScaLAPACK routine  
4.  Release the process grid

A pseudo program that calls a ScaLAPACK dense linear solver (pdgesv) is
shown as follow:

    ! Step 1: nitialize the process grid working environment
    
      call blacs_pinfo
      call blacs_setup
      call blacs_gridinit
      call balcs_gridinfo
    
    ! Step 2: distribute the data if they are not in place on each process
    
      if (i am the root process) then
          ! send data to each non-root process
          do i=0, np-1
            if (i.NE.root) call dgesd2d   
      else
          call dgerv2d   ! non-root process receives data
      endif
      call descinit      ! create descriptors about the global matrix 
    
    ! Step 3: call the scalapack routine
    
      call pdgesv
    
    ! Step 4: release the process grid.
    
      call blacs_gridexit
      call blacs_exit

Complete sample programs in Fortran 90 and C can be downloaded from
here:
[mypdgesvdriver.f90](https://hprc.tamu.edu/files/mypdgesvdriver.f90) and
[mypdgesvdriver.c](https://hprc.tamu.edu/files/mypdgesvdriver.c). These
programs have been tested on Eos with the Intel compilers and the Intel
MPI library.

    [login1]$ mpiifort -mkl=cluster mypdgesvdriver.f90 -o mypdgesvdriver_f.exe
    [login1]$ mpiicc -mkl=cluster mypdgesvdirver.c -o mypdgesvdriver_c.exe
    [login1]$ mpirun -np 6 ./mypdgesvdriver_c.exe
    0.00000000 -0.16666667 -0.50000000 0.16666667 
    0.50000000 0.00000000 0.00000000 
    0.00000000 0.00000000 

#### FFTW wrappers

(needs documentation)

#### Automatic Offloading

MKL provides automatic offloading to a PHI co processor for some of its
compute intensive routines. Offloading is done in a completely
transparent manner and requires no change to the code or use of special
compilation flags.The table below shows the environmental variables MKL
provides to guide automatic offloading

| Env var                     | Description                                                                                                                      |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| MKL\_MIC\_ENABLE            | Enables automatic offloading; 0 (disabled), 1 (enabled)                                                                          |
| OFFLOAD\_DEVICES            | Specifies list of PHI co processors to use. If not set, default is to use all available PHI processors                           |
| MKL\_HOST\_WORKDIVISION     | Specifies what fraction of work should be done on host; value between 0 and 1.0                                                  |
| MKL\_MIC\_WORKDIVISION      | Specifies what fraction of work should be done on all PHI co processors within the node; value between 0 and 1.                  |
| MKL\_MIC\_<N>\_WORKDIVISION | Specifies what fraction of work should be done on PHI co processors with id N; value between 0 and 1.                            |
| MKL\_MIC\_MAX\_MEMORY       | Specifies the maximum memory that can be used on all PHI co processors within the node.                                          |
| MKL\_MIC\_<N>\_MAX\_MEMORY  | Specifies the maximum memory that can be used on PHI co processors with id N.                                                    |
| OFFLOAD\_REPORT             | Specifies the profiling report level for Automatic Offload; values \[0..2\], where 0 is no report and 2 is most detailed report. |

The most important environmental variable from the table above is
**MKL\_MIC\_ENABLE** . If this variable is not set, MKL will not offload
any computation.

To specify the number of threads use the environmental variable
**MKL\_NUM\_THREADS** or **MIC\_MKL\_NUM\_THREADS** (assuming **MIC** is
the prefix used with **MIC\_ENV\_PREFIX** environmental variable). It is
recommended to use **MIC\_MKL\_NUM\_THREADS** to distinguish number of
threads on host and PHI.

**NOTE:** Every PHI co processor has 60 cores and every core has 4
hardware threads. Therefore, in general the recommended value for
**MIC\_MKL\_NUM\_THREADS** is 240

**Example 1:** Enable Automatic offloading, and set the number of
threads to 240

    [login8]$ export MKL_MIC_ENABLE=1
    [login8]$ export MIC_MKL_NUM_THREADS=240 

**Example 2:** Set the fraction of work to offload to the PHI to 0.7.
Use 240 Threads on the PHI and 16 threads on the host.

    [login8]$ export MKL_MIC_ENABLE=1
    [login8]$ export MKL_MIC_WORKDIVISION=0.7
    [login8]$ export MKL_HOST_WORKDIVISION=0.3
    [login8]$ export MIC_MKL_NUM_THREADS=240 
    [login8]$ export MKL_NUM_THREADS=16

#### Further Information

Our examples show some basic use of compiling and linking the MKL
library with the Intel compilers and how to do automatic offloading. For
other usage, such as static linking, Single Dynamic Library, linking
with MPICH2, compiling with the GNU compilers, compiling with the PGI
compilers, please check with the [Intel MKL Linking
Advisor](http://software.intel.com/en-us/articles/intel-mkl-link-line-advisor).

We also show an example (in C and Fortran) on how to program with
ScaLAPACK, a distributed linear algebra package provided in MKL. For
more examples on how to program with MKL routines, please see files in
$MKLROOT/composrxe/mkl/examples on Grace. To get the complete source
files, copy the \*.tgz file to your scratch and untar them with `tar
xzvf *.tgz`

For a complete reference of MKL, check the [Intel MKL Reference
Manual](http://software.intel.com/en-us/mkl_11.1_ref).

## Using Knitro

As mentioned, Knitro has bindings for MATLAB, R, Python, C/C++, and
Fortran. To use Knitro with any of these, you need to load the
appropriate module (e.g. Matlab, R) in addition to the Knitro module

### MATLAB

To use Knitro with MATLAB, load both modules first:

    module load Knitro/12.4
    module load Matlab

Loading the Knitro module will set the **$MATLABPATH** to the directory
containing the Knitro mex files and interfaces. After loading the
modules you can call the Knitro solver like any regular MATLAB function.
The $MATLABROOT directory also contains a sample Knitro options file and
example MATLAB scripts that use the Knitro solver.

### R

To use Knitro with R, load both modules first:

    module load Knitro/12.4
    module load R

**NOTE:** Instead of loading the default **R** module it's recommended
to load a version specific R version (e.g.
R/3.3.2-iomkl-2017A-Python-2.7.12-default-mt). Alternatively, you can
also load the R\_tamu module. Knitro will work with any R or R\_tamu
version.

The Knitro module will append the Knitro package directory to the R
environmental variable **$R\_LIBS\_USER**. Loading the Knitro package
can be done using the R **library()** function

``` 
   > library('KnitroR')
```

For some example R scripts that use the Knitro solver, see directory
**${KNITROEXAMPLES}/R**

### Python

To use Knitro with Python, load both modules first:

    module load Knitro/12.4
    module load Python/3.5.2-intel-2017A

**NOTE:** The Python version used above is just an example. Knitro will
work with any Python version (2.7.xx as well as 3.xx) and toolchain
combination.

The Knitro module will set the environmental variable **PYTHONPATH** to
include the Knitro Python directory. The Knitro solver can be accessed
from any Python script. For some example Python scripts that use the
Knitro solver, see directory **${KNITROEXAMPLES}/Python**

### C/C++ and Fortran

To use Knitro inside your own C/C++, or Fortran code, load Knitro and
the preferred toolchain first:

    module load Knitro/12.4
    module load intel/2020b

**NOTE:** The toolchain used above is just an example. Knitro will work
with any toolchain (e.g. Intel, GNU).

The Knitro module will set the environmental variables **CPATH** for the
include files, **LIBRARY\_PATH** for the compile time library paths, and
**LD\_LIBRARY\_PATH** for the runtime library paths.

Directories **${KNITROEXAMPLES}/C**, **${KNITROEXAMPLES}/C++**, and
**${KNITROEXAMPLES}/Fortran** contain example programs for C,C++, and
Fortran respectively. The directories also contain a Makefile,
explaining how to compile the examples.
