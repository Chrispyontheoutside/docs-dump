# Terra Hardware Overview

Terra: A Lenovo x86 HPC Cluster

-----

![caption](/kb3/assets/images/Terra-racks.jpg "caption")

<table>
<tbody>
<tr class="odd">
<td><p>System Name:</p></td>
<td><p>Terra</p></td>
</tr>
<tr class="even">
<td><p>Host Name:</p></td>
<td><p>terra.tamu.edu</p></td>
</tr>
<tr class="odd">
<td><p>Operating System:</p></td>
<td><p>Linux (CentOS 7)</p></td>
</tr>
<tr class="even">
<td><p>Total Compute Cores/Nodes:</p></td>
<td><p>9,632 cores<br />
320 nodes</p></td>
</tr>
<tr class="odd">
<td><p>Compute Nodes:</p></td>
<td><p>256 28-core compute nodes, each with 64GB RAM<br />
48 28-core GPU nodes, each with one dual-GPU Tesla K80 accelerator and 128GB RAM<br />
8 68-core KNL nodes with 96GB RAM<br />
8 72-core KNL nodes with 96GB RAM</p></td>
</tr>
<tr class="even">
<td><p>Interconnect:</p></td>
<td><p>Intel Omni-Path Fabric 100 Series switches.</p></td>
</tr>
<tr class="odd">
<td><p>Peak Performance:</p></td>
<td><p>377 TFLOPs</p></td>
</tr>
<tr class="even">
<td><p>Global Disk:</p></td>
<td><p>7PB (raw) via Lenovo's DSS-G260 appliance for general use<br />
1PB (raw) via Lenovo's GSS24 purchased by and dedicated for GEOSAT</p></td>
</tr>
<tr class="odd">
<td><p>File System:</p></td>
<td><p>General Parallel File System (GPFS)</p></td>
</tr>
<tr class="even">
<td><p>Batch Facility:</p></td>
<td><p><a href="http://slurm.schedmd.com/">Slurm by SchedMD</a></p></td>
</tr>
<tr class="odd">
<td><p>Location:</p></td>
<td><p>Teague Data Center</p></td>
</tr>
<tr class="even">
<td><p>Production Date:</p></td>
<td><p>February 2017</p></td>
</tr>
</tbody>
</table>

