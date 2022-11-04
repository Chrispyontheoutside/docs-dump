# NAMD

## Description

NAMD is a fast, parallel, and scalable molecular dynamics program
designed for high-performance simulation of large biomolecular systems.
NAMD is distributed free of charge with source code. It is developed in
conjunction with VMD. It is also file-compatible with AMBER, CHARMM, and
X-PLOR.  
Homepage: [NAMD](https://www.ks.uiuc.edu/Research/namd/)

## Access

### Loading the Module

There are a variety of NAMD modules supported on Ada and Terra. For more
information, see our [ modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.  
  
Make sure you have a clean environment before getting started:

` [ netID@cluster ~]$ `**`ml   purge`**

To see all versions of NAMD available on Ada or Terra:

` [ netID@cluster ~]$ `**`ml   spider   NAMD`**

To load a particular version of NAMD on Ada or Terra:

` [ netID@cluster ~]$ `**`ml   NAMD/2.14-intel-2020a-mpi`**

<font color="purple">NOTE: Pay close attention to the information
following the version number of the module. This is called the [
toolchain](/kb3/Software/useful-tools/SW@Toolchains/ "wikilink"). This information describes what
other modules will be loaded with NAMD. These modules will be disrupted
by use of extraneous modules of different toolchains, so please purge
all unnecessary modules prior to using NAMD.</font>
