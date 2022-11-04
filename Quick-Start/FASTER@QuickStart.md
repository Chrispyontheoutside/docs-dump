# FASTER Quick Start Guide

## FASTER Usage Policies

**Access to FASTER is granted with the condition that you will
understand and adhere to all TAMU HPRC and FASTER-specific policies.**

General policies can be found on the [HPRC Policies
page](https://hprc.tamu.edu/policies/).

## Accessing FASTER

Most access to FASTER is done via a secure shell session. In addition,
**two-factor authentication** is required to login to any cluster.

Users on **Windows** computers use either [PuTTY](http://www.putty.org/)
or [MobaXterm](http://mobaxterm.mobatek.net/). If MobaXterm works on
your computer, it is usually easier to use. When starting an ssh session
in PuTTY, choose the connection type 'SSH', select port 22, and then
type the hostname 'faster.hprc.tamu.edu'. For MobaXterm, select
'Session', 'SSH', and then remote host 'faster.hprc.tamu.edu'. Check the
box to specify username and type your NetID. After selecting 'Ok', you
will be prompted for Duo Two Factor Authentication. For more detailed
instructions, visit the [Two Factor
Authentication](/kb3/Helpful-Pages/Two-Factor/Two_Factor/#mobaxterm/) page.

Users on **Mac** and **Linux/Unix** should use whatever SSH-capable
terminal is available on their system. The command to connect to FASTER
is as follows. Be sure to replace \[NetID\] with your TAMU NetID.

`[user1@localhost ~]$ `**`ssh   `*`[NetID]`*`@faster.hprc.tamu.edu`**

<font color=teal>**Note:** In this example *\[user1@localhost ~\]$*
represents the command prompt on your local machine.</font>  
Your login password is the same that used on
[Howdy](https://howdy.tamu.edu/). You will not see your password as your
type it into the login prompt.

### Off Campus Access

Please visit [this page](/kb3/Helpful-Pages/Access/HPRC@Access/#access-using-ssh/)
to find information on accessing FASTER remotely.

For more detailed instructions on how to access our systems, please see
the [ HPRC Access page](/kb3/Helpful-Pages/Access/HPRC@Access/ "wikilink").
