# The Modules System

## Introduction

The *Modules* system organizes the multitude of packages we have
installed on our clusters so that they can be easily maintained and
used. More specifically, Modules configure appropriately the execution
environment of each package (and version).  
Most non-OS software is organized by the Modules system. This includes
all compilers and associated libraries. Each package has a corresponding
*modulefile* or simply a *module* where the appropriate actions are
specified (in a prescibed format) in setting up its execution
environment.  
**Notify the help desk if you cannot locate the module appropriate for
an application.**  

## Module Commands

To find out what software packages are available under the Modules
system use one of the following two commands:

`[NetID@cluster ~]$ `**`module   spider   `*`[packageName]`***

`[NetID@cluster ~]$ module avail `*`[packageName]`*` `

In order to use some software on our clusters, the module for the
software must be loaded first. To load the module for a software
package, use the following command:

`[NetID@cluster ~]$ module load `*`packageName/version`**`''`
<font color=teal>**`Note:`*`' The specification of packageName in the load command is case sensitive and it `**`must`**` include a specific version. `**`No 
 packages   are   preloaded   by 
 default.`**</font>  
<font color=teal>**`Note:`**` Loading a package is required in order to access the man pages associated with the package if they are available. `</font>  

To find out what packages/modules you have loaded on your current
session, use the following command:

`[NetID@cluster ~]$ `**`module   list`**

To remove one module from your current session, use the following
command:

`[NetID@cluster ~]$ `**`module   unload   [packageName]`**

To remove ALL modules from your current session, use the following
command:

`[NetID@cluster ~]$ `**`module   purge`**

<font color=teal>**Note:** It is **very** important to remove all
modules when switching between software and compilers. Mixing modules
and versions is NOT a good idea and can cause many problems.</font>  
To search and list what packages/modules are available on Grace, enter
any suitable combination of the following:

`[ NetID@grace ~]$ `**`module   spider 
 `*`[packageName]`***`          # List all versions of all packages or just for packageName.`  
`[ NetID@grace ~]$ `**`module   spider 
 `*`string`***`                # List all modules that contain the "string".`  
`[ NetID@grace ~]$ `**`module   spider 
 `*`packageName/version`***`   # List detailed information about that version of packageName`  
`[ NetID@grace ~]$ `**`module   keyword 
 `*`string`***`                # List all modules and whatis that contain string.`

For additional help see:

`[ NetID@grace ~]$ `**`module 
 help`**`                          # Lists all the subcommands under the module command.`  
`[ NetID@grace ~]$ `**`module   help 
 `*`packageName`***`              # Lists information about packageName`

To remove (unload) a module and load another, use the swap subcommand:

`[ NetID@grace ~]$ `**`module   swap   `*`packageOUT 
 packageIN`***

The above command is short for:

`[ NetID@grace ~]$ `**`module   unload   `*`packageOUT`***` `  
`[ NetID@grace ~]$ `**`module   load   `*`packageIN`***

### HPRC Shorthand

A handy front end for the HPRC module system is the command: **ml**.

<font color=teal>**Note:** The abbreviation **ml** can be used instead
of **module**, **module load**, or **module list** depending on the
situation. This can be seen in the examples below.</font>

`[ NetID@grace ~]$ `**`ml`**  
`                             means: module list`  
`[ NetID@grace ~]$ `**`ml   foo   bar`**  
`                             means: module load foo bar`  
`[ NetID@grace ~]$ `**`ml   -foo   -bar   baz   goo`**  
`                             means: module unload foo bar;`  
`                                    module load baz goo;`  
`[ NetID@grace ~]$ `**`ml   subcommand   arg1   arg2 
 ...`**  
`                             means: module subcommand arg1 arg2 ...;`  
`     where subcommand is any of avail, save, restore, show, swap...`

An additional shorthand command provided is: **mla**. It replicates the
function of module avail, but stores results in a file for quick
reference later.

`[ NetID@grace ~]$ `**`mla   foo`**  
`                             means: module avail foo ...`  
`[ NetID@grace ~]$ `**`mla   -f`**  
`                     Use -f to force an update of the cached module list.`

### Examples

The output below shows the output of the **spider** command for
*ABAQUS*:

`[ NetID@grace ~]$ `**`ml   spider 
 `*`ABAQUS`***`         `*`#   module   abbreviated 
 as   `**`ml`***  
`----------------------------------------------------------------------------------------`  
`  ABAQUS:`  
`----------------------------------------------------------------------------------------`  
`    Description:`  
`      Finite Element Analysis software for modeling, visualization and best-in-class`  
`      implicit and explicit dynamics FEA. - Homepage:`  
`      `<http://www.simulia.com/products/abaqus_fea.html>  
  
`     Versions:`  
`        ABAQUS/6.12.1-linux-x86_64`  
`        ABAQUS/6.13.5-linux-x86_64`  
`   . . .`

The output below illustrates the fact that a modulefile's complete name
includes its version. An installed application can have several
versions.

`[ NetID@cluster ~]$ `**`ml   `*`ABAQUS/2017`***`       `*`# 
 module   load   abbreviated   as   `**`ml`***  
`[ NetID@cluster ~]$ `**`ml`**`                   `*`#   module 
 list   abbreviated   as   `**`ml`***  
` `  
`Currently Loaded Modules:`  
`  1) ABAQUS/2017`

The output below shows the functionality of the **swap** command:

`[ NetID@cluster ~]$ `**`ml   load   `*`ABAQUS/2016`***  
`[ NetID@cluster ~]$ `**`ml   swap   `*`ABAQUS/2016 
 ABAQUS/2017`***  
  
`The following have been reloaded with a version change:`  
`  1) ABAQUS/2016 => ABAQUS/2017`  
  
`[ NetID@cluster ~]$ `**`module   list`**  
  
`Currently Loaded Modules:`  
`  1) ABAQUS/2017`

## WARNING: Do not include module commands in your startup files\!\!\!

We advise users to NOT put **module load** commands in their startup
files like $HOME/.bashrc and $HOME/.bash\_profile. Although you may
think this makes life easier you will find in time that it causes all
kinds of problems later on (e.g. when switching to different programs or
running batch jobs).

If you really want to be able to load a set of modules quickly then look
at Lmod's ["user
collections"](https://lmod.readthedocs.io/en/latest/010_user.html#user-collections).
You can use **module save** to create a default collection of modules
and then you simply have to run **module restore** to restore them (BUT
DON'T DO THAT in .bashrc/.bash\_profile). You can also named
collections... e.g. I might do **module save openfoam** after loading
all the OpenFOAM modules I need (after a **module purge**) and then do a
**module save ANSYS** that has the modules I use with ANSYS. Then I can
restore either of those collections with **module restore <name>**.
