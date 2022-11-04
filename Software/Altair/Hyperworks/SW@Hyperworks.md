# Hyperworks

## Description

Altair Hyperworks provides the most comprehensive, open-architecture CAE
solution in the industry including best-in-class modeling, analysis, and
optimization. - Homepage: <http://www.altairhyperworks.com/>

### Documentation

We have documentation available for the following versions of
Hyperworks:

  - [Hyperworks 2017](https://hprc.tamu.edu/softwareDocs/hyperworks/2017/altair_help/welcome_page.htm)

## Access

To see all versions of Hyperworks available on Ada:

` [ netID@cluster ~]$ `**`module   spider   Hyperworks`**

To load a particular version of Hyperworks on Ada (Example: 2017):

` [ netID@cluster ~]$ `**`module   load   Hyperworks/2017`**

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (20 cores, 64GB or 256GB). There are fewer VNC
nodes than comparable compute nodes. Nearly all processing that is done
within the GUI can be done more efficiently within a non-interactive job
once the pre-processing is done.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Ada Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/ "wikilink")
page.

### Running the Hyperworks GUI

Using the Hyperworks GUI requires loading an OpenGL module before
launching the GUI. To load the necessary OpenGL module on Ada:

` [ netID@cluster ~]$ `**`module   load   OpenGL/NVIDIA`**

Hyperworks has various commands to start its desktop applications:

  - **hg:** Starts HyperWorks Desktop with the HyperGraph 2D client
    loaded

<!-- end list -->

  - **hm:** Starts HyperMesh standalone

<!-- end list -->

  - **hmdesktop:** Starts HyperWorks Desktop with the HyperMesh client
    loaded

<!-- end list -->

  - **hv:** Starts HyperWorks Desktop with the HyperView client loaded

<!-- end list -->

  - **hw:** Starts HyperWorks Desktop with the default client loaded

<!-- end list -->

  - **mview:** Starts HyperWorks Desktop with the MotionView client
    loaded

While in a VNC job, use **hw** (with vglrun) to start the Hyperworks
desktop with the default client loaded:

`[NetID@gpu ~]$ `**`vglrun   hw`**
