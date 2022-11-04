# Python

Python is an interpreted high-level programming language for
general-purpose programming. Python has had many versions over the
years. Most python programs run on Python 2 (example - 2.7.x) or Python
3 (example - 3.6.x).

### Modules and Versions

To check the available Python modules on a cluster please type the
following command:

`  [NetID@cluster NetID]$ module spider Python`

This will show the versions of python complied with different
toolchains. The first part of the module name, Python/3.6.6 for example,
refers to the python language version. The second part of the module
name, -intel-2018b for example, refers to the HPRC toolchain used to
compile the module.

       Python/3.6.6-foss-2018b
       Python/3.6.6-fosscuda-2018b
       Python/3.6.6-giolf-2018b
       Python/3.6.6-intel-2018b
       Python/3.6.6-iomkl-2018b
       Python/3.7.0-foss-2018b
       Python/3.7.0-intel-2018b
       Python/3.7.0-iomkl-2018b
       Python/3.7.2-GCCcore-8.2.0
       Python/3.7.4-GCCcore-8.3.0

### What is a toolchain?

A **toolchain** on a TAMU HPRC cluster is a collection of tools used for
building software. They typically include:

  - a compiler collection providing basic language support
    (C/Fortran/C++)
  - a MPI implementation for multi-node communication
  - a set of linear algebra libraries (FFTW/BLAS/LAPACK) for accelerated
    math

For more information on toolchains checkout our [ Toolchains
](/kb3/Software/useful-tools/SW@Toolchains/ "wikilink") page.

### Which Python to use?

If your project requires a specific version of python language (Ex.
2.7.15) with specific compiler, then use that particular version. We
recommend using the most recent toolchain (intel-2018b) with your python
version. Once you decide your version, please continue to do your work
on the same version. Changing versions can cause errors. In short,
current recommended version for python 2 language

`  Python/2.7.15-intel-2018b`

Current recommended version for python 3 language

`  Python/3.6.6-intel-2018b`

### Loading/Unloading Python

You can use "module load" command for loading a particular python
version on cluster. An example command for loading python 3:

`  [NetID@cluster NetID]$ module load Python/3.6.6-intel-2018b`

You can use the following example command for unloading python 3:

`  [NetID@cluster NetID]$ module purge `

Write the following command, if you want to check the python language
version that you are currently using.

`  [NetID@cluster NetID]$ python --version`

### Default Python Packages (pip)

Python is useful if it has many packages. The "pip list" command will
show the default python packages available.

`  [NetID@cluster NetID]$ pip list`

**<span style="color:red;"> NOTE: Users don't have permission to install
new packages using "pip install" command directly on the terminal. Users
need to create a virtual environment for that purpose.</span>**

### How to install new packages (pip install) ?

Users first need to create a private virtual environment and install
packages in that environment, only need to create virtual environment
and pip install packages **once**.

#### Create a virtual environment

Users should create virtual environment inside "scratch" and preferably
inside their project directory. The next few commands show how to create
a virtual environment inside a new project directory. We recommend
enabling system-site-packages so that any other modules you load will
continue to function.

    [NetID@cluster NetID]$ module load Python/3.6.6-intel-2018b   # Load Python module
    [NetID@cluster NetID]$ cd $SCRATCH                            # Go to scratch directory
    [NetID@cluster NetID]$ mkdir python_project                   # Make a new directory named python_project
    [NetID@cluster NetID]$ cd python_project                      # Go to the project directory
    [NetID@cluster python_project]$ virtualenv --system-site-packages venv               # Make a virtual environment "venv"

#### Activate/Deactivate virtual environment

This section shows how to activate and deactivate the virtual
environment. You have to give path from your project directory

    [NetID@cluster NetID]$ module load Python/3.6.6-intel-2018b         # Load Python module
    [NetID@cluster NetID]$ cd $SCRATCH/python_project                   # Go to the project directory
    [NetID@cluster python_project]$ source venv/bin/activate            # Activate virtual environment (Command line should show environment name on left)
    (venv) [NetID@cluster python_project]$ pip list                     # Check the packages in environment
    (venv) [NetID@cluster python_project]$ python --version             # Check the python version in environment
    (venv) [NetID@cluster python_project]$ deactivate                   # Deactivate virtual environment
    [NetID@cluster python_project]$                                     # Command line returns to normal

#### Install/Uninstall packages in virtual environment

To install packages, we first have to load python module and activate
our environment. The next few commands show installation/uninstallation
of the numpy package using "pip install" command.

    [NetID@cluster NetID]$ module load Python/3.6.6-intel-2018b         # Load Python module
    [NetID@cluster NetID]$ cd $SCRATCH/python_project                   # Go to the project directory
    [NetID@cluster python_project]$ source venv/bin/activate            # Activate virtual environment 
    (venv) [NetID@cluster python_project]$ pip install numpy            # Install numpy package
    (venv) [NetID@cluster python_project]$ pip list                     # Check the packages in environment
    (venv) [NetID@cluster python_project]$ pip uninstall numpy          # Uninstall numpy package
    (venv) [NetID@cluster python_project]$ deactivate                   # Deactivate virtual environment

#### Remove a virtual environment

You can delete the environment folder using "rm -r venv" command. Answer
with "y" if there are questions about write protected files.

### How to install an environment using Anaconda

See our [Anaconda](/kb3/Software/ANACONDA/SW@Anaconda/ "wikilink") wiki page for details on
creating an environment using Anaconda which is also used for Jupyter
Notebook and JupyterLab on the HPRC portal.

### Other topics

Parallelize with [ Scoop](/kb3/Software/Python/SW@Python@Scoop/ "wikilink")
