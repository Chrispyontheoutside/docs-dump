# Other

### Q: "What is "Disk Quota Exceeded"?

**A:** This message refers to one or more file quotas being reached.

  - Users are advised to check their quotas regularly with
    **showquota**.
  - **SOLUTION:** Clear out the problem directories of any unnecessary
    files.
  - More information on file systems and quotas can be found on our [
    file systems](/All-Pages/Ada:Filesystems_and_Files/ "wikilink") page.

**Extra Tips:**

  - Some files may be hidden or stored deep within your subdirectories.
  - Hidden files can be seen with the **ls -la** or **tree -a**
    commands.
  - The following commands will show you the number of files within each
    top directory:

<!-- end list -->

    % ml mpifileutils/0.9.1-intel-2019a
    % dwalk mydir
    [2020-06-03T17:33:49] Walking /scratch/user/netid/mydir
    [2020-06-03T17:33:49] Walked 896 items in 0.015395 seconds (58200.092672 files/sec)
    [2020-06-03T17:33:49] Items: 896
    [2020-06-03T17:33:49]   Directories: 12
    [2020-06-03T17:33:49]   Files: 884
    [2020-06-03T17:33:49]   Links: 0
    [2020-06-03T17:33:49] Data: 115.775 GB (134.110 MB per file)

  - The following command will show you the number of files within the
    current directory (first column, ignore second and third): **find .
    | wc**

### Q: "Why does my program stop after 1 hour on the login nodes?"

**A:** Since the login nodes are resources which are constantly shared
by many users, we must enforce limits on computing on the login nodes in
order to prevent irresponsible usage. One of these limits is on CPU
time. **Users are limited to ONE HOUR of CPU time per login session.**
If you need more than one hour of CPU time, you will need to submit a
job to the batch system. More information on batch processing can be
found on our [ batch processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink") page. You are
expected to be **responsible** and **courteous to other users** when
using software on the login nodes.

### Q: "How do I acquire an HPRC account for a Texas A\&M credit-bearing course?"

**A:** Details for creating HPRC accounts for use in connection with a
Texas A\&M University credit-bearing course can be found on our wiki: [
Hosting a Class with HPRC](/kb3/Helpful-Pages/HostingClass/HPRC@HostingClass/ "wikilink")

### Q: "How can I add output to my .bashrc without breaking anything?"

**A:** Avoid messing with your .bashrc if at all possible. However, if
you must add output to your .bashrc to print every time you log into a
machine, add the following boolean:

  if [ "$SSH_TTY" ]
  then  
    # Put output here
  fi

### Q: "How do I set up two-factor authentication?"

**A:** In order to set up two-factor authentication (needed to access
the TAMU VPN and log into CAS), go to <https://duo.tamu.edu/>. There
will be an option to "Enroll/Manage Devices". Clicking this option will
bring you to the CAS login page, where you enter your NetID and
password. Next, you will add a device to use for authentication. Enter
the requested information. Download the Duo Mobile app ([Google
Play](https://play.google.com/store/apps/details?id=com.duosecurity.duomobile&hl=en_US)/[Apple
App Store](https://itunes.apple.com/us/app/duo-mobile/id422663827?mt=8))
on your registered device and log in. Now, whenever you log into a
device through CAS, a request will be sent to your registered device
asking for approval of the log in.

### Q: "My account is locked after failed login attempts (incorrect password, duo related problem), what can I do?"

**A:** Your account will be locked if you failed to provide the correct
password after 7 attempts. It will be unlocked after 10 minutes. You are
also able to specify a different login node. Please be aware that
certain MobaXterm setups might cause problems when duo authentication is
enabled. Please refer to ([Two Factor Authentication wiki
page](/kb3/Helpful-Pages/Two-Factor/Two_Factor/)/) for more information.

### Q: "Application xyz failed to connect to the cluster, what can I do?"

**A:** Starting **November 4th, 2019**, Duo authentication is required
for every SSH login request. This has been known to cause issues with
certain applications. As of this writing, we don't have a complete list
of which applications will have issues when duo authentication is
enabled. Please send us an email at help@hprc.tamu.edu when you
encounter login-related issues with the software you are using. We will
try our best to assist you.

### Q: "How do I unsubscribe from the TAMU HPRC email list?"

**A:** As of right now, the only way to unsubscribe from our mailing
list is to deactivate your HPRC account.