Terra is an Intel x86-64 Linux cluster with 320 compute nodes (9,632
total cores) and 3 login nodes. There are 256 compute nodes with 64 GB
of memory, 48 compute nodes with 128 GB of memory and a K80 GPU card.
These 304 compute nodes are a dual socket server with two [Intel Xeon
E5-2680 v4 2.40GHz 14-core
processors](https://ark.intel.com/products/91754/Intel-Xeon-Processor-E5-2680-v4-35M-Cache-2_40-GHz),
commonly known as Broadwell. There are also 16 Intel Knights Landing
(KNL) nodes with 96 GB of memory with either 68 or 72 cores per node.

The interconnecting fabric is a two-level fat-tree based on Intel
Omni-Path Architecture (OPA). High performance mass storage of 7.4
petabyte (raw) capacity is made available to all nodes by one Lenovo
DSS-G260 storage appliance (added in Fall 2019) and one GSS24 storage
appliance (from Fall 2017).

Get details on using this system, see the [ User Guide for
Terra](/kb3/User-Guides/Terra/Terra/ "wikilink").

## Compute Nodes

A description of the two types of compute nodes is below:

<table>
<caption>Table 1 Details of Compute Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>General 64GB<br />
Compute</p></th>
<th><p>GPU 128 GB<br />
Compute</p></th>
<th><p>KNL 96 GB (68 core)<br />
Compute</p></th>
<th><p>KNL 96 GB (72 core)<br />
Compute</p></th>
<th><p>V100 GPU 192 GB<br />
Compute</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Total Nodes</p></td>
<td><p>256</p></td>
<td><p>48</p></td>
<td><p>8</p></td>
<td><p>8</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p>Processor Type</p></td>
<td><p>Intel Xeon E5-2680 v4 (Broadwell), 2.40GHz, 14-core</p></td>
<td><p>Intel Xeon Phi CPU 7250 (Knight's Landing), 1.40GHz, 68-core</p></td>
<td><p>Intel Xeon Phi CPU 7290 (Knight's Landing), 1.50GHz, 72-core</p></td>
<td><p>Intel Xeon Gold 5118 (Skylake), 12-core, 2.30 GHz</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Sockets/Node</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Cores/Node</p></td>
<td><p>28</p></td>
<td><p>68</p></td>
<td><p>72</p></td>
<td><p>24</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory/Node</p></td>
<td><p>64 GB DDR4, 2400 MHz</p></td>
<td><p>128 GB DDR4, 2400 MHz</p></td>
<td><p>96 GB DDR4, 2400 MHz</p></td>
<td><p>192 GB, 2400 MHz</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Accelerator(s)</p></td>
<td><p>N/A</p></td>
<td><p>1 NVIDIA K80 Accelerator</p></td>
<td><p>N/A</p></td>
<td><p>2 NVIDIA 32GB V100 GPUs</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Interconnect</p></td>
<td><p>Intel Omni-Path Architecture (OPA)</p></td>
<td><p>Intel Omni-Path Architecture (OPA)</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Local Disk Space</p></td>
<td><p>1TB 7.2K RPM SATA disk</p></td>
<td><p>220GB</p></td>
<td><p>300GB</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**Note, each K80 accelerator has two GPUs.**

## Usable Memory for Batch Jobs

While nodes on Terra have either 64GB or 128GB of RAM, some of this
memory is used to maintain the software and operating system of the
node. In most cases, excessive memory requests will be automatically
rejected by SLURM.

The table below contains information regarding the approximate limits of
Terra memory hardware and our suggestions on its use.

<table>
<caption>Memory Limits of Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>64GB Nodes</p></th>
<th><p>128GB Nodes</p></th>
<th><p>96GB KNL Nodes (68 core)</p></th>
<th><p>96GB KNL Nodes (72 core)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Node Count</p></td>
<td><p>256</p></td>
<td><p>48</p></td>
<td><p>8</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>Number of Cores</p></td>
<td><p>28 Cores (2 sockets x 14 core)</p></td>
<td><p>68 Cores</p></td>
<td><p>72 Cores</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory Limit<br />
Per Core</p></td>
<td><p>2048 MB<br />
2 GB</p></td>
<td><p>4096 MB<br />
4 GB</p></td>
<td><p>1300 MB<br />
1.25 GB</p></td>
<td><p>1236 MB<br />
1.20 GB</p></td>
</tr>
<tr class="even">
<td><p>Memory Limit<br />
Per Node</p></td>
<td><p>57344 MB<br />
56 GB</p></td>
<td><p>114688 MB<br />
112 GB</p></td>
<td><p>89000 MB<br />
84 GB</p></td>
<td><p>89000 MB<br />
84 GB</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

SLURM may queue your job for an excessive time (or indefinitely) if
waiting for some particular nodes with sufficient memory to become free.

\`

## Login Nodes

The **terra.tamu.edu** hostname can be used to access the Terra cluster.
This translates into one of the three login nodes,
**terra\[1-3\].tamu.edu**. To access a specific login node use its
corresponding host name (e.g., terra2.tamu.edu). All login nodes have 10
GbE connections to the TAMU campus network and direct access to all
global parallel (GPFS-based) file systems. The table below provides more
details about the hardware configuration of the login nodes.

<table>
<caption>Table 2: Details of Login Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>No Accelerator</p></th>
<th><p>Two NVIDIA K80 Accelerator</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HostNames</p></td>
<td><p>terra1.tamu.edu<br />
terra2.tamu.edu</p></td>
<td><p>terra3.tamu.edu</p></td>
</tr>
<tr class="even">
<td><p>Processor Type</p></td>
<td><p>Intel Xeon E5-2680 v4 2.40GHz 14-core</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Memory</p></td>
<td><p>128 GB DDR4 2400 MHz</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Total Nodes</p></td>
<td><p>2</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Cores/Node</p></td>
<td><p>28</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Interconnect</p></td>
<td><p>Intel Omni-Path Architecture (OPA)</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Local Disk Space</p></td>
<td><p>per node: two 900GB 10K RPM SAS drives</p></td>
<td></td>
</tr>
</tbody>
</table>

## Mass Storage

7PB (raw) via one Lenovo DSS-G260 appliance for general use and 1PB
(raw) via Lenovo GSS24 appliance purchased by and dedicated for GEOSAT.
All storage appliances use IBM Spectrum Scale (formerly GPFS).

## Interconnect

![Opa\_fabric.png](/kb3/assets/images/Opa_fabric.png "Opa_fabric.png")

## Namesake

"terra" comes from the Latin word for "this planet" a.k.a. "Earth". One
of the purposes of this cluster is to study images gathered from a
"Earth Observation Satellite" (EOS). Given that we just retired a
cluster named "Eos" (named after the Greek goddess of the dawn waiting
to spread the light of knowledge each day), the name terra was chosen
instead
