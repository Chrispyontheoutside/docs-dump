# R_tamu

R\_tamu is an extension built on top of R and provides a large number of
additionally installed packages not found in the base R version. In
addition, R\_tamu can also act as an R-project environment manager.
Loading R\_tamu will automatically load the matching R module so there
is no need to load the R module separately. HPRC will update the
installed packages regularly to make sure all packages are up-to-date
with the latest bug fixes and improvements.

### Loading the Module

To see a listing of all available R\_tamu versions:

`[NetID@cluster ~]$ `**`module   spider   R_tamu`**

To load a particular version of R\_tamu (Example: 3.4.2 with the iomkl
toolchain):

`[NetID@cluster ~]$ `**`module   load 
 R_tamu/3.4.2-iomkl-2017A-Python-2.7.12-default-mt`**

### Using R and Rscript

Using R and Rscript works exactly the same as the base R module. To
start the R interpreter and to execute an R script, see example below.

    [NetID@cluster ~]$ module load R_tamu/3.4.2-iomkl-2017A-Python-2.7.12-default-mt
    [NetID@cluster ~]$ R
    > # execute R commands
    > q()
    [NetID@cluster ~]$ Rscript myprog.R

For a more detailed introduction how to run R/Rscript on the login nodes
and through the batch system, see the [ R Wiki page](/kb3/Software/R/SW@R/ "wikilink")

## Viewing Available Packages

As mentioned, R\_tamu provides a large number of installed packages;
currently, around 300 (including bio-conductor packages). Use the R
**library()** function to see all installed packages. Alternatively,
**installed.packages()** will list all installed packages.

## Installing New Packages

In case a package is missing there are two ways to make it available:

  - Request HPRC to install package
  - Install locally in ${SCRATCH} directory

### Request Additional packages

To request installation of additional R package, send email to
help@hprc.tamu.edu and specify the package that is requested, a short
description of its use, and any relevant documentation (if any).HPRC
will install the package globally if the package might be useful to the
general public.

### Install Locally

R\_tamu automatically sets up the environment for users to install
packages locally by setting environmental variable **R\_LIBS\_USER**
(set to */scratch/$user/R\_LIBS\_USER/<RVERSION>*, where <RVERSION> is
the R version/toolchain). R\_tamu will create the $R\_LIBS\_USER
directory if needed. Use the R function **install.packages(<PKGS>)**
function (or any other approach) to install the required package. The
packages will automatically be installed locally in the $R\_LIBS\_USER
directory. **NOTE:** HPRC can provide assistance to install the package
to a user's personal directory as well.

#### Installing packages from Github

Whenever packages need to be loaded from repositories other than CRAN
(e.g. github), directly loading the packages will result in errors. This
is because packages are loaded by default in systemwide R\_LIBS which is
not writable by users. To handle this issue, set R\_LIBS to
R\_LIBS\_USER temporarily using following command:

`export R_LIBS=$SCRATCH/R_LIBS_USER/`<RVERSION>

For example, if you load **R\_tamu/4.0.3-foss-2020a-recommended-mt**,
you can use the following command before loading R packages from Github:

`export R_LIBS=$SCRATCH/R_LIBS_USER/4.0.3-foss-2020a-recommended-mt`

## R-project environments

R\_tamu can also be used as a package manager for R projects. Using
R\_tamu, R and Rscript accept an additional flag
**--rtamuenvs=<PROJECTNAME>** which sets up the environment for R to
search for packages in a specific location. It will also create the
directory structure to store the packages. This feature can be useful
when a user is working on multiple projects each requiring the use of a
certain number of R packages with specific versions. Using a project
environment will also allow for reproducibility (e.g. user can run R
simulations using the same environment again at a later time when
needed). **NOTE** the globally installed packages will still be
available, so there is no need to install every package again.

### Example

Suppose, a user is working on two different R projects (let's call them
*projectA* and *projectB*), When user is working on project A,
environment for *projectA* will be used, when user switches to project
B, environment for *projectB* will be used.

    [NetID@cluster ~]$ module load R_tamu/3.4.2-iomkl-2017A-Python-2.7.12-default-mt
    [NetID@cluster ~]$ R --rtamenvs=ProjectA
    >
    > #install packages for projectA
    > install.packages(c('mypack1.tar.gz',mypack2.tar.gz'))
    > library(mypack1)
    > # use packages
    > q()
    
    [NetID@cluster ~]$ R --rtamenvs=ProjectB
    >
    > # packages installed under projectA will not be visible
    > library(mypack1)
    Error in library(mypack1) : there is no package called ‘mypack1’
    > # install packages needed for projectB and use them
    > q()
    
    [NetID@cluster ~]$ R --rtamenvs=ProjectA
    >
    > # packages installed under projectA will be visible
    > library(mypack1)
    > # use library mypack1, mypack2, etc
    > q()
    
    [NetID@cluster ~]$ Rscript --rtamuenvs=ProjectA myAscript.R

### Notes

The **--rtamuenvs** flag can accept a list of project environments
(separated by :). For example: **R --rtamuenvs=NewProj:ProjA**. This can
be useful when working on a new project that is based on an old project
with some additional packages.
