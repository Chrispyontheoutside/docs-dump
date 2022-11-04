# Software

### Q: Is \[blank\] software installed on the clusters?

**A:** To see if the software is available on the clusters, use **module
avail**:

`[NetID@cluster ~]$ `**`module   avail   `*`[package 
 name]`***

This will show a list of all the available software matching this name.
The command **module spider** can be used to search for available
software:

`[NetID@cluster ~]$ `**`module   spider   `*`[package 
 name]`***

<font color=teal>More information on the module system can be found on
our [Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.</font>

### Q: How do I load \[blank\] software?

**A:** Our clusters use a module system to manage software. This means
that to use the software, the proper modules must be loaded first. To
load a module, use **module load**:

`[NetID@cluster ~]$ `**`module   load   `*`[package 
 name]`***

**Note:** The full module name, including the version number, is
required to load specific modules. Use **module spider** to find the
full module name.  
<font color=teal>More information on the module system can be found on
our [Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.</font>

### Q: How many \[blank\] licenses are available?

**A:** On our clusters we have a license status checker tool in order to
see how many licenses are currently in use and how many are available.
To check the license status of a certain software, use **license\_status
-s**:

`[NetID@cluster ~]$ `**`license_status   -s   `*`[package 
 name]`***

<font color=teal>More information for this tool can be found on our
[License Checker](/kb3/Software/useful-tools/SW@License_Checker/ "wikilink") page.</font>

### Q: The software I need is not installed, what can I do?

**A:** If a particular software is not already installed on the cluster,
you can [contact us](https://hprc.tamu.edu/about/contact.html) regarding
the installation of this software. If the software requires a license
which we do not already have, you or your department will need to
provide your own license to be able to use the software on the cluster.
In general we try to provide as much software as possible for our users.
However, this is not always possible, nor is it always possible in a
timely manner. If you need a software that is not installed on the
cluster, you are also able to install it for yourself on your Scratch
directory. However, this is only recommended for experienced users.  
**Note:** We are unable to install Windows only software/packages on our
clusters.  
<font color=teal>Please account for delays in your installation request
timeline. </font>

### Q: I have a license server for \[blank\] software, can I use this software on your clusters?

**A:** If you have a license for a particular software which you would
like to use on the clusters, you will need to [contact
us](https://hprc.tamu.edu/about/contact.html) with that information. We
will need the name and version of the software you will be using along
with the license file and the host name of your license server.

### Q: I do not know how to use \[blank\] software, can you help me?

**A:** We have documentation on the [ software](/kb3/Software/SW/ "wikilink") page
regarding some of our software, however, these are more for getting
started running jobs on the cluster, not necessarily using the software.
In a lot of cases, we do not have a lot of experience using the software
that is provided on our clusters. That being said, it is often best to
consult the user guide of a particular software if you are having
trouble using the software. We can always try to provide assistance, but
in some cases we will only be able to provide as much help as the user
guide for that software provides.