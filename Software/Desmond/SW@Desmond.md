# Desmond/Maestro (for academic use only)

## Description

Desmond is a high-performance molecular dynamics (MD) code for
biological systems developed by D. E. Shaw Research. Only GPUs are
supported starting from the Desmond\_Maestro\_2019.1 release. For more
information, visit the
[Desmond](https://www.deshawresearch.com/resources_desmond.html).  

## Access

Access to Desmond/Maestro non-commercial version is granted to users who
have registered to download Desmond. Licenses for the commercial use of
Desmond are available from Schrödinger, LLC.  
Access to other [Schrödinger](/kb3/Software/Schrodinger/SW@Schrodinger/)
applications (ligprep, glide, prime, etc.) is restricted to subscribers
of the HPRC-Laboratory for Molecular Simulation(LMS).

### Desmond Registration

First, visit [this
page](https://www.deshawresearch.com/downloads/download_desmond.cgi/) to
complete registration. Acceptance of an End User License Agreement
(EULA) containing the terms of registration is also required. Once
accepted, several download links will be available.

Please send an email to help@hprc.tamu.edu stating that the user has
registered and agreed to the terms and conditions to get access on HPRC
clusters.

### Loading the Desmond modules

Both Grace and Terra have Desmond modules available. To find available
versions, use the following command:  
On Grace:

`[NetID]@grace ~]$ mla desmond`

On Terra:

`[NetID]@terra ~]$ ml spider desmond`

To load a particular Desmond module:

`[NetID]@grace/terra ~]$ ml Desmond/2021-1`

### Running Desmond in the Portal

It is suggested to run Maestro using VNC implemented under [Interactive
Apps](/kb3/Software/Portal/SW@Portal/#interactive-apps/) in the
[Portal](/kb3/Software/Portal/SW@Portal/)

You can request a CPU node (eg. 2 hours, 2 cores, 8GB memory, any node
type)  

Load the correct module. For example:  
On Grace:

`ml Desmond/2021-1`

On Terra:

`ml desmond/2021-1`

Run Maestro:  
maestro

A set of modules are preloaded to the portal to support the smooth
running of graphical interface. **ml purge** should be used with
caution. If the window decorations does not show up properly, please
right click in the blank area and choose Fluxbox menu \> Restart.
