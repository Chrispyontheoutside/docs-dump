# LS-PREPOST

LS-PREPOST is an advanced pre and post-processor for LS-DYNA. -
Homepage: <http://www.lstc.com/lspp/>

## Access

LS-PREPOST is available to <font color=teal>**any users within an
academic department which has purchased their own license**</font>. We
host the license on behalf of the licensed department(s).

## Documentation

The documentation can be found at
<http://www.lstc.com/lspp/content/overview.shtml>.

### Loading the Module

To see all versions of LS-PREPOST available on Ada:

`[NetID@cluster ~]$ module spider LS-PREPOST`

To load a particular version of LS-PREPOST on Ada (Example: 4.3):

`[NetID@cluster ~]$ module load LS-PREPOST/4.3`

To show the help information for a particular version of LS-PREPOST:

``` 
 [NetID@cluster ~]$ module help LS-PREPOST/4.3

----------------------------------------------------- Module Specific Help for "LS-PREPOST/4.3" ------------------------------------------------------
  LS-PREPOST is an advanced pre and post-processor that is delivered free with LS-DYNA. - Homepage: http://www.lstc.com/lspp/ 
  Sets up environment for LS-PREPOST 4.3. 
  The command to launch LS-PREPOST is lsprepost.  
  For online help, select Help->Documentation from the menu within LS-PREPOST. 
  Examples can be found in the /sw/hprc/LS-PREPOST/examples directory. 
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

<font color=teal>**NOTE: LS-PREPOST should be started with vglrun when
used via VNC jobs .**</font>

## Examples

LS-PREPOST examples can be found in the
<font color=teal>**/sw/hprc/LS-PREPOST/examples**</font> and
<font color=teal>**/sw/hprc/sw/LS-PREPOST/examples**</font> directories
on Ada and Terra respectively.

## More Information

To find more information on LS-PREPOST, please consult
<http://www.lstc.com/lspp/> for an overview, tutorials, FAQ, and the
LS-PREPOST user group.
