# Software

We currently have many commercial and freeware (foss, free and open
source software) packages installed on our supercomputers. Online
documentation and links to the vendor's website are available to TAMU
computers and to computers using TAMU's
[VPN](https://u.tamu.edu/KB0010938). Requests to use restricted software
should be emailed to the [HPRC
helpdesk](https://hprc.tamu.edu/user_services/consulting.html). Please
also consult our [Software Policy
page](https://hprc.tamu.edu/policies/software.html) for more information
about acquiring and using restricted (EAR and ITAR) and licensed
software on our clusters.

## Finding Software

On our clusters, the software is available through the [ module
system](/kb3/Software/useful-tools/SW@Modules/ "wikilink"). Available software can be queried with:

  - **module avail**

or

  - **module spider**

or

  - **fml**

fml command is a fast alternative to module spider. However, for the
most up-to-date module information, please use *module spider*

To search for available Python module,

fml Python

To query information about a particular module

fml Python/3.8.2-GCCcore-9.3.0

A complete module listing for each cluster can be found here:

  - [FASTER Module List](https://hprc.tamu.edu/software/faster/)
  - [Grace Module List](https://hprc.tamu.edu/software/grace/)
  - [Terra Module List](https://hprc.tamu.edu/software/terra/)

On our Linux workstations, a list of available packages can be queried
with:

  - rpm -qa | sort 

## Temporary Files and Using the *Home* Directory

Many software packages create and manipulate temporary files during the
execution of the program. These temporary files are commonly placed
within your *Home* directory by default. You must remain aware of how
much quota space is left within your *Home* directory at all times. If
your *Home* directory is filled, attempts to write or modify temporary
files will fail.

<font color="red" size="4">This may cause your jobs to **terminate** (be
killed) or **hang** (do nothing, waste SUs). </font>

The easiest way to avoid this issue is to store your files within your
*Scratch* directory. Use **cd $SCRATCH** to navigate to your Scratch
directory.

**showquota** will allow you to view your quota limits.

## Available Packages and Software Collections

We maintain a number of pages documenting the use of some of the
available software packages, including:


  - [ ABAQUS](/kb3/Software/ABAQUS/SW@ABAQUS/ "wikilink")
  - [ AlphaFold](/kb3/Software/AlphaFold/SW@AlphaFold/ "wikilink")
  - Altair
      - [ Hyperworks](/kb3/Software/Altair/Hyperworks/SW@Hyperworks/ "wikilink")
      - [ Optistruct](/kb3/Software/Altair/Optistruct/SW@Hyperworks@Optistruct/ "wikilink")
  - [ ANACONDA](/kb3/Software/ANACONDA/SW@Anaconda/ "wikilink")
  - [ ANSYS](/kb3/Software/ANSYS/SW@ANSYS/ "wikilink")
      - [ CFX](/kb3/Software/ANSYS/SW@ANSYS@CFX/ "wikilink")
      - [ Ensight](/kb3/Software/ANSYS/SW@ANSYS@Ensight/ "wikilink")
      - [ Fluent](/kb3/Software/ANSYS/SW@ANSYS@Fluent/ "wikilink")
      - [ ICEM CFD](/kb3/Software/ANSYS/SW@ANSYS@ICEM/ "wikilink")
      - [ TurboGrid](/kb3/Software/ANSYS/SW@ANSYS@Turbogrid/ "wikilink")
      - [ Workbench](/kb3/Software/ANSYS/SW@ANSYS@Workbench/ "wikilink")
  - [ Avogadro](/kb3/Software/Avogadro/SW@Avogadro/ "wikilink")
  - [ Bioinformatics Software Collection](/kb3/Software/Bioinformatics/Bioinformatics/ "wikilink")
  - [ Caffe](/kb3/Software/Caffe/SW@CAFFE/ "wikilink")
  - [ cctools/parrot](/kb3/Software/cctools/SW@cctools/ "wikilink") access CVMFS
  - [ Dalton](/kb3/Software/Dalton/SW@Dalton/ "wikilink")
  - [ Faster-RCNN](/kb3/Software/Faster-RCNN/SW@Faster-RCNN/ "wikilink")
  - [ Galaxy](/kb3/Software/Galaxy/SW@Galaxy/ "wikilink")
  - [ Globus Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink")
  - GNU Compiler Collection
  - [ GROMACS](/kb3/Software/GROMACS/SW@GROMACS/ "wikilink")
  - Intel Cluster Suite
      - Compilers
      - MPI
      - [ Math Kernel Library](/kb3/Software/Intel-Cluster-Suite/Math-Kernel-Library/SW@MKL/ "wikilink")
      - VTune
  - [ Julia](/kb3/Software/Julia/SW@Julia/ "wikilink")
  - [ Keras ](/kb3/Software/Keras/SW@Keras/ "wikilink")
  - [ Knitro](/kb3/Software/Knitro/SW@Knitro/ "wikilink")
  - [ LAMMPS](/kb3/Software/LAMMPS/SW@LAMMPS/ "wikilink")
  - Livermore Software Technology
      - [ LS-DYNA](/kb3/Software/Livermore-Software-Technology/ls-dyna/SW@LSDYNA/ "wikilink")
      - [ LS-OPT](/kb3/Software/Livermore-Software-Technology/ls-opt/SW@LS-OPT/ "wikilink")
      - [ LS-PREPOST](/kb3/Software/Livermore-Software-Technology/ls-prepost/SW@LS-PREPOST/ "wikilink")
  - [ Machine Learning](/kb3/Software/Machine-Learning/SW@Machine_Learning/ "wikilink")
  - [ Matlab](/kb3/Software/MATLAB/SW@Matlab/ "wikilink")
  - [ moose](/kb3/Software/moose/SW@moose/ "wikilink")
  - [ myHadoop](/kb3/Software/myHadoop/SW@myhadoop/ "wikilink")
  - [ NAMD](/kb3/Software/NAMD/SW@NAMD/ "wikilink")
  - NCAR Command Language (NCL)
  - netCDF
  - [ NWChem](/kb3/Software/NWChem/SW@NWChem/ "wikilink")
  - [ OpenFOAM](/kb3/Software/OpenFOAM/SW@OpenFOAM/ "wikilink")
  - [ pigz](/kb3/Software/pigz-(Parallel-Gzip)/SW@pigz/ "wikilink") (parallel gzip)
  - [ Portal](/kb3/Software/Portal/SW@Portal/ "wikilink")
  - [ PostgreSQL](/kb3/Software/PostgreSQL/SW@PostgreSQL/ "wikilink")
  - [ Psi4](/kb3/Software/Psi4/SW@Psi4/ "wikilink")
  - [ Python](/kb3/Software/Python/SW@Python/ "wikilink")
  - [ PyTorch](/kb3/Software/PyTorch/SW:PyTorch/ "wikilink")
  - [ QuantumESPRESSO](/kb3/Software/QuantumESPRESSO/SW@QuantumESPRESSO/ "wikilink")
  - [ R](/kb3/Software/R/SW@R/ "wikilink")
  - [ R\_tamu](/kb3/Software/R-tamu/SW@R_tamu/ "wikilink")
  - [ rclone](/kb3/Software/rclone-(Cloud-Backup)/SW@rclone/ "wikilink") (cloud backup)
  - [ RCS](/kb3/Software/rcs-(Revision-Control-System)/SW@RCS/ "wikilink") (Revision Control System)
  - SAS
  - [ Scikit\_Learn](/kb3/Software/Scikit-Learn/SW@Scikit_Learn/ "wikilink")
  - [ Singularity](/kb3/Software/Singularity/SW@Singularity/ "wikilink")
  - [ STAR-CCM+](/kb3/Software/STAR-CCM+/SW@Starccm/ "wikilink")
  - [ SWAN](/kb3/Software/SWAN/SW@SWAN/ "wikilink")
  - [ tamulauncher ](/kb3/Software/tamulauncher/SW@tamulauncher/ "wikilink")
  - [ VMD](/kb3/Software/VMD/SW@VMD/ "wikilink")
  - [ TensorFlow](/kb3/Software/TensorFlow/SW@TensorFlow/ "wikilink")
  - [ Web Proxy](/kb3/Software/Web-Proxy/SW@WebProxy/ "wikilink") (internet access from compute
    nodes)
  - [ WRF](/kb3/Software/WRF/SW@WRF/ "wikilink")
  - [ Zebulon](/kb3/Software/Zebulon/SW@Zebulon/ "wikilink")


### License-Restricted Packages

These packages are restricted by license. Individuals or groups have
purchased licenses for these packages and manage the list of users that
may access them.

**Note:** These packages are not the same as *Export-Controlled
Software*, as mentioned in the [Software
Policy](https://hprc.tamu.edu/policies/software.html).


  - [ Amber](/kb3/Software/Amber/SW@Amber/ "wikilink")
  - CHARMM
  - [ Comsol](/kb3/Software/Comsol/SW@Comsol/ "wikilink")
  - GAMS
  - [ Gaussian](/kb3/Software/gaussian/SW@Gaussian/ "wikilink")
  - [ IDL](/kb3/Software/IDL/SW@IDL/ "wikilink")
  - [ ORCA](/kb3/Software/ORCA/SW@ORCA/ "wikilink")
  - [ Schrödinger](/kb3/Software/Schrodinger/SW@Schrodinger/ "wikilink")
  - Stata
  - [ VASP](/kb3/Software/VASP/SW@VASP/ "wikilink")
  - [ Cadence](/kb3/Software/Cadence/SW@Cadence/ "wikilink")


### Toolchains for Compiling Software

Information on the available toolchains for compiling software can be
found on our [ Toolchains ](/kb3/Software/useful-tools/SW@Toolchains/ "wikilink") page.

## Useful Tools

The following is a list of the most frequently requested / needed tools
on our clusters.


  - [ dos2unix](/kb3/Software/useful-tools/SW@dos2unix/ "wikilink")
  - [ gedit](/kb3/Software/useful-tools/SW@gedit/ "wikilink")
  - [ tamulauncher](/kb3/Software/tamulauncher/SW@tamulauncher/ "wikilink")
  - [ Ada Project Allocation Tool](/kb3/User-Guides/AMS-Documentation/HPRC@AMS@UI/#ada "wikilink")
  - [ License Checker Tool](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink")
  - [ Other Useful Utilities & Tips](/kb3/Software/useful-tools/SW@Misc/ "wikilink")

