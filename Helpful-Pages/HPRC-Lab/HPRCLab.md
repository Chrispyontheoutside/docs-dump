# HPRC Lab

## Purpose

The HPRC group provides its users with access to several specially
configured "HPRC Lab" Linux workstations at two separate locations (see
below) on campus. The primary function of such workstations is to
provide stand-alone platforms for interactive pre- and post-processing
tasks, including visualization, that are directly related to
larger-scale computation on the clusters themselves. This manner of
handling such tasks is more convenient and effective than the direct use
of clusters for them.

## Access requirements

Access to the HPRC Lab workstations is available to any user of HPRC
clusters. We are working on automating that process, but for now if you
would like to use these systems, please [contact
us](https://hprc.tamu.edu/about/contact.html), email preferred.

## Locations and availability

Three workstations (hostname:
**hprclab1.tamu.edu**,**hprclab6.tamu.edu**,**hprclab7.tamu.edu**) have
been installed at the [Student Computing
Center](http://oal.tamu.edu/Lab-Locations#0-StudentComputingCenter(SCC))
(SCC). This lab is typically open 24 hours during the weekdays and for a
more limited time on the weekends. The daily schedule the SCC can be
found [here](http://oal.tamu.edu/Lab_Information/Daily_Lab_Hours.php).

The final workstation, **hprclab0.tamu.edu** is available at our help
desk at [114B Henderson Hall on Jones
street](https://hprc.tamu.edu/about/contact.html) (across from Northside
Dorms) from 9-5 M-F (when open... please email HPRC help to check on
availability).

## Obtaining help

If you have any issues, please email <help@hprc.tamu.edu>. We can help
with login and other issues. When sending email, be sure to follow these
[recommendations](https://hprc.tamu.edu/user_services/consulting.html)
so we can help you in a prompt and efficient manner.

In the case of obvious serious hardware failure (smoke), please contact
the OAL personnel for assistance in unplugging the machine ASAP.

## Usage policy and guidelines

The HPRC Lab workstation accounts are to be used for work that is
related to the purpose for which a user was granted a HPRC account.
These machines are meant primarily for interactive tasks
(post-processing or visualization work). Users who need to work
primarily through the batch systems on the clusters (submitting batch
jobs and running programs on the command line) may do so using any of
the Windows machines in the Open Access Labs. They simply need a secure
shell window to log in to one or more of the clusters. When both types
of users wish to use the Linux workstations, those with non-interactive
needs must yield use of the machines to those who have
interactive/graphical/visualisation tasks to perform. Furthermore, no
user may occupy a workstation for more than 2 hours in a single sitting,
unless there is no one else waiting to use a workstation.

## Logging in

Users may login to these workstations either at the console (while
sitting in front of the workstation), or remotely over the network using
a secure shell connection (SSH). In either case, the user must use their
NetID and password.

## Disk space management

At present, there are no quota on user's /home directories. User's are
expected to move their files off the system when not using them.

1.  Directories which are not shared, like `/home/aggie` for instance,
    represent separate and independent disk storage that is local to
    each workstation. Saving a file in `/home/aggie` on the workstation
    **hprclab2.tamu.edu** means that you cannot access it in
    `/home/aggie` on any workstation other than **hprclab2.tamu.edu**.
2.  If you like, you can use **sshfs** to access your data on HPRC
    clusters. For example:

<!-- end list -->

    cd                # change to home directory 
    mkdir ada         # make a directory for ada mounts
    mkdir ada/home    # for ada:/home
    mkdir ada/scratch # for ada:/scratch
    sshfs $USER@ada.tamu.edu:/home/$USER ~/ada/home # mount ada:/home/$MyNetID
    sshfs $USER@ada.tamu.edu:/scratch/user/$USER ~/ada/scratch # mount ada:/scratch/user/$MyNetID

Then you can access your ada files with something like **ls
~/ada/scratch**.

These mounts will automatically disconnect when you log out.

NOTE: This is only provided as a way to easily copy files/data back and
forth between clusters and workstations. IT IS REALLY SLOW. Don't try to
run models from ada filesystems... copy them to the local system (and
then remember to copy back) any data files/models/etc as needed.

## Locally installed software

The following software packages have been installed on each of the Linux
workstations to enable users to offload postprocessing and visualization
tasks from the heavily loaded (and therefore interactively less
responsive) clusters.

The following commericial (licensed) applications are presently
installed.

  - Abaqus 6.14 CAE   

To launch the abaqus GUI, use the following command:

`[ netID@hprclab ~]$ `**`abaqus   cae   -mesa`**

<font color=teal>**Bug Notice:** If Abaqus launches with transparent
windows and/or a off color GUI, use the command:</font color=teal>

`[ netID@hprclab ~]$ `**`xfconf-query   -c   xfwm4   -p 
 /general/use_compositing   -t   bool   -s   false`**

  - **Matlab 2013a**  

To launch Matlab, use the following command:

`[ netID@hprclab ~]$ `**`matlab`**

**Note:** For users that are running Abaqus CAE and Viewer on a SCLAB
workstation and using X11 forwarding to display the GUI on their Windows
PC. The -mesa command line option should be used if your X11 emulator
does not support OpenGL (eg. Xming).

In addition to commercial applications, there is a plethora of
open-source software installed on these systems. These include:

  - [Grace](http://plasma-gate.weizmann.ac.il/Grace/) - **xmgrace**
  - [GROMACS](http://www.gromacs.org/) - (see: rpm -ql gromacs | grep
    bin)
  - [LAMMPS](http://lammps.sandia.gov/) - **lmp\_g++**
  - [LibreOffice](http://www.libreoffice.org/) - **ooffice**
  - [NAMD](http://www.ks.uiuc.edu/Research/namd/) - **namd**
  - [Ncview](http://meteora.ucsd.edu/~pierce/ncview_home_page.html) -
    **ncview**
  - [OpenFOAM](http://www.OpenFOAM.org/) - (see: rpm -ql OpenFOAM | grep
    /bin/)
  - [Paraview](http://www.paraview.org/) - **paraview**
  - [RStudio](http://www.rstudio.com/) - **rstudio**
  - [TexLive](http://tug.org/texlive/) - **latex, dvips, bibtex** etc.

## Launching remote software

If there is a need to launch software that resides on one of the
clusters but have it display it's graphical interface on the Linux
workstation where the user is sitting, the following instructions can be
used: Assume the program name is "xemacs" and that it resides on and
will be executed on the machine "eos". At the prompt in a unix shell
window (on your workstation), type:

    ssh <NetID>@<clustername>.tamu.edu

NOTE: By default, ssh on the HPRC Lab workstations includes '-X'
(forward X11)

## Hardware

  - System: Dell OptiPlex 9030s
  - Processor: Intel(R) Core(TM) i7-4770S @ 3.10GHz (BLOC 130) or
    i7-4790S CPU @ 3.20GHz (SCC)
  - RAM: 8GB
  - Operating System: Fedora 32 x86\_64
  - Hard Disk: 465GB
  - Network: 1000/100Mbps Ethernet

## Photos

### OAL in the Student Computing Center (SCC)

The SCC is located next to Evans Library, behind the Central Campus
Garage.

|                                                                                                         |
| ------------------------------------------------------------------------------------------------------- |
| ![Hprclab workstations available in the SCC](/kb3/assets/images/SCC-3-web.jpg "Hprclab workstations available in the SCC") |
