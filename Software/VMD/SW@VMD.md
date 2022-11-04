# VMD

## Description

VMD is a powerful molecular visualization tool that is very popular for
preparation and analysis of biological systems (protiens, nucleic acids,
*etc.*). VMD can be used to animate and analyze the trajectory of
molecular dynamics (MD) simulations from both external MD programs and
NAMD. NAMD is a fast, parallel, and scalable molecular dynamics program
developed in conjunction with VMD.  
Homepage: <https://www.ks.uiuc.edu/Research/vmd/>

## Access

### Running VMD in the Portal

There are a variety of VMD modules supported on Terra and Grace.  
It is suggested to run VMD using VNC implemented under [Interactive
Apps](/kb3/Software/Portal/SW@Portal/#interactive-apps/) in the
[Portal](/kb3/Software/Portal/SW@Portal/). You will need to request
a GPU node.  
When the portal VNC terminal is started, use the following commands to
launch VMD.

#### Grace

To purge unnecessary modules before getting started:

` [ netID@cluster ~]$ `**`ml   purge`**

To load a particular version of VMD on Grace:

` [ netID@cluster ~]$ `**`ml   iccifort/2020.1.217 
 impi/2019.7.217   VMD/1.9.3-Python-2.7.18`**

To launch VMD:

` [ netID@cluster ~]$ `**`vmd`**

#### Terra

To purge unnecessary modules before getting started:

` [ netID@cluster ~]$ `**`ml   purge`**

To load a particular version of VMD on Terra:

` [ netID@cluster ~]$ `**`ml   VMD/1.9.3-LINUXAMD64-opengl`**

To launch VMD:

` [ netID@cluster ~]$ `**`vglrun   vmd`**
