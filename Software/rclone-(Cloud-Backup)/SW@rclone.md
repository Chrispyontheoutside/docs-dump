# rclone

rclone is a tool for syncing files from HPRC systems to remote storage
sites like Google Drive, Dropbox, Amazon's AWS and many more. rclone is
available on ada, terra and HPRC Lab workstations. No module is required
for any of them. If you are using this from ada or terra, then you
probably want to use the fast transfer nodes (ftns) (i.e.
ada-ftn1.tamu.edu, ada-ftn2.tamu.edu and terra-ftn.hprc.tamu.edu \[note
the 'hprc' in the last one\]).

### Configure rclone for your Google Drive

  - configure rclone for your destination, in this case your Google
    Drive (TAMU or not)

<!-- end list -->

    rclone config

1.  choose: n) New remote
2.  pick a name for the drive. e.g. mygdrive
3.  choose the type, in this example we use 11) Google Drive
4.  select the default (blank) option for the following
5.  leave Google Application Client Id blank (default)
6.  leave Google Application Client Secret blank (default)
7.  choose: 1) Full access to all files
8.  leave root\_folder\_id blank (default)
9.  leave service\_account\_file blank (default)
10. when it ask if you want to auto\_config, answer 'n' or 'N' for no
11. at this point, rclone will provide a URL for you to log into in
    order to get an access code. Open the URL in your local browser and
    login (in this case to Google). If successful, you will get an
    access code. Copy/paste the code to the rclone prompt: Enter
    verification code\>
12. this example is for a non-team drive so answer 'n' to the 'Configure
    this as a team drive?' prompt
13. review settings and choose 'y' to save
14. choose 'q' to exit rclone config

<!-- end list -->

  - These settings will be stored in $HOME/.config/rclone/rclone.conf
    and can be transferred between systems as needed if you don't want
    to run 'rclone configure' again. Be sure to keep them secure.

### Use rclone with your Google Drive

  - see the rclone man page and --help screen for other commands
  - here's a simple backup of one's $HOME directory (from terra)

<!-- end list -->

    rclone copy $HOME mygdrive:home-terra

  - in your local browser watch as new files are created on your remote
    storage
  - to update your image (as needed) use something like

<!-- end list -->

    rclone sync $HOME mygdrive:home-terra

\[more to come\]

### Google Team Drives

  - use the steps above
  - think of a good (short/easy) name for the team drive you are about
    to choose
  - when prompted to use a team drive, choose 'y'
  - you will be given a menu of team drives that you have access to,
    choose one
  - continue like above

### Configure rclone for your Microsoft Onedrive

You can access [TAMU Microsfot
Onedrive](https://it.tamu.edu/services/email-messaging-and-collaboration/collaboration/microsoft-onedrive/)
using rclone. This configuration require accessing a web browser. We
recommend you request a vncjob via [portal](/kb3/Software/Portal/SW@Portal/ "wikilink"), or
copy configuration from your local Linux (~/.config/rclone/rclone.conf)
to your cluster home directory.

1.  Start rclone configuration

` rclone config`

1.  choose: n) New remote
2.  pick a name for the drive. e.g. myonedrive
3.  choose the type, in this example we use 26) Microsoft Onedrive
4.  select the default (blank) option for the following
      - leave "OAuth Client Id" blank (default)
      - leave "OAuth Client Secret" blank (default)
5.  select "1/ Microsoft Cloud Global" (default "global") for national
    cloud region for OneDrive
6.  select "No" (default) for "Edit advanced config"
7.  select "Yes" (default) for "Use auto config"
8.  then open URL provided in a browser with URL like
    <http://127.0.0.1:53682/auth?state=some_hash_string>. Note that the
    web browser must be running from the same server where you run
    "rclone" command.
    1.  you will be prompt to login Microsoft One drive by providing
        "NetID@tamu.edu"
    2.  enter your TAMU NetID Password
    3.  provide DUO token
    4.  you will then get a message "Approval required" (for accessing
        your files). Provide a short description for your request. Then
        click on "Request approval". You will receive an email (to your
        TAMU email address) for your request.
    5.  after you receive the approval email, then start over the
        process (starting from step one "rclone config")
9.  after getting "Success" message in the browser, select "1/ OneDrive
    Personal or Business" for "Type of connection"
10. select "Yes" (default) for accessing "root" drive (sample URL
    "<https://tamucs-my.sharepoint.com/personal/netid_tamu_edu/Documents>")
11. select "Yes" (default) to accept the configuration
12. choose 'q' to exit rclone config

### More information

  - the [rclone home page](https://rclone.org/) includes more
    information on services like Dropbox and Amazon AWS S3 and many
    more.
