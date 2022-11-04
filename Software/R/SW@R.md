# R

## Description

R is a free software environment for statistical computing and
graphics.  
Homepage: <http://www.r-project.org/>

## Access

R is open to all HPRC users.

### Loading the Module

To see all versions of R available:

`[NetID@cluster ~]$ `**`module   spider   R`**

To load a particular version of R (Example: 3.4.2 with the iomkl
toolchain):

`[NetID@cluster ~]$ `**`module   load 
 R/3.4.2-iomkl-2017A-Python-2.7.12-default-mt`**

### R\_tamu

Loading the R module will setup the environment for the base R
installation without any additional packages. For the user's
convenience, HPRC developed an extension to R called **R\_tamu** which
is built on top of R and provides a large number of additionally
installed packages not found in the base R version. R\_tamu also makes
it easy to install personal packages. In addition, R\_tamu can also act
as an R-project environment manager.

To see all versions of the R\_tamu available:

`[NetID@cluster ~]$ `**`module   spider   R_tamu`**

For more information about R\_tamu, please visit the [ R\_tamu Wiki
page](/kb3/Software/R-tamu/SW@R_tamu/ "wikilink")

### Installing Packages

While there are many packages available with the **R\_tamu** module, you
may find that we do not have a package installed that is needed. If you
think that a particular package might be useful for other R users, you
can [contact us](https://hprc.tamu.edu/about/contact.html) with a
request to install this packages systemwide. Alternatively, you can
install any packages yourself in your own directory.

The most common way to install a package is to start an interactive R
session and use the R function

`> `**`install.packages("`*`package_name`*`")`**

Alternatively, you can also use **R CMD INSTALL** command from the
shell. This is useful when you already have a local copy of the R
package ( \*.tar.gz format).

R\_tamu sets the R environment variable **R\_LIBS\_USER** to
${SCRATCH}/R\_LIBS/<VERSION> ( where <VERSION> is currently loaded R
version), so all packages will be automatically installed in that
directory.

In case you are using the R module, you will be asked to provide a
personal directory where to install it. The easiest way is to set
**R\_LIBS\_USER** before you start your R session. For example:

`  [NetID@cluster ~]$ export R_LIBS_USER=${SCRATCH}/myRlibs`

**NOTE:** In case you are using the R module, to be able to use the
installed packages, R\_LIBS\_USER needs to be set every time before
starting an R Session.

<font color=teal> If you have trouble installing packages for yourself,
you can also [contact us](https://hprc.tamu.edu/about/contact.html) with
any concerns. </font>

  

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

'

### Slurm Example (terra)

**Example 1:** A serial (single core) R Job example: (Last updated March
24, 2017)

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=R_Job        # Sets the job name to R_Job
    #SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
    #SBATCH --ntasks=1              # Requests 1 core
    #SBATCH --ntasks-per-node=1     # Requests 1 core per node (1 node)
    #SBATCH --mem=5G                # Requests 5GB of memory per node
    #SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

    ## Load the necessary modules
    module purge
    module load R_tamu/3.3.2-iomkl-2017A-Python-2.7.12-default-mt

    ## Launch R with proper parameters 
    Rscript myScript.R

**Example 2:** A parallel (multiple core) R Job example, where
*myScript.R* is a script that requests 10 slaves. (Last updated March
24, 2017)  
**Note:** The number of cores requested should match the number of
slaves requested.

    #!/bin/bash

    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=R_Job        # Sets the job name to R_Job
    #SBATCH --time=5:00:00          # Sets the runtime limit to 5 hr
    #SBATCH --ntasks=10             # Requests 10 cores
    #SBATCH --ntasks-per-node=10    # Requests 10 cores per node (1 node)
    #SBATCH --mem=50G               # Requests 50GB of memory per node
    #SBATCH --output=stdout1.o%J    # Sends stdout and stderr to stdout1.o[jobID]

    ## Load the necessary modules
    module purge
    module load R_tamu/3.3.2-iomkl-2017A-Python-2.7.12-default-mt

    ## Launch R with proper parameters 
    mpirun -np 1 Rscript myScript.R

To submit the batch job, run: (where *jobscript* is a file that looks
like one of the above examples)

`[ NetID@terra ~]$ `**`sbatch   `*`jobscript`***

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.
