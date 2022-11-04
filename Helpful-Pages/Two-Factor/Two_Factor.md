## Logging in With Two-Factor Authentication

**Starting November 4th, 2019, two-factor authentication will be
required to login to any cluster.**

This is most commonly done with Duo, which can be set up by following
[these
instructions](/kb3/Helpful-Pages/Two-Factor/IT_Info/).

When enabled, the login prompt will add the following information
following successful password entry:

    Duo two-factor login for netid
    
    Enter a passcode or select one of the following options:
    
     1. Duo Push to XXX-XXX-1234
     2. Phone call to XXX-XXX-1234
     3. SMS passcodes to XXX-XXX-1234 (next code starts with: 9)
    
    Passcode or option (1-3):

Any option can be selected. After successfully using Duo two-factor
authentication, you will see the following message, be logged into your
home directory, and can resume normal use.

    Success. Logging you in...

## Duo With FTP, SSH Clients

Before the implementation of two-factor authentication, FTP clients such
as Filezilla or MobaXterm simply needed to send a username and password
to successfully login. However, with the integration of Duo into the
login process, the clusters must also send a prompt to select which form
of two factor authentication to use. This extra step in the process
requires some reconfiguring of the FTP client in order to successfully
login.

**NOTE: If you are facing issues with login, please ensure that your
password is not saved in your FTP client, as this will not allow Duo to
function properly.**

### FileZilla

**NOTE: FileZilla is known to require a two factor authentication for
each file needing to be transferred. Due to this inefficiency, FileZilla
is no longer recommended for file transfers.**

1\. From the menu bar at the top of the screen select Site Manager  
![ 700px | center](/kb3/assets/images/Fz-0.png)

2\. Click the 'New Site' button  
![ 700px | center](/kb3/assets/images/Fz-1.png)

3\. In the General settings tab, set the protocol to SFTP - SSH File
Transfer Protocol  
![ 700px | center](/kb3/assets/images/Fz-2.png " 700px | center")

4\. Set the host to the hostname of the cluster you're attempting to
connect to (e.g. ada.tamu.edu)

5\. Set the port to 22  
![ 700px | center](/kb3/assets/images/Fz-3.png " 700px | center")

6\. Set the logon type to 'Interactive'

6b. In the same windows, click on "Transfer Settings" tab. Then check
Limit the number of simultaneous connection.  
Make sure the maximum number of connections is set to 1. ![ 700px |
center](/kb3/assets/images/Fz-6b.png " 700px | center")

7\. In the resulting dialog, select 'Do Not Save Passwords'  
![ 700px | center](/kb3/assets/images/Fz-4.png " 700px | center")

8\. In the next dialog, enter your NetID (NOT your UIN and NOT your full
email)

9\. If an 'Unknown host key' dialog appears, just click 'OK'  
![ 700px | center](/kb3/assets/images/Fz-5.png " 700px | center")

10\. Press 'Connect'.  
![ 700px | center](/kb3/assets/images/Fz-6.png " 700px | center")

11\. Continuing with login, an 'Enter password' dialog should appear.
Enter your NetID password.  
![ 700px | center](/kb3/assets/images/Fz-7.png " 700px | center")

12\. A second 'Enter password' dialog will appear with the duo two
factor authentication prompt. Choose your preferred option by entering
the corresponding number into the password field, then click 'OK'  
![ 700px | center](/kb3/assets/images/Fz-8.png " 700px | center")

13\. On the secondary authentication device (e.g. mobile phone) approve
the notification/phone call, and you will be logged into the cluster  
![ 700px | center](/kb3/assets/images/Fz-9.png " 700px | center")

### MobaXterm (Windows only)

#### Option 1:

1\. On the top left corner of MobaXterm window, click 'Session'
button.  
![ 700px | center](/kb3/assets/images/moba-0.png " 700px | center")

2\. You will be prompted with a window which asks for your session
settings.

3\. Enter the 'Remote Host' (e.g. ada.tamu.edu, terra.tamu.edu, etc.)
you would like to connect to.

4\. Select 'Specify', then enter your username (your NetID).

