# Grace Hardware Overview

**Grace: A Dell x86 HPC Cluster**

![caption](/kb3/assets/images/Grace-racks.jpg "caption")

<table>
<tbody>
<tr class="odd">
<td><p>System Name:</p></td>
<td><p>Grace</p></td>
</tr>
<tr class="even">
<td><p>Host Name:</p></td>
<td><p>grace.hprc.tamu.edu</p></td>
</tr>
<tr class="odd">
<td><p>Operating System:</p></td>
<td><p>Linux (CentOS 7)</p></td>
</tr>
<tr class="even">
<td><p>Total Compute Cores/Nodes:</p></td>
<td><p>44,656 cores<br />
925 nodes</p></td>
</tr>
<tr class="odd">
<td><p>Compute Nodes:</p></td>
<td><p>800 48-core compute nodes, each with 384GB RAM<br />
100 48-core GPU nodes, each with two A100 40GB GPUs and 384GB RAM<br />
9 48-core GPU nodes, each with two RTX 6000 24GB GPUs and 384GB RAM<br />
8 48-core GPU nodes, each with 4 T4 16GB GPUs<br />
8 80-core large memory nodes, each with 3TB RAM</p></td>
</tr>
<tr class="even">
<td><p>Interconnect:</p></td>
<td><p>Mellanox HDR 100 InfiniBand</p></td>
</tr>
<tr class="odd">
<td><p>Peak Performance:</p></td>
<td><p>6.2 PFLOPS</p></td>
</tr>
<tr class="even">
<td><p>Global Disk:</p></td>
<td><p>5PB (usable) via DDN Lustre appliances for general use<br />
1.4PB (usable) via Lenovo DSS GPFS appliance (purchased by and dedicated for Dr. Junjie Zhang's CryoEM Lab)<br />
1.9PB (usable) via Lenovo DSS GPFS appliance (purchased by and dedicated for Dr. Ping Chang's iHESP Lab)</p></td>
</tr>
<tr class="odd">
<td><p>File System:</p></td>
<td><p>Lustre and GPFS</p></td>
</tr>
<tr class="even">
<td><p>Batch Facility:</p></td>
<td><p><a href="http://slurm.schedmd.com/">Slurm by SchedMD</a></p></td>
</tr>
<tr class="odd">
<td><p>Location:</p></td>
<td><p>West Campus Data Center</p></td>
</tr>
<tr class="even">
<td><p>Production Date:</p></td>
<td><p>Spring 2021</p></td>
</tr>
</tbody>
</table>

Grace is an Intel x86-64 Linux cluster with 925 compute nodes (44,656
total cores) and 5 login nodes. There are 800 compute nodes with 384 GB
of memory, and 117 GPU nodes with 384 GB of memory. Among the 117 GPU
nodes, there are 100 GPU nodes two A100 40 GB GPU cards, 9 GPU nodes
with two RTX 6000 24GB GPU cards, 8 GPU nodes with four T4 16GB GPU
cards. These 800 compute nodes and 117 GPU nodes are a dual socket
server with two Intel 6248R 3.0GHz 24-core processors, commonly known as
Cascade Lake. There are 8 compute nodes with 3 TB of memory and four
Intel 6248 2.5 GHz 20-core processors.

The interconnecting fabric is a two-level fat-tree based on HDR 100
InfiniBand.

High performance mass storage of 5 petabyte (usable) capacity is made
available to all nodes by the DDN Lustre storage. Also, 3.3 PB of Lenovo
DSS GPFS storage is for their respective research labs.

Get details on using this system, see the [ User Guide for
Grace](/kb3/User-Guides/Grace/Grace/ "wikilink").

## Compute Nodes

A description of the four types of compute nodes is below:

<table>
<caption>Table 1 Details of Compute Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>General 384GB<br />
Compute</p></th>
<th><p>GPU A100<br />
Compute</p></th>
<th><p>GPU RTX 6000<br />
Compute</p></th>
<th><p>GPU T4<br />
Compute</p></th>
<th><p>Large Memory 3TB<br />
Compute</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Total Nodes</p></td>
<td><p>800</p></td>
<td><p>100</p></td>
<td><p>9</p></td>
<td><p>8</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>Processor Type</p></td>
<td><p>Intel Xeon 6248R (Cascade Lake), 3.0GHz, 24-core</p></td>
<td><p>Intel Xeon 6248 (Cascade Lake), 2.5 GHz, 20-core</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Sockets/Node</p></td>
<td><p>2</p></td>
<td><p>4</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Cores/Node</p></td>
<td><p>48</p></td>
<td><p>80</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory/Node</p></td>
<td><p>384GB DDR4, 3200 MHz</p></td>
<td><p>3TB DDR4, 3200 MHz</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Accelerator(s)</p></td>
<td><p>N/A</p></td>
<td><p>2 NVIDIA A100 40GB GPU</p></td>
<td><p>2 NVIDIA RTX 6000 24GB GPU</p></td>
<td><p>4 NVIDIA T4 16GB GPU</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Interconnect</p></td>
<td><p>Mellanox HDR100 InfiniBand</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Local Disk Space</p></td>
<td><p>1.6TB NVMe (/tmp), 480GB SSD</p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Usable Memory for Batch Jobs

While nodes on Grace have either 384GB or 3TB of RAM, some of this
memory is used to maintain the software and operating system of the
node. In most cases, excessive memory requests will be automatically
rejected by SLURM.

The table below contains information regarding the approximate limits of
Grace memory hardware and our suggestions on its use.

<table>
<caption>Memory Limits of Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>384GB Nodes (Regular and GPU)</p></th>
<th><p>3TB Nodes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Node Count</p></td>
<td><p>917</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>Number of Cores</p></td>
<td><p>48 Cores</p></td>
<td><p>80 Cores</p></td>
</tr>
<tr class="odd">
<td><p>Memory Limit<br />
Per Core</p></td>
<td><p>7500 MB<br />
~7.5 GB</p></td>
<td><p>37120 MB<br />
36.25 GB</p></td>
</tr>
<tr class="even">
<td><p>Memory Limit<br />
Per Node</p></td>
<td><p>368640 MB<br />
360 GB</p></td>
<td><p>2969600 MB<br />
2900 GB</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Login Nodes

The **grace.hprc.tamu.edu** hostname can be used to access the Grace
cluster. This translates into one of the five login nodes,
**grace\[1-5\].hprc.tamu.edu**. To access a specific login node use its
corresponding host name (e.g., grace2.hprc.tamu.edu). All login nodes
have 10 GbE connections to the TAMU campus network and direct access to
all global parallel (Lustre-based) file systems. The table below
provides more details about the hardware configuration of the login
nodes.

<table>
<caption>Table 2: Details of Login Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>NVIDIA A100 GPU</p></th>
<th><p>NVIDIA RTX 6000 GPU</p></th>
<th><p>NVIDIA T4 GPU</p></th>
<th><p>No GPU</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hostnames</p></td>
<td><p>grace1.hprc.tamu.edu</p></td>
<td><p>grace2.hprc.tamu.edu</p></td>
<td><p>grace3.hprc.tamu.edu</p></td>
<td><p>grace4.hprc.tamu.edu<br />
grace5.hprc.tamu.edu</p></td>
</tr>
<tr class="even">
<td><p>Processor Type</p></td>
<td><p>Intel Xeon 6248R 3.0GHz 24-core</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory</p></td>
<td><p>384GB DDR4 3200 MHz</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Total Nodes</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>Cores/Node</p></td>
<td><p>48</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Interconnect</p></td>
<td><p>Mellanox HDR100 InfiniBand</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Local Disk Space</p></td>
<td><p>per node: two 480 GB SSD drives, 1.6 TB NVMe</p></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Mass Storage

  - 5PB (usable) with Lustre provided by DDN ES200NV appliance and two
    ES7990X appliances
  - 1.4PB (usable) with GPFS provided by Lenovo's DSS-G220 appliance
  - 1.9PB (usable) with GPFS provided by Lenovo's DSS-G230 appliance

## Interconnect

Two level fat tree topology with Mellanox HDR100:

  - There are 5 core switches and 11 leaf switches.
  - Each leaf switch has 2 Mellanox HDR InfiniBand (200Gb/s) uplinks to
    each core switch.
  - There are up to 80 compute nodes attached to each leaf switch.
  - Each login or compute node has a single Mellanox HDR100 InfiniBand
    (100Gb/s) link to a leaf switch.
  - The DDN storage has 12 total HDR100 links.
  - The Lenovo DSS-G220 storage (Dr. Junjie Zhang's CryoEM Lab) has 8
    HDR100 links.
  - The Lenovo DSS-G230 storage (Dr. Ping Chang's iHESP Lab) has 8 EDR
    links (100Gb/s).

## Namesake

"Grace" is named for [Grace
Hopper](https://en.wikipedia.org/wiki/Grace_Hopper).
