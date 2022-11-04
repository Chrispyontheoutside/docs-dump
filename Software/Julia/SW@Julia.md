# Julia

Julia is a high-level, high-performance dynamic programming language for
technical computing, with syntax that is familiar to users of other
technical computing environments. It provides a sophisticated compiler,
distributed parallel execution, numerical accuracy, and an extensive
mathematical function library. - Homepage: [Julia
website](http://julialang.org)

## Versions available on Ada

[Software modules on Ada](https://hprc.tamu.edu/software/ada/)

    Versions:
    Julia/0.5.0-intel-2015B-Python-2.7.10
    Julia/0.6.2-intel-2017A-Python-2.7.12-ParMETIS-4.0.3
    Julia/0.6.2-intel-2017A-Python-2.7.12-METIS-5.1.0
    Julia/0.6.2-intel-2017A-Python-2.7.12-noSuiteSparse
    Julia/0.7.0-linux-x86_64
    Julia/1.0.5-linux-x86_64
    Julia/1.1.1-linux-x86_64
    Julia/1.4.1-linux-x86_64
    Julia/1.5.1-linux-x86_64 

[Software modules on Terra](https://hprc.tamu.edu/software/terra/)

    Versions:
    Julia/0.6.2-intel-2017A-Python-2.7.12-ParMETIS-4.0.3
    Julia/0.6.2-intel-2017A-Python-2.7.12-METIS-5.1.0
    Julia/0.6.2-intel-2017A-Python-2.7.12-noSuiteSparse
    Julia/1.0.5-linux-x86_64
    Julia/1.4.1-linux-x86_64
    Julia/1.5.1-linux-x86_64

## Installing the latest version of Julia

You can always download the unzip the latest Julia version from [Julia
Download Page](https://julialang.org/downloads/). The only thing to keep
in your mind is that Julia packages contain many files. It is always a
good practice to use your scratch space ($SCRACH) to install external
packages.

E.g., to install and run Julia version 1.5.3 under your scratch
directory, you just need to:

    cd $SCRATCH
    wget https://julialang-s3.julialang.org/bin/linux/x64/1.5/julia-1.5.3-linux-x86_64.tar.gz
    tar -zxvf julia-1.5.3-linux-x86_64.tar.gz
    ./julia-1.5.3/bin/julia

You can choose to add $SCRATCH/julia-1.5.3/bin to your PATH in
~/.bash\_profile or ~/.bashrc, so that you just need to type julia to
get started next time.

    export PATH=$PATH:$HOME/.local/bin:$HOME/bin:$SCRATCH/julia-1.5.3/bin

If you choose to use your own installation, you don't need to load any
modules to use Julia. However, you will need to reset your
`JULIA_DEPOT_PATH` to `$SCRATCH/.julia` before run Julia for the first
time to install Julia packages under your scratch space. Since the
default installation path (~/.julia) will quickly use up your file
quota, which could be checked with `showquota`.

     export JULIA_DEPOT_PATH=$SCRATCH/.julia

## Using Pre-installed Julia on Ada/Terra

On either Ada or Terra, a given Julia module can be loaded with the
'module load' command.

For example, to load the Julia module version Julia/1.5.1-linux-x86\_64,
use the following command:

    module load Julia/1.5.1-linux-x86_64

or simply

    ml Julia/1.5.1-linux-x86_64

To run Julia from the command line, do:

    julia

To run code non-interactively, do:

    julia script.jl arg1 arg2

## Julia Packages

### Julia 1.5.1

To add Julia packages, please make sure that `JULIA_DEPOT_PATH` has been
set to a directory under `$SCRATCH`. E.g.,

    export JULIA_DEPOT_PATH=$SCRATCH/.julia

1\. Load the Julia module

    module load   Julia/1.5.1-linux-x86_64

2\. Open the Julia REPL

    julia

you will see the julia prompt which looks like this:

    julia>

3\. Type \] to open the Pkg REPL

    ]

you will see the Pkg prompt which looks like this:

    (@v1.5) pkg> 

4\. add your package (Plots in this example will add more than 10,000
files to your $SCRATCH/.julia directory)

    (@v1.5) pkg> add Plots

5\. type backspace to return to the julia REPL from the Pkg REPL

### Julia 0.6.2

The Julia 0.6.2 package directory in the Julia\_tamu module is a shared
directory for packages. Users do not have permission to install packages
into this directory.

Julia 0.6.2 does not support multiple package install directories. Use
version 1.1.1 instead.

Julia\_tamu just loads Julia plus a compatible version of R.

To install packages into your own $SCRATCH directory, you will need to
the following:

  - Request a file quota increase for your $SCRATCH directory if needed.
      - Initializing your $SCRATCH julia package directory and
        installing a few julia packages can create 50,000+ files.

<!-- end list -->

  - Change the JULIA\_PKGDIR environment variable after loading the
    Julia module and prior to starting julia.
      - Julia does not support multiple package directories.
      - The Julia\_tamu module currently loads Julia and a compatible
        version of R which is required by some Julia packages.

On the UNIX command line type the following to load Julia\_tamu, change
the package directory and start julia before installing packages with
the Pkg.add(), bash command(replace the Julia\_tamu module name with the
one that's available):

    module load Julia_tamu/0.6.2-intel-2017A-Python-2.7.12-METIS-5.1.0
    JULIA_PKGDIR=$SCRATCH/.julia
    julia  #this will open the julia REPL
    Pkg.init()
    Pkg.add("PACKAGE_NAME")
