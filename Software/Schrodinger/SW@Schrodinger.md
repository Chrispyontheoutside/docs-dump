# Schrödinger

**Schrödinger is a restricted software.**

Usage of this software is restricted only to subscribers of the
HPRC-[Laboratory for Molecular
Simulation(LMS)](https://lms.hprc.tamu.edu/). If you believe you are
eligible to use Schrödinger on our clusters, please email the HPRC Help
Desk with the request and justification.  
Access to free-to-academics version of Desmond/maetstro does not require
LMS subscription. Please follow the insturctions on the
[Desmond](/kb3/Software/Desmond/SW@Desmond/) wiki page and email the
HPRC Help Desk with the request.

## Description

**Schrödinger** is a software platform used for pharmaceutical,
biotechnology, and materials science research. Homepage:
[Schrodinger.com](https://www.schrodinger.com/)  
**Maestro** is the graphical user interface of Schrödinger and the
portal to all of Schrödinger's computational applications.
[Maestro](https://www.schrodinger.com/maestro)  
**Desmond** is the high-performance molecular dynamics (MD) code.
[Desmond](https://www.schrodinger.com/desmond)  
**Glide** is used for ligand-receptor docking.
[Glide](https://www.schrodinger.com/glide)  
**Jaguar** is the quantum mechanical (QM) code for ab inito electronic
structure calculations.
[Jaguar](https://www.schrodinger.com/ms-jaguar)  
A full list of applications on Schrödinger Platform can be found at [All
Products](https://www.schrodinger.com/platform#product-list-collapse)  

### Loading the Schrödinger modules

Both Grace and Terra have Schrödinger modules available.  
To check the available number of licenses:

`license_status -s Schrodinger`

**On Grace**  
To list the versions of Schrodinger installed on Grace (as of
10/12/2021):

`[NetID]@grace ~]$ mla Schrodinger`  
`Schrodinger/2020-1`  
`Schrodinger/2021-3`

To load a particular Schrödinger module:

`[NetID]@grace ~]$ ml Schrodinger/2020-1`

**On Terra**  
To list the versions of Schrodinger installed on Terra:

`[NetID]@terra ~]$ ml spider schrodinger`  
` schrodinger/2018-4`  
` schrodinger/2020-1`

To load a particular Schrödinger module:

`[NetID]@terra ~]$ ml schrodinger/2020-1`

### Running Schrödinger in the Portal

It is suggested to run Maestro using VNC implemented under [Interactive
Apps](/kb3/Software/Portal/SW@Portal/#interactive-apps/) in the
[Portal](/kb3/Software/Portal/SW@Portal/)

You can request a CPU node (eg. 2 hours, 2 cores, 8GB memory, any node
type)  
Load the correct module. For example:  
on Grace:

`ml Schrodinger/2021-3 `

on Terra:

`ml schrodinger/2020-1 `

To launch Maestro:

`maestro`

To launch Maestro Material Science Interface:

`maestro -profile MaterialsScience`

A set of modules are preloaded to the portal to support the smooth
running of graphical interface. **ml purge** should be used with
caution. If the window decorations does not show up properly, please
right click in the blank area and choose Fluxbox menu \> Restart.

## Frequently Asked Questions
