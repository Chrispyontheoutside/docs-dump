# EnSight

## Description

EnSight is a software program for visualizing, analyzing, and
communicating data from computer simulations and/or experiments. -
Homepage: <https://www.ensight.com/ensight10/what-is-ensight/>

## Access

EnSight is open to all HPRC users when used within the terms of our
license agreement. If you have particular concerns about whether
specific usage falls within the TAMU HPRC license, please send an email
to the HPRC Helpdesk.

<font color=teal>**Note:** Ensight is ONLY available via the ANSYS 19.0
or newer modules.</font>

### Loading the Module

Load the ANSYS 19.3 module first:

       [NetID@cluster ~]$ `**`module   load   ANSYS/19.3`**

<font color=teal>**Note:** New versions of software become available
periodically. Version numbers may change.</font>

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.

### Running the EnSight GUI

While in a VNC job, use **ensight** (with vglrun) to start the EnSight
GUI:

        [NetID@gpu ~]$ vglrun ensight102 