5\. Enter the 'Port Number' 22 (the default should be 22).  
![ 700px | center](/kb3/assets/images/moba-1.png " 700px | center")

6\. Press enter.

7\. You will be prompt to authentication with Duo (either using mobile
app, text message or call).

8\. If you wish to open the session again, open the 'Session' tab on the
left side of the screen and double-click the appropriate session to
launch.  
![ 700px | center](/kb3/assets/images/moba-2.png " 700px | center")

#### Option 2:

1\. Select 'Start Local Terminal' in the home tab. ![ 800px |
center](/kb3/assets/images/Mobalocal.png " 800px | center")

2\. Type 'ssh NetID@cluster.tamu.edu', replacing the netID and cluster
fields appropriately.

3\. You will be prompted for your password with
"netID@cluster.tamu.edu's password:." Do NOT type your password yet.
Press 'Enter' until you are prompted with just "Password:."

4\. Finally, type in your password and select a choice for Duo
Authentication, once prompted.

![ center](/kb3/assets/images/Twofactor.png " center")

**File Transfer**

1\. On the top left corner of MobaXterm window, click Session button.

2\. Choose 'SFTP' session type.

3\. Enter remote host (e.g. ada.tamu.edu, terra.tamu.edu, etc.) and
username (your netID).

4\. Go to 'Advanced Sftp settings' and check '2-steps authentication'
checkbox.

5\. Select 'Ok' to finish configuration of the SFTP session.

6\. When you login with this SFTP session, there will be **TWO** pop-up
windows.

  - The first pop-up window will ask you for your password. Enter your
    TAMU password here.

![ 400px | center](/kb3/assets/images/Mobaxterm_password_prompt.png " 400px | center")

  - A second pop-up window will say "Duo two-factor login for NetID".
    Enter a number corresponding to one of your configured
    authentication methods (Push, Call, Text, Second device, etc).
    Select the appropriate option. **Do not type your TAMU password
    again here.**

![ 800px | center](/kb3/assets/images/Mobaxterm_duo_prompt.png " 800px | center")

**Here are example Duo Authentication methods that would be shown when
you SSH to a HPRC cluster login node. You won't see this, it is just to
remind you of the numbering format of Duo Authentication menu options.**

    Enter a passcode or select one of the following options:
    
     1. Duo Push to XXX-XXX-1234
     2. Duo Push to iOS
     3. Phone call to XXX-XXX-1234

**Your Duo settings will be different.**

### WinSCP (Windows only)

1\. Open WinSCP. Click on new section located on the menu bar.

2\. The above step will open the login windows.

3\. Enter your relevant information (hostname: ada.tamu.edu,
terra.tamu.edu, username, password, etc.)

4\. Your will be shown our authentication banner. Click continue.

5\. Another windows will be opened (Server prompt) asking for your duo
options (text, push, phone call, etc.) Select what is appropriate for
your case.

6\. Press Ok.

**Note: In most cases, the above steps should work. If they don't please
follow these steps.**

3b. Starting with step 3. In the login windows, after you have entered
your information (username, password, etc.) Click on advanced.

4b. On the left pannel of Advanced Site Settings, select authentication.
Check on "Attempt 'keyboard-interactive' authentication. Also select
'response with password to the first prompt'. Press Ok.

5b. Resume with step 3 specified in the above section.

### File Transfer via Web Portal

An alternative option for file transfer is to use our web portal.

1\. Go to <https://portal.hprc.tamu.edu>

2\. Select the appropriate cluster.

3\. On the top left corner of the website, you will see "Files". Click
on Files menu.

4\. Select the desired directory. This will open a new tab in your web
browser.

5\. In the new tab, you should be able to manipulate (download, upload,
modify files) via the web interface.

For more information about OnDemand portal, please visit this
[link](/kb3/Software/Portal/SW@Portal/)

### FAQ

1\. My account is locked after several login attempts, what can I do?

Your account will be locked after 7 failed login attempts. It will be
automatically unlocked after 10 minutes. Please refer to above sections
for updated instructions on how to use SSH, SFTP clients with duo
authentication enabled.
