# File Transfer on HPRC Clusters

### File Transfer Software

There are several options for choosing a software to transfer files to
and from HPRC clusters. The choice is largely depending on many factors,
such as size, location, transfer frequency, etc. If the data size is
small (transfer time is less than an hour), just pick a software
convenient/familiar to you.

#### Globus Connect

[Globus Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") is a reliable,
high-performance file transfer platform allowing users to transfer large
amounts of data seamlessly between systems or endpoints. Users can
schedule transfer via a web interface on globus.org and receive
notification after transfer is completed. The endpoint can be systems
with Globus installed (like terra-ftn) or user's personal desktop.

  - *What Globus Connect is good at*
      - transfer large amount of data (say 100+ GB)
      - it's fast (utilizing up to 4 data streams); as fast as the
        slowest link from your server/desktop/laptop to HPRC fast
        transfer nodes
      - transfer files between two endpoints (for example, between Grace
        and Terra, or between Grace and endpoint on your laptop)
      - personal endpoint works behind NAT (Network Address Translation;
        like your desktop behind a wifi router at home)
      - resume for failed transfers
      - can
        [sync](https://docs.globus.org/how-to/get-started/#request_a_file_transfer)
        directories (similar to rsync)
      - receive a email notification after a scheduled transfer is
        completed

<!-- end list -->

  - *What Globus Connect is not good at*
      - your server or desktop/laptop must have Globus Connect software
        installed and setup as an endpoint
      - ~~by default, data stream is not encrypted~~ encryption has been
        turned on by default as of Jan 14, 2021

<!-- end list -->

  - *How do I use Globus Connect*
      - visit [Globus Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") wiki page
        for more information
      - Globus Connect software is supported on Windows, Mac, and Linux.
      - use endpoints: "TAMU terra-ftn" for Terra cluster, and "TAMU
        grace-dtn" for Grace cluster

#### SCP/SFTP

SCP and SFTP protocols are a means of securely transferring computer
files between a local host and a remote host.

  - *What SCP/SFTP is good at*
      - ubiquitous; simple to use
      - *sftp* offers an interactive interface (command line) to
        download/upload files
      - data stream is encrypted

<!-- end list -->

  - *What SCP/SFTP is not good at*
      - not very fast (file transfer only uses one data stream over SSH
        protocol)

<!-- end list -->

  - *How do I use SCP/SFTP*
      - you can use command line on Linux, Mac or MobaXterm terminal to
        issue scp/sftp command
      - use [WinSCP](https://winscp.net/eng/index.php) on Windows,
        [FileZilla](https://filezilla-project.org/) (use SFTP protocol)
        on Windows or Mac, or use File Transfer panel on MobaXterm. See
        instruction on [ file transfer from
        Windows](/kb3/Helpful-Pages/Access/HPRC@Access/#access-from-windows/#file-transfer-from-windows "wikilink").
        Also, check [instructions on using SCP/SFTP software with
        Duo](/kb3/Helpful-Pages/Two-Factor/Two_Factor/#duo-with-ftp-ssh-clients "wikilink").
      - HPRC cluster login nodes have 60 minutes CPU time limit. Your
        data transfer might get interrupted for moving large amount of
        data. To by pass this problem, use
        [rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") or use data
        transfer nodes ("terra-ftn.hprc.tamu.edu" for Terra,
        "grace-dtn1.hprc.tamu.edu", "grace-dtn2.hprc.tamu.edu" for
        Grace), which do not have CPU time limit.
      - check [scp man
        page](http://man7.org/linux/man-pages/man1/scp.1.html) and [sftp
        man page](http://man7.org/linux/man-pages/man1/sftp.1.html) for
        options and examples
      - Note two factor authentication has been enabled on Nov 4, 2019.
        Please see [ two factor authentication wiki
        page](/kb3/Helpful-Pages/Two-Factor/Two_Factor/ "wikilink") on how to use two factor for some
        software listed above.

#### FTP

File Transfer Protocol (FTP) protocol is used to transfer files between
a client a server. FTP is not as popular as it was.
[NCBI](https://www.ncbi.nlm.nih.gov/pmc/tools/ftp/) still uses FTP to
transfer data. FTP protocol transfers user name, password, and data
unencrypted. Users should choose FTPS, whose password is transferred
over encrypted channel, whenever possible.

  - *What FTP is good at*
      - FTP client offers an interactive interface (command line) to
        download/upload files
      - data stream is not encrypted, thus data transfer rate is faster
        than SCP/SFTP

<!-- end list -->

  - *What FTP is not good at*
      - FTP protocol doesn't encrypt password and data transfer, thus
        less secure
      - require FTP server at remote server

<!-- end list -->

  - *How do I use FTP*
      - [lftp](https://lftp.yar.ru/lftp-man.html) is available on
        Grace/Terra as a module. Run "module load lftp" to load the
        module.
      - On FTN nodes, you can lunch lftp via absolute path (Terra:
        /sw/eb/sw/lftp/4.8.4-GCCcore-6.4.0/bin/lftp). To find the
        up-to-date path of lftp, first run "module load lftp" on Terra
        login nodes, then run "which lftp" to find the path of lftp.

#### rsync

[rsync](https://rsync.samba.org/) is a fast, versatile, remote (and
local) file-copying tool and recommended when relatively few differences
exist between target and source versions, because rsync copies only the
differences of files that have actually changed. By default, rsync uses
the SSH remote shell.

  - *What rsync is good at*
      - resume file transfer for partial transferred file
      - synchronize files/dirs of two directories (local-local,
        local-remote, remote-local)
      - by default, transfer is over SSH protocol, so data stream is
        encrypted

<!-- end list -->

  - *What rsync is not good at*
      - by default, files transferred over SSH which uses only one data
        stream and not very fast
      - compression option, "-z", might not shorten the transfer time

<!-- end list -->

  - *How do I use rsync*
      - from command line on Linux, Mac, or MobaXterm terminal to issue
        rsync command
      - use
        [DeltaCopy](http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp)
        or [Grsync](https://sourceforge.net/projects/grsync/) on Windows
      - use [cwRsync client](https://www.itefix.net/cwrsync) for command
        line on Windows. [Sample commands of using
        cwRsync](https://www.rsync.net/resources/howto/windows_rsync.html).
      - check [rsync man
        page](http://man7.org/linux/man-pages/man1/rsync.1.html) for
        options and examples
      - Note two factor authentication has been enabled on Nov 4, 2019.
        Please see [ two factor authentication
        wiki](/kb3/Helpful-Pages/Two-Factor/Two_Factor/ "wikilink") page for details.
      - For large files (100G+), you can use additional parameters with
        rsync to shorten the time to resume transfer after rsync
        transfer was interrupted. This example uses Terra FTN as the
        target host.

` rsync -av --partial --inplace --append --progress my_file NetID@tarra-ftn.hprc.tamu.edu:/scratch/user/NetID/`

#### rclone

[rclone](/kb3/Software/rclone-(Cloud-Backup)/SW@rclone/ "wikilink") is a tool for syncing files from HPRC
systems to remote storage sites like Google Drive, Dropbox, Amazon's AWS
and many more.

  - *What rclone is good at*
      - copy data to or from cloud (Google Drive, Dropbox, AWS, etc)

<!-- end list -->

  - *What rclone is not good at*
      - transfer can be slow

<!-- end list -->

  - *How do I use rclone*
      - rclone is available on grace, terra and HPRC Lab workstations.
        No module is required for any of them
      - reference [rclone](/kb3/Software/rclone-(Cloud-Backup)/SW@rclone/ "wikilink") wiki page for
        instructions and examples

#### portal

[HPRC Portal (OnDemand)](/kb3/Software/Portal/SW@Portal/ "wikilink") is a web platform through
which users can access HPRC clusters and services with a web browser.
You can download/upload file via menu "Files".

  - *What portal is good at*
      - web interface and simple to use
      - you can view content (text, image, movie) via web browser

<!-- end list -->

  - *What portal is not good at*
      - transfer large files \>2GB
      - transfer can be slow (file is transfer via single data stream)

<!-- end list -->

  - *How do I use portal*
      - visit <https://portal.hprc.tamu.edu>, or visit
        <https://protal-terra.hprc.tamu.edu> for Terra portal, and
        <https://portal-grace.hprc.tamu.edu> for Grace portal.
      - check [portal](/kb3/Software/Portal/SW@Portal/ "wikilink") wiki page for additional
        info
      - portal is CAS authenticated

### Tutorial Videos

  - [File transfer using WinSCP, MobaXterm, Filezilla, Cyberduck, and
    Open OnDemand portal](https://www.youtube.com/watch?v=oCSzuJf6p7g)
    (March 12, 2021)
  - [File Transfers using Globus
    Connect](https://www.youtube.com/watch?v=_ROApd7MtRQ) (May 13, 2021)

### Host selection

For transferring large files, selecting a better target host could
greatly shorten the data transfer time. TAMU firewall scanning adds a
significant overhead to the data transfer flow through campus firewall.
The table below gives a general guidance of selecting target hosts for
your transfer. The transfer speed is rated "Very Good", "Good+" (a bit
better than "Good"), "Good" and "Fair".

<table>
<thead>
<tr class="header">
<th><p>src/dest</p></th>
<th><p>Terra login</p></th>
<th><p>Terra FTN</p></th>
<th><p>Grace login</p></th>
<th><p>Grace DTN</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>on TAMU campus network</p></td>
<td><p>Very Good</p></td>
<td><p>Fair</p></td>
<td><p>Very Good</p></td>
<td><p>Very Good</p></td>
</tr>
<tr class="even">
<td><p>at home via TAMU VPN</p></td>
<td><p>Good+</p></td>
<td><p>Fair</p></td>
<td><p>Good+</p></td>
<td><p>Good+</p></td>
</tr>
<tr class="odd">
<td><p>HPRC cluster login</p></td>
<td><p>Very Good</p></td>
<td><p>Fair</p></td>
<td><p>Very Good</p></td>
<td><p>Very Good</p></td>
</tr>
<tr class="even">
<td><p>HPRC cluster FTN/DTN</p></td>
<td><p>Fair</p></td>
<td><p>Very Good</p></td>
<td><p>Fair</p></td>
<td><p>Very Good</p></td>
</tr>
<tr class="odd">
<td><p>TACC cluster login</p></td>
<td><p>-</p></td>
<td><p>Very Good</p></td>
<td><p>-</p></td>
<td><p>Very Good</p></td>
</tr>
<tr class="even">
<td><p>other HPC sites</p></td>
<td><p>-</p></td>
<td><p>Very Good<br />
only Globus Connect</p></td>
<td><p>-</p></td>
<td><p>Very Good<br />
only Globus Connect</p></td>
</tr>
</tbody>
</table>

Comments:

  - Unless it's noted, ssh, scp/sftp, and
    [rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") can be used for data
    transfer.
  - [Globus Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") can be used to move
    files between HPRC clusters and other HPC sites. Globus Connect
    command line can be used on FTN/DTN.
  - Terra FTN is outside campus firewall and all HPRC cluster login
    nodes are behind campus firewall. Thus, file transfer from login
    nodes to Terra FTN will be impacted by campus firewall scanning.
    Grace DTNs are behind firewall.

### Other Considerations

  - *What is the best way to move my files between HPRC clusters?*

[Globus Connect](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#globus-connect "wikilink") is the
best option. Use [rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") if you
want sync a directory between two clusters and only a few files
changed/added, or some files were partially transferred / changed.

  - *I am off campus or travel abroad. Can I transfer files from/to HPRC
    cluster?*

All Grace/Terra login nodes are behind TAMU campus firewall, so TAMU VPN
access is required if you are off campus. If you have personal [Globus
Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") endpoint setup on your laptop, you
can transfer files to/from your laptop via globus.org using [Globus
Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink"), without using TAMU VPN.

  - *Should I use FTN or regular Grace/Terra/Grace login nodes to
    transfer files?*

Please see table in [Host
selection](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#host-selection "wikilink") for a quick
summary.

All Terra login nodes (terra.tamu.edu) and Grace login nodes
(grace.hprc.tamu.edu) have 10 Gbps links to HPRC edge switches, which
have dual 10 Gbps link to campus network.

For short file transfer (less than one hour), either data transfer or
login nodes would work. For transfer time over 1 hour, please use data
transfer nodes (terra-ftn.hprc.tamu.edu for Terra cluster;
grace-dtn1.hprc.tamu.edu or grace-dtn2.hprc.tamu.edu for Grace cluster),
which do not have one hour CPU process time limit. Use
[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") when possible, as rsync
supports resume transfer, or use [Globus
Connect](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#globus-connect "wikilink") if moving files
between two clusters.

If you are on campus or transfer small files over VPN, please use
Grace/Terra login nodes (terra.tamu.edu and grace.hprc.tamu.edu) to
transfer your data. If you are off campus, please consider using [Globus
Connect](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#globus-connect "wikilink") to transfer your
data.

If you are using clusters at TACC, you can scp/sftp/rsync to FTN or use
Globus Connect.

  - *Can I download files from internet (say NIH) inside a job script?*

Grace/Terra compute nodes do not have access to internet, so you cannot
download files from internet on the compute node. Please set up [web
proxy](/kb3/Software/Web-Proxy/SW@WebProxy/ "wikilink") in your job script or download necessary
files on Grace/Terra login nodes or DTN/FTN nodes.

  - *I want to back up files to my desktop/laptop.*

[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") or
[rclone](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rclone "wikilink") (to cloud storage)
probably the best choice.

  - *Can I mount my Grace/Terra home/scratch directory on my
    desktop/laptop to transfer files?*

[**SSHFS**](https://en.wikipedia.org/wiki/SSHFS) is the best option.

  - *I have 100+ TB data to transfer.*

Please contact us at help@hprc.tamu.edu. We would like to get more
information first and see how we can support this.

  - *Why the file transfer takes so long?*

This is a complicated question. The file transfer time is largely
depended on data size, bandwidth of the slowest link from HPRC cluster
to your desktop (bottleneck link), how congested/busy the network link
is, and how fast file system can read/write. For 100 Giga Bytes data
transferred over a 100 Mbps link, it will take about 170 min under the
best case scenario (80% efficiency, no cross traffic and no I/O
bottleneck). Often, link speed of network to your desktop/laptop (the
last mile) and storage on your desktop/laptop are the slowest part for
the entire file transfer.

The transfer rate of medium for storing files (spinning disk, SSD,
external disk via USB) could be a limiting factor. Spinning hard drive
typically has a limit of 30~50 MB/sec transfer rate. Most USB storage
(like USB sticks, USB external drive) cannot transfer at max speed of
USB standard (USB 2.0 of 60 MB/sec and USB 3.0 of 640 MB/sec). When
assess overall data transfer rate, be aware of transfer limit from
combinations of storage speed, storage to computer interface (like USB),
network link speed (Wifi or Ethernet), CPU speed (CPU can process
limited number of file system access requests), and internet connecting
speed of your laptop/desktop. Making a few test transfers with small
data set can help you make a (more) reasonable transfer time for a
larger data set.

Number of data transfer streams would make a difference as well. [Globus
Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") utilizes up to 4 data streams to
shorten the transfer time (more noticeable for large files; typically
seeing 2.5x speedup).

  - *I don't see the answer for my file transfer issues.*

Please contact us at help@hprc.tamu.edu with details of your questions.
