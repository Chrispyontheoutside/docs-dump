# Terra File Systems, Quotas and File Transfers


## File Space

Global file space on Terra is available on all compute and login nodes.
It is organized in the two file systems showing in the table below.
Access to the allocated file space is through the indicated directories
that are setup automatically for every user.

| File System | Directory           | Environment Variable | Storage Hardware | File Space Quota | File Counts Quota | Comments                                                                                                                                                                                                                                                                                                               |
| ----------- | ------------------- | -------------------- | ---------------- | ---------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Home        | /home/$USER         | $HOME                | DSS-G260         | 10 GB            | 10000             | Upon login, you will be situated in **/home/$USER**. The use of this area is for small-to-modest amount of processing. Its space and file count limits are not extensible. **This area is backed up on a nightly basis.**                                                                   |
| Scratch     | /scratch/user/$USER | $SCRATCH             | DSS-G260         | 1 TB             | 250000            | This is a high performance storage, intended to temporarily hold rather large files, and only for on-going processing that uses them. **It is NOT backed up nor is it intended as long-term storage area.** Please delete or move out of these area any files that are not frequently used. |

## Quotas & File Use

A user can run the *showquota* home-wrapper command to display file
usage on Terra. Below is a sample output of command *showquota*.

`[NetID@terra1 ~]$ `**`showquota`**  
`Your current disk quotas are:`  
`Disk       Disk Usage      Limit    File Usage      Limit`  
`/home          12.75M        10G           120      10000`  
`/scratch         1.5M         1T            15      250000`

## Transferring Files

Data transfer utilites [scp,
sftp](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#scp/sftp "wikilink"), and
[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink") are available Terra login
nodes. All Terra login nodes have 10 Gigbit Ethernet connection to the
intra-campus network. These are suitable for small-to-medium sized data
transfers, as transfer could be interrupted by 60 minute CPU process
time limit on the Terra login nodes. We suggests
"[rsync](/kb3/Helpful-Pages/File-Transfer/HPRC@File_Transfers/#rsync "wikilink")" which supports resume
transfer. For transferring large amount of data, use
*terra-ftn.hprc.tamu.edu* as host name, or use [Globus
Connect](/kb3/Software/Globus-Connect/SW@GlobusConnect/ "wikilink") with "TAMU terra-ftn" as the
endpoint.

For transferring files on Terra to/from a Windows machine, please use
[WinSCP](/kb3/Helpful-Pages/Access/HPRC@Access/#access-from-windows/#winscp "wikilink").


<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/oCSzuJf6p7g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>