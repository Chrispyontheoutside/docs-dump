# EBROOT

<font color=red> *THIS PAGE IS UNDER CONSTRUCTION*</font>


Some software installation procedures and/or advanced usage of the
clusters require access to the installation directories of module
software. The $EBROOT\* variables can be used to find relevant
directories, simplify scripting, or avoid typing the full path.

EXAMPLE (wip):

    module load intel/2015B
    echo $EBROOTINTEL
    ////

## env

## bashrc + (default files?) + warning

The bashrc file is used to initialize your environment when using Bash
on our clusters. (Re)Initialization usually occurs when first logging
in, within bash scripts, and within jobs. It is for this reason that it
is recommended that you DO NOT MODIFY the bashrc file. Modifications may
work while on the login nodes or for certain jobs, but they often cause
obscure issues when modules/modifications conflict.

### Conflict Example

The following is an example of bad modification to the bashrc file that
causes a conflict between modules under certain circumstances. Trying to
recreate this issue may cause any of the same result, different
problems, or no issue - this is due to the updating of modules and
further compounds troubleshooting difficulty.

### Default bashrc

If you wish to restore your bashrc file to the cluster-default, you can
retrieve a copy from the following locations.

**Ada/Curie:**

`    PH`

**Terra:**

`    PH`  

**Crick:**

`    PH `
