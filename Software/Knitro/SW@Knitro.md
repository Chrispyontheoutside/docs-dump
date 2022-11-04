# Knitro

## Description

The Artelys Knitro Solver is a plug-in Solver Engine that extends
Analytic Solver Platform, Risk Solver Platform, Premium Solver Platform
or Solver SDK Platform to solve nonlinear optimization problems of
virtually unlimited size. The solver has plugins for MATLAB, R, Python,
C/C++, and Fortran.

**NOTE:** Knitro is currently only available on the **terra** cluster.

For more information, please visit
<https://www.solver.com/artelys-knitro-solver-engine>

## Setting up the Knitro environment

Before using Knitro, you need to set up the environment. To do this,
load the Knitro module

`  [NetID@terra ~]$ `**`module   load   Knitro/12.4`**

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

Directories **\$\{KNITROEXAMPLES\}/C, \$\{KNITROEXAMPLES\}/C++**, and **\$\{KNITROEXAMPLES\} /Fortran** contain example programs for C,C++, and
Fortran respectively. The directories also contain a Makefile,
explaining how to compile the examples.

## Acknowledgement

The license for Knitro has been purchased by the Department of
Economics. We are thankful for their contribution and for allowing
access to all HPRC users.
