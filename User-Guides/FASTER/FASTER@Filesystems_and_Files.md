# FASTER File Systems, Quotas and File Transfers


## File Space

Global file space on FASTER is available on all compute and login nodes.
It is organized in the two file systems showing in the table below.
Access to the allocated file space is through the indicated directories
that are setup automatically for every user.

| File System | Directory                | Environment Variable | Storage Hardware | File Space Quota | File Counts Quota | Comments                                                                                                                                                                                                                                                                                                               |
| ----------- | ------------------------ | -------------------- | ---------------- | ---------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Home        | /home/USERID             | $HOME                | DDN              | 10 GB            | 10000             | Upon login, you will be situated in **/home/$USER**. The use of this area is for small-to-modest amount of processing: small software, scripts, compiling, editing. Its space and file count limits are not extensible. **This area is backed up on a nightly basis.**                      |
| Scratch     | /scratch/user/USERID     | $SCRATCH             | DDN              | 1 TB             | 250000            | This is a high performance storage, intended to temporarily hold rather large files, and only for on-going processing that uses them. **It is NOT backed up nor is it intended as long-term storage area.** Please delete or move out of these area any files that are not frequently used. |
| Project     | /scratch/group/PROJECTID | $PROJECT             | DDN              | 5 TB             | 500000            | This is a high performance storage for specific storage allocation requests. Not purged while allocation is active. Removed 90 days after allocation expiration.                                                                                                                            |

## Quotas & File Use

A user can run the *showquota* home-wrapper command to display file
usage on FASTER. Below is a sample output of command *showquota*.



`[NetID@FASTER1 ~]$ showquota`  
`Your current disk quotas are:`  
`Disk                   Disk Usage      Limit   File Usage      Limit`  
`/home/userid                 1.4G      10.0G         3661      10000`  
`/scratchuser/userid        117.6G       1.0T        24226     250000`  
`/scratch/group/projectid   510.5G       5.0T       128523     500000 `



## Transferring Files

Data transfer utilites [scp,
sftp](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#scp/sftp "wikilink"), and
[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") are available FASTER login
nodes. All FASTER login nodes have 10 Gigbit Ethernet connection to the
intra-campus network. These are suitable for small-to-medium sized data
transfers, as transfer could be interrupted by 60 minute CPU process
time limit on the FASTER login nodes. We suggest
"[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink")" which supports
intermittent transfer. For transferring large amount of data to or from
off campus, use [Globus Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") with "TAMU
FASTER DTN1" or "XSEDE TAMU FASTER" as the endpoint. (The XSEDE endpoint
is restricted to XSEDE users. )

For transferring files on FASTER to/from a Windows machine, you can use
[MobaXterm or
WinSCP](/kb3/Helpful-Pages/Access/HPRC@Access/#file-transfer-from-windows "wikilink"). Please see
[instructions on using SFTP/SCP software with
Duo](/kb3/Helpful-Pages/Two-Factor/Two_Factor/#duo-with-ftp.2c-ssh-clients "wikilink"). Use
[rclone](/kb3/Software/rclone-(Cloud-Backup)/SW@rclone/ "wikilink") to move data to/from cloud storage from
the login nodes.

Please see [file transfer wiki page](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/ "wikilink") for
more details on choices of transfer software and [answers to frequently
asked questions](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#other-considerations "wikilink").
