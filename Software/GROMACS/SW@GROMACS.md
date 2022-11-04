# GROMACS

## Description

GROMACS is a versatile package to perform molecular dynamics, i.e.
simulate the Newtonian equations of motion for systems with hundreds to
millions of particles. - Homepage: <http://www.gromacs.org>

## Access

### Loading the Module

There are a variety of GROMACS modules supported on Terra and Grace. For
more information, see our [ modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.  
**Grace Instructions:**  
To purge unnecessary modules before getting started:

`[netID@grace2]ml purge`

List the versions of GROMACS installed (as of 06/21/2021):

    [netID@grace2]mla gromacs
    GROMACS/2018.1-PLUMED
    GROMACS/2018.2
    GROMACS/2018.3
    GROMACS/2018.4-PLUMED-2.5.0
    GROMACS/2019.3
    GROMACS/2019.4
    GROMACS/2019.6
    GROMACS/2020
    GROMACS/2020.1-Python-3.8.2
    GROMACS/2020.3
    GROMACS/2020.4-Python-3.8.2

List the required module dependencies for *GROMACSversion*:

`ml spider `*`GROMACSversion`*

Finally, load *GROMACSversion* with the *dependencies* listed first to
setup your environment to run GROMACS:

`ml `*`dependencies`*` `*`GROMACSversion`*

For example, to use the cpu version:

`ml  GCC/7.3.0-2.30  OpenMPI/3.1.1 GROMACS/2018.4-PLUMED-2.5.0`

To use the GPU version:

`ml GCC/7.3.0-2.30  CUDA/9.2.88  OpenMPI/3.1.1 GROMACS/2018.4-PLUMED-2.5.0`

**Terra Instructions:**  
To purge unnecessary modules before getting started:

` [ netID@cluster ~]$ `**`module   purge`**

To see all versions of GROMACS available Terra:

` [ netID@cluster ~]$ `**`module   spider   GROMACS`**

To load a particular version of GROMACS on Terra:

` [ netID@cluster ~]$ `**`module   load 
 GROMACS/2020-foss-2019b`**

<font color="purple">NOTE: Pay close attention to the information
following the version number of the module. This is called the [
toolchain](/kb3/Software/useful-tools/SW@Toolchains/ "wikilink"). This information describes what
other modules will be loaded with GROMACS. These modules will be
disrupted by use of extraneous modules of different toolchains, so
please purge all unnecessary modules prior to using GROMACS.</font>

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use
non-interactive batch jobs for resource-intensive and/or multiple-core
processing. Users are requested to be responsible and courteous to other
users when using software on the login nodes.

The most important processing limits here are:

- ONE HOUR of PROCESSING TIME per login session.  

- EIGHT CORES per login session on the same node or (cumulatively) across all login nodes.

Anyone found violating the processing limits will have their processes
killed without warning. Repeated violation of these limits will result
in account suspension. Note: Your login session will disconnect after
one hour of inactivity.
