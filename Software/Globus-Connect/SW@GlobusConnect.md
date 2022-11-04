# Globus Connect

Globus Connect is a reliable, high-performance file transfer platform
allowing users to transfer large amounts of data seamlessly between
systems or endpoints. Users can schedule transfer via a web interface
and receive notification after transfer is completed. The endpoint can
be systems with Globus installed (like terra-ftn) or user's personal
desktop.

### Access Globus Connect

Globus has a good tutorial on [How To Log In and Transfer Files with
Globus](https://docs.globus.org/how-to/get-started/)

  - Go to [globus.org login page](https://app.globus.org/). Select
    "Texas A & M University" from the drop down menu, under "Use your
    existing organizational login", and then login with NetID.

Optional, you can install [Globus Connect
Personal](https://www.globus.org/globus-connect-personal) on your
desktop. Follow instruction from Globus web site.

  - [Globus Connect Personal for
    Mac](https://docs.globus.org/how-to/globus-connect-personal-mac) for
    Mac OS X 10.4 or higher (Intel only)
  - [Globus Connect Personal for
    Linux](https://docs.globus.org/how-to/globus-connect-personal-linux)
    for common x86-based distributions
  - [Globus Connect Personal for
    Windows](https://docs.globus.org/how-to/globus-connect-personal-windows)

### Data Transfer

  - Select an endpoint (or "collection"), where data locates
      - For Terra, search "TAMU" in "Collection" and use "TAMU
        terra-ftn" as endpoint.
      - For Grace, search "TAMU" in "Collection" and use "TAMU
        grace-dtn" as endpoint.
      - For FASTER, search "TAMU" in "Collection" and use "TAMU FASTER
        DTN1" as endpoint for TAMU users. "XSEDE TAMU FASTER" for XSEDE
        users.
  - You might be asked to login with your NetID/NetID Password if you
    login globus.org web page with Globus ID
  - The default directory is your home directory. To access your scratch
    directory, enter "/scratch/user/YourNetID" in the Path.
  - Drag and Drop file or directory as needed.
  - Under "Transfer & Sync Options", you can choose
    "[sync](https://docs.globus.org/how-to/get-started/#request_a_file_transfer)"
    to transfer new or changed files. The default is "transfer". You can
    also enable "preserve source file modification times" to preserve
    modification date of the source file. Note that date and permission
    of the directories are not preserved. You can run
    [rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink")" afterward to update
    the modification date and permission if needed.
  - After transfer is completed, you should receive an email
    notification.

### Globus GUI connectivity to One Drive

Onedrive now provides 10TB storage space for all tamu.edu registered
accounts. You can follow the steps provided in this
[video](https://www.youtube.com/watch?v=_ROApd7MtRQ) to transfer your
files from one TAMU end point to another.

  - To transfer your files from Grace or Terra, choose one of the
    endpoints as "TAMU Grace - dnt" or "TAMU Terra - fnt."
  - Set "TAMU AIP Azure OneDrive Globus Storage Collection" as second
    endpoint.

![GlobusOneDrive.JPG](/kb3/assets/images/GlobusOneDrive.JPG "GlobusOneDrive.JPG")

  - Authenticate OneDrive using your NetID@tamu.edu credential.
  - Execute file transfer as per the instructions in the video.

### Log out Globus Connect

To log out Globus, click on "Account" icon on the left, then "Logout"
button on the top right corner.

### Tutorial Videos

  - [File Transfers using Globus
    Connect](https://www.youtube.com/watch?v=_ROApd7MtRQ) (May 13, 2021)
  - [Globus Connect Personal
    Basics](https://www.youtube.com/watch?v=bpnVcAN99WY) (Aug 27, 2020)
  - [Globus GUI to One
    Drive](https://www.youtube.com/watch?v=_ROApd7MtRQ) (May 13, 2021)

### Globus Command Line Interface (CLI)

Globus CLI is a standalone application that can be installed on the
user’s machine and used to access the Globus service. globus-cli is
written in python and can be installed on Linux/Mac by following this
[installation guide](https://docs.globus.org/cli/installation/) using
"pip". Python 2.7+ or 3.4+ is required.

Once login, user can transfer files between two endpoints, or list
directory on an endpoint. The login session is valid for two days (see
additional note below).

**Useful links:**

  - Installation guide: <https://docs.globus.org/cli/installation/>
  - Installation prerequisites:
    <https://docs.globus.org/cli/installation/prereqs/>
  - Quick Start guide: <https://docs.globus.org/cli/quickstart/>
  - Examples: <https://docs.globus.org/cli/examples/>
  - Reference: <https://docs.globus.org/cli/reference/>
  - Globus CLI home page: <https://docs.globus.org/cli/>

**Additional notes:**

  - "[globus login](https://docs.globus.org/cli/reference/login/)" will
    try to open a web page for CAS authentication. Or user can
    copy/paste the URL onto another browser.
  - After login, globus session is valid for 2 days. You can check
    session status via "[globus session
    show](https://docs.globus.org/cli/reference/session_show/)". After
    two days, "globus session show" will be empty. However, based on our
    testing, a login session is valid for 10 days.
  - To renew your login session, you can use "[globus session
    update](https://docs.globus.org/cli/reference/session_update/)" or
    login web site (https://globus.org globus).

### Note for accessing TACC clusters with Globus Connect

For those using TAMU allocation on TACC clusters, your accounts are not
part of XSede and additional steps are needed for using Globus Connect
at TACC.

  - See instruction "[Using Globus at
    TACC](https://portal.tacc.utexas.edu/tutorials/globus)" on how to
    import DN on TACC's portal.
  - Choose "TACC Stampede" (for non-XSede accounts) as endpoint
