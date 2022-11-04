# Terra Accessing

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

| Cluster    | Hostname             | Number of login nodes  | Credential (UserID / Password) |
| ---------- | -------------------- | ---------------------- | ------------------------------ |
| **Terra**  | terra.tamu.edu       | 3 (terra1 ~ terra3)   | NetID / NetID password         |
| **Grace**  | grace.hprc.tamu.edu  | 5 (grace1 ~ grace5)   | NetID / NetID password         |
| **FASTER** | faster.hprc.tamu.edu | 4 (faster1 ~ faster4) | NetID / NetID password         |

Table 1: Hostname and credential info of HPRC clusters

<p align="center">
<iframe width="520" height="275" src="https://www.youtube.com/embed/KjHwfZI_ej4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

### Off-campus Access

For connecting to cluster login nodes from outside the campus, you need
to activate Virtual Private Network (VPN) first, then initiate SSH
connection to the cluster login nodes. You can find VPN installation
instruction from [TAMU ServiceNow Knowledge Base page on
VPN](https://tamu.service-now.com/tamu-selfservice/knowledge_detail.do?sysparm_document_key=kb_knowledge,02ce68792badc6009b4c26e405da151e).

<span style="color:red"> **WSL and Windows Users Attention:**</span>
There is a known issue which users use WSL on Windows 11 with VPN and
cannot log into cluster at this time. You will instead need to use
PowerShell or the provided Shell Access via the portal.

1\. PowerShell: you will use syntax similar to when you use WSL. For
example: To access Grace, you will use "ssh
\[NetID\]@grace.hprc.tamu.edu"

2\. Shell Access via the portal: you will access portal.hprc.tamu.edu
and choose portal (Grace or Terra. On the top bar, choose "Clusters"
then choose the "Shell Access" option.

### Two Factor Authentication Requirement

Starting October 1, 2018, the Division of Information Technology will
require use of Duo NetID Two Factor Authentication on its Virtual
Private Network (VPN) (connect.tamu.edu) service.

Duo provides a second layer of security to Texas A\&M accounts.

If you are not already enrolled in Duo and plan to use VPN, you can
enroll now at duo.tamu.edu. Enrolling is as easy as 1-2-3:

1\. Choose your device and download the Duo Mobile app. (We strongly
recommend the mobile app as the most user-friendly option.)

2\. Start your enrollment at <https://gateway.tamu.edu/duo-enroll/>;

3\. Remember: Once you sign up, you will need your Duo-enrolled device
when you log in to most Texas A\&M resources.

For more information, consult IT's knowledge base article for Duo:
<https://u.tamu.edu/KB0012105>

## Detailed Access Information

For more in-depth information on accessing the TAMU HPRC clusters and
guides for configuring your SSH client, see the [ Detailed
Access](/kb3/Helpful-Pages/Access/HPRC@Access/ "wikilink") page.

## Terra-Specific Information

### Login Nodes

There are a total of three Terra login nodes. Connecting to
terra.tamu.edu will direct you to one of the three nodes based on a
round-robin queue.

You can connect to a particular node by utilizing the node-specific
names. For example, to connect to Terra login node 2:

`[user1@localhost ~]$ `**`ssh   `*`[NetID]`*`@terra.tamu.edu`**

To see information on the Terra login node configurations, see the
[Terra Login Node Hardware](/kb3/User-Guides/Terra/Terra@Intro/#login-nodes "wikilink") section
of the [Terra Hardware Introduction](/kb3/User-Guides/Terra/Terra@Intro/ "wikilink") page.
