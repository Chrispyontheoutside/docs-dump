# FASTER Computing Environment


## Introduction

FASTER is using the **CentOS 7** Linux distribution on all nodes. The
global file systems (accessible to all nodes) are organized by
**Lustre** Parallel File System. These are **/home** and **/scratch**.
Both are hosted on the 5PB usable disk space provided by DDN.  
The batch system, although a **very** important part of the computing
environment, is covered in a separate section of its own. More
information on the batch system can be found on the [ Batch Processing
](/kb3/User-Guides/FASTER/FASTER@Batch/ "wikilink") page.

## Login

The default shell for FASTER (all nodes) is bash. Its environment is
defined in the startup file, **.bash\_profile**. It is read and executed
when you login, and it resides in your home directory.

Each of the four login nodes can be accessed with ssh to
faster.tamu.hprc.edu. To access a specific login node, you would need to
use the specific name to ssh. To access FASTER, use the following
command from your local machine:

`[user1@localhost ~]$ `**`ssh   `*`[NetID]`*`@faster.hprc.tamu.edu`**

The use of the login nodes is for small-to-medium code development and
processing. The most important processing limits here are:  
\* CPU time - ONE HOUR per login session.

  - Cores for Concurrent Use - EIGHT CORES per login session, on the
    same node or (cumulatively) across all login nodes.

<font size=3 color=red>**ANYONE found violating these limits WILL have
their processes killed WITHOUT WARNING. Repeated violation of these
limits WILL result in account suspension.**</font>

More information about the hardware of each of the login nodes can be
found on the [ Hardware Summary ](/kb3/User-Guides/FASTER/FASTER@Intro/#login-nodes "wikilink")
page.  

## File Space

Immediately upon logging in to FASTER, the following message about the
status of your disk space use greets you (format may vary):

    Your current disk quotas are:
    Disk       Disk Usage      Limit    File Usage      Limit
    /home           2.49G        10G           113      10000
    /scratch        1.25G         1T            40      250000
    Type 'showquota' to view these quotas again. 

<font color=teal>**Note:** It is important to pay attention to this
information, as it shows how much space has been used in each directory.
Hitting a quota limit can cause problems for the user and should be
avoided.</font>  
More information on the specific file systems including limitations and
information about expansions can be found on the [ File Systems
](/kb3/User-Guides/FASTER/FASTER@Filesystems_and_Files/ "wikilink") page.

## Modules

The *Modules* system organizes the multitude of packages we have
installed on our clusters so that they can be easily maintained and
used. **Any** software you would like to use on FASTER should use the
Modules system.  
**NO modules are loaded by default.**

The main command necessary for using software on FASTER is the *load*
command. To load a module, use the following command:

`[NetID@cluster ~]$ `**`module   load   `*`[packageName]`***

The specification of packageName in the *load* command is case sensitive
and it **should** include a specific version. To find the full name of
the module you want to load, use the following command:

`[NetID@cluster ~]$ `**`module   spider   `*`[packageName]`***

To see a list of available modules, please use the mla wrapper script:

`[NetID@cluster ~]$ `**`mla`**

More information on the Modules system can be found on the [ Modules
System ](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.
