# How to Access to Cluster

## Access Using SSH


To connect to HPRC clusters, you must use SSH (Secure Shell). SSH is a
client-server software that provides for secure (by encryption) logins
and other communication between two hosts. SSH is freely available on
the Internet for Linux/Unix and PC Windows (in the guise of
[MobaXterm](http://mobaxterm.mobatek.net/)).

To initiate SSH connection to target cluster's login node, find the
hostname (terra/grace) and credential (userID/password) info from Table
1 below. For example, if you are connecting to Grace cluster from a
terminal enter:

`[user1@localhost ~]$ `**`ssh   `*`NetID`*`@grace.tamu.edu`**

where the grace.tamu.edu address is a DNS round-robin alias for
grace\[1-4\].tamu.edu. You will be prompted for your password in order
to establish authentication. Once you login into one of the login nodes,
the shell's prompt will be *\[NetID\].grace*\[1-8\].  
If, however, you are connecting for the very first time, you will see a
message similar to the following before arriving at the password prompt:

    The authenticity of host 'grace (165.91.16.18)' can't be established.
    ECDSA key fingerprint is SHA256:SfQPtDJW30sj4kG2c4KGFw7LcEduSOFeXGIlsf4WhEA.
    ECDSA key fingerprint is MD5:9c:ea:ba:22:0f:6f:1e:b9:0c:21:d4:b6:70:0f:a0:d5.
    Are you sure you want to continue connecting (yes/no)? 

Type **yes** and you will then be presented with the password prompt.

    Warning: Permanently added 'grace' (ECDSA) to the list of known hosts.
    NetID@grace.tamu.edu's password:

| Cluster   | Hostname            | Number of login nodes | Credential (UserID / Password) |
| --------- | ------------------- | --------------------- | ------------------------------ |
| **Terra** | terra.tamu.edu      | 3 (terra1 ~ terra3)  | NetID / NetID password         |
| **Grace** | grace.hprc.tamu.edu | 4 (grace1 ~ grace4)  | NetID / NetID password         |

Table 1: Hostname and credential info of HPRC clusters

### Off-campus Access

For connecting to cluster login nodes from outside the campus, you need
to activate Virtual Private Network (VPN) first, then initiate SSH
connection to the cluster login nodes. You can find VPN installation
instruction from [TAMU ServiceNow Knowledge Base page on
VPN](https://tamu.service-now.com/tamu-selfservice/knowledge_detail.do?sysparm_document_key=kb_knowledge,02ce68792badc6009b4c26e405da151e).

### Two Factor Authentication Requirement

Starting October 1, 2018, the Division of Information Technology will
require use of Duo NetID Two Factor Authentication on its Virtual
Private Network (VPN) (connect.tamu.edu) service.

Duo provides a second layer of security to Texas A&M accounts.

If you are not already enrolled in Duo and plan to use VPN, you can
enroll now at duo.tamu.edu. Enrolling is as easy as 1-2-3:

1\. Choose your device and download the Duo Mobile app. (We strongly
recommend the mobile app as the most user-friendly option.)

2\. Start your enrollment at <https://gateway.tamu.edu/duo-enroll/>;

3\. Remember: Once you sign up, you will need your Duo-enrolled device
when you log in to most Texas A&M resources.

For more information, consult IT's knowledge base article for Duo:
<https://u.tamu.edu/KB0012105>

## Access from Windows

### Using MobaXterm (Recommended)

[MobaXterm](http://mobaxterm.mobatek.net/) is an enhanced terminal for
Windows with a built-in X11 server, tabbed SSH client, built-in file
editor, SFTP functionality, and other useful features. You may download
MobaXterm from: <http://mobaxterm.mobatek.net/download.html>

You will need to choose which license (free Home edition, or
professional) and then select the Portable or Installer edition. The
Installer edition works best on your personal machine, when you have the
privileges to install software. The portable version may be necessary
when using a lab workstation, for example. (Be sure to check if
MobaXterm is already installed in the Windows Start menu.)

#### Configuration

You may create saved sessions for connecting to **ada.tamu.edu** or
other HPRC clusters, for your convenience. See
<http://mobaxterm.mobatek.net/documentation.html#1_2> for instructions.
For example:

![ 675px | center | MobaXterm SSH](/kb3/assets/images/Moba_ssh.png
" 675px | center | MobaXterm SSH")

IMPORTANT: When asked if you would like to save your password, choose
"**No**" to avoid potential security exploits.

![ 675px | center | MobaXterm save password](/kb3/assets/images/Moba_save-pw.png
" 675px | center | MobaXterm save password")

#### Two factor authentication

1\. On the top left corner of MobaXterm window, click 'Session'
button.  
![ 675px](/kb3/assets/images/moba-0.png " 675px")

2\. You will be prompted with a window which asks for your session
settings.

3\. Enter the 'Remote Host' (e.g. ada.tamu.edu, terra.tamu.edu, etc.)
you would like to connect to.

4\. Select 'Specify', then enter your username (your NetID).

5\. Enter the 'Port Number' 22 (the default should be 22).  
![ 675px](/kb3/assets/images/moba-1.png " 675px")

6\. Press enter.

7\. You will be prompt to authentication with Duo (either using mobile
app, text message or call).

8\. If you wish to open the session again, open the 'Session' tab on the
left side of the screen and double-click the appropriate session to
launch.  
![ 450px](/kb3/assets/images/moba-2.png " 450px")

**File Transfer**

1\. On the top left corner of MobaXterm window, click Session button.

2\. Choose 'SFTP' session type.

3\. Enter remote host (e.g. ada.tamu.edu, terra.tamu.edu, etc.) and
username (your netID).

4\. Go to 'Advanced Sftp settings' and check '2-steps authentication'
checkbox.

5\. After you select 'Ok', you will be prompted with Duo Authentication
method (Push, Call, Text, Second device, etc). Select the appropriate
option. **Do not type your TAMU password.**

Example Duo Authentication methods (You won't see this, it is just to
remind you of the format of Duo Authentication options)

    Enter a passcode or select one of the following options:
    
     1. Duo Push to XXX-XXX-1234
     2. Duo Push to iOS
     3. Phone call to XXX-XXX-1234

**Your Duo settings will be different**

#### File Transfers

On the left-hand side of the MobaXterm window, different tabs are
available. The labels are written vertically. Choosing the "Sftp" tab
will display a file tree of the remote machine to which you are
connected, such as:

![ 675px | center | MobaXterm file explore](/kb3/assets/images/Moba_file-explore.png
" 675px | center | MobaXterm file explore")

You may choose files to edit with the built-in editor. You may also
transfer files from your Windows machine to the remote cluster, and vice
versa. Just drag a local file (from a Windows File Explorer window or
similar program) to the SFTP file tree on the left side of the MobaXterm
window.

#### Remote Display of Programs with Graphical Interfaces

By default, MobaXterm connections have X11 forwarding available. So,
when you connect to **ada.tamu.edu** or other machine, you should be
able to run an X-Windows program by simply typing the command. That will
open the program in a new window behind the MobaXterm main window.

#### Running MobaXterm on Open Access Lab workstations

**Verify MobaXterm is installed**

After logging in to Open Access Labs (OAL) workstation, click on the
magnifying glass to search for an installed program. As you start typing
"MobaXterm", matching programs will be displayed on the left-hand side
of the screen, above the search field.

![ 600px | center | find MobaXterm on Open Access Lab
workstation](/kb3/assets/images/OAL_Find_MobaXterm.png
" 600px | center | find MobaXterm on Open Access Lab workstation")

Once you have started MobaXterm, click "Start local terminal" (as
pictured above in **Local Terminal** section). You may encounter an
error such as the following:

![ 600px | center | MobaXterm permission error
message](/kb3/assets/images/Moba_roothome_error.png
" 600px | center | MobaXterm permission error message")

To solve this problem, you will need to change the location of the
virtual "root" and "home" directories. At the top of the MobaXterm
window in the row of buttons, click "Settings" (the second to last on
the right-hand side):

![ 600px | center | MobaXterm settings button](/kb3/assets/images/Moba_settings.png
" 600px | center | MobaXterm settings button")

A settings dialog will open. By default, the virtual root and home
directories will be set to "***\_MyDocuments\_\MobaXterm***" which
lacks proper write permissions for the OAL workstations:

![ 600px | center | MobaXterm default root and
home](/kb3/assets/images/Moba_default_root_home.png
" 600px | center | MobaXterm default root and home")

Change both of these by clicking on the current values (with the little
yellow folder on the right-hand side). Scroll up to find the
"***Temp***" folder, which is under the "***C:***" drive:

![ 600px | center | MobaXterm choose C:\Temp](/kb3/assets/images/Moba_choose_temp.png
" 600px | center | MobaXterm choose C:\Temp")

Once both have been changed, they should look like this:

![ 600px | center | MobaXterm root and home set to
C:\Temp](/kb3/assets/images/Moba_temp_selected.png
" 600px | center | MobaXterm root and home set to C:\Temp")

Once you click "OK", MobaXterm will need to restart to commit these
changes:

![ 600px | center | MobaXterm restart](/kb3/assets/images/Moba_restart.png
" 600px | center | MobaXterm restart")

#### Installing on Temp Drive of Open Access Lab workstation

**Special Instructions**

Note: This only applies to an unusual circumstance. In most cases,
MobaXterm will already be installed on the OAL workstations. You will
not need to do this on your personal computer or any computer for which
you have privileges to install the software.

If MobaXterm is not installed on an [Open Access
Lab](http://oal.tamu.edu/) workstation, download the portable version
and copy the programs to a folder in the **C:\Temp** folder, i.e.,
**C:\Temp\Moba** (you will need to create this folder first). From
that folder, run the program **MobaXterm\_Portable\_*version*.exe** to
start MobaXterm. Select "Settings" in the top menu and choose "global
settings". In the "General" tab of the settings window, specify
**C:\Temp** as the Persistent home directory and Persistent root
(**/**) directory:

![ 450px | center | MobaXterm choose C:\Temp](/kb3/assets/images/Moba_choose_temp.png
" 450px | center | MobaXterm choose C:\Temp")

Once you have completed this, you should be able to run the portable
version from your home drive without error.

## Access from MacOS

### Using the Terminal Program

Find the Terminal program under Applications->Utilities.

On your Mac click the Finder ![finder.png](/kb3/assets/images/finder.png "finder.png") icon
to start finder:

1.  Select Applications ![app-icon.jpg](/kb3/assets/images/app-icon.jpg "app-icon.jpg")
2.  Double click the Utilities folder
3.  Double click the Terminal utility ![term-icon.jpg](/kb3/assets/images/term-icon.jpg
    "term-icon.jpg")
4.  A Terminal window will now appear.
5.  Connect to the cluster using [ SSH](#access-using-ssh "wikilink").

### Remote Display of Programs with Graphical Interfaces

The recommended X-Windows emulator for Mac OS X is XQuartz, which is
available for free from [the XQuartz Project](http://www.xquartz.org/).

1.  After XQuartz is installed on your system, start XQuartz.
2.  An xterm window should appear on your screen.
3.  Login to the desired cluster (example: `grace.tamu.edu`).
        ssh -X netID@grace.tamu.edu
    The `-X` option tells SSH to allow programs to forward and display
    their graphical interfaces. This is known as X11 forwarding.
4.  To verify that X11 forwarding is working, type the following
    command:
        xterm
    If a new xterm terminal window for the remote system pops up, then
    X11 forwarding is working correctly.

## Access from Linux/Unix

[OpenSSH](http://www.openssh.com/) is an SSH v1.x and v2.x compliant SSH
package that is available for many Linux and Unix operating systems and
is " ...freely usable and re-usable by everyone under a BSD license...
". OpenSSH also includes secure copy (scp), which may be used instead of
ftp. It is available from:
<ftp://ftp.openssh.com/pub/OpenBSD/OpenSSH/portable/>.

### Using the Terminal

If you are using a UNIX based system (IRIX, Linux, SunOS, etc), open a
terminal window and connect to the cluster using [
SSH](#access-using-ssh "wikilink").

### Remote Display of Programs with Graphical Interfaces

Typically, if you use a graphical login screen to login a Linux or Unix
system, then the system is already running a X11 server. You will need
to login with SSH to the cluster in a slightly different manner:

    ssh -X NetID@ada.tamu.edu

The `-X` option tells SSH to allow programs to forward and display their
graphical interfaces. This is known as X11 forwarding. To verify that
X11 forwarding is working, type the following command:

    xterm

If a new xterm terminal window for the remote system pops up, then X11
forwarding is working correctly.
