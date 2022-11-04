# LS-OPT

LS-OPT is a standalone Design Optimization and Probabilistic Analysis
package FOR LS-DYNA.  
Homepage: <http://www.lstc.com/products/ls-opt>

## Access

LS-OPT is available to <font color=teal>**any users within an academic
department which has purchased their own license**</font>. We host the
license on behalf of the licensed department(s).

## Documentation

The documentation can be found at <http://www.lsoptsupport.com/>.

### Loading the Module

To see all versions of LS-OPT available on Ada:

`[NetID@cluster ~]$ module spider LS-OPT`

To load a particular version of LS-OPT on Ada (Example: 5.2.1):

`[NetID@cluster ~]$ module load LS-OPT/5.2.1`

To show the help information for a particular version of LS-OPT:

``` 
 [NetID@cluster ~]$ module help LS-OPT/5.2.1

------------------------------- Module Specific Help for "LS-OPT/5.2.1" --------------------------------
  LS-OPT is a standalone Design Optimization and Probabilistic Analysis package with an interface to LS-DYNA. - Homepage: http://www.lstc.com/products/ls-opt/
    
  Sets up environment for LS-OPT 5.2. A module for LS-DYNA will also be loaded for use with this module.  Use the lsopt command to start LS-OPT or the lsoptui command to start the LS-OPT GUI.  The manual is located at /software/tamusc/LS-OPT/5.2/LSOPT_EXE/lsopt_52_manual.pdf 
```

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use
non-interactive batch jobs for resource-intensive and/or multiple-core
processing. Users are requested to be
<font color=teal>**responsible**</font> and <font color=teal>**courteous
to other users**</font> when using software on the login nodes.

The most important processing limits here are:  
\* **ONE HOUR** of **PROCESSING TIME** per login session.

  - **EIGHT CORES** per login session on the same node or (cumulatively)
    across all login nodes.

<font color=red size=3>**Anyone found violating the processing limits
will have their processes killed without warning. Repeated violation of
these limits will result in account suspension.**</font>  
<font color=teal>**Note:** Your login session will disconnect after
**one hour** of inactivity.</font>

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.

<font color=teal>**NOTE: LS-OPT should be started with vglrun when used
via VNC jobs .**</font>

## More Information

To find more information on LS-OPT, please consult
<http://www.lstc.com/support/resources> for an overview, tutorials, FAQ,
and the LS-OPT user group.
