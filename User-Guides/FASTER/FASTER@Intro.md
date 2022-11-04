# FASTER Hardware Overview
 
## FASTER: A Dell x86 HPC Cluster

![caption](/kb3/assets/images/FASTER.jpeg "caption")

<table>
<tbody>
<tr class="odd">
<td><p>System Name:</p></td>
<td><p>FASTER</p></td>
</tr>
<tr class="even">
<td><p>Host Name:</p></td>
<td><p>faster.hprc.tamu.edu</p></td>
</tr>
<tr class="odd">
<td><p>Operating System:</p></td>
<td><p>Linux (CentOS 8)</p></td>
</tr>
<tr class="even">
<td><p>Total Compute Cores/Nodes:</p></td>
<td><p>11,520 cores<br />
180 nodes</p></td>
</tr>
<tr class="odd">
<td><p>Compute Nodes:</p></td>
<td><p>180 64-core compute nodes, each with 256GB RAM</p></td>
</tr>
<tr class="even">
<td><p>Composable GPUs:</p></td>
<td><p>200 T4 16GB GPUs<br />
40 A100 40GB GPUs<br />
10 A10 24GB GPUs<br />
4 A30 24GB GPUs<br />
8 A40 48GB GPUs</p></td>
</tr>
<tr class="odd">
<td><p>Interconnect:</p></td>
<td><p>Mellanox HDR100 InfiniBand (MPI and storage)<br />
Liqid PCIe Gen4 (GPU composability)</p></td>
</tr>
<tr class="even">
<td><p>Peak Performance:</p></td>
<td><p>1.2 PFLOPS</p></td>
</tr>
<tr class="odd">
<td><p>Global Disk:</p></td>
<td><p>5PB (usable) via DDN Lustre appliances</p></td>
</tr>
<tr class="even">
<td><p>File System:</p></td>
<td><p>Lustre</p></td>
</tr>
<tr class="odd">
<td><p>Batch Facility:</p></td>
<td><p><a href="http://slurm.schedmd.com/">Slurm by SchedMD</a></p></td>
</tr>
<tr class="even">
<td><p>Location:</p></td>
<td><p>West Campus Data Center</p></td>
</tr>
<tr class="odd">
<td><p>Production Date:</p></td>
<td><p>2021</p></td>
</tr>
</tbody>
</table>

FASTER is a 184-node Intel cluster from Dell with an InfiniBand HDR-100
interconnect. A100 GPUs, A10 GPUs, A30 GPUs, A40 GPUs and T4 GPUs are
distributed and composable via Liqid PCIe fabrics. All login and compute
nodes are based on the [Intel Xeon 8352Y Ice Lake
processor](https://ark.intel.com/content/www/us/en/ark/products/212284/intel-xeon-platinum-8352y-processor-48m-cache-2-20-ghz.html).

## Compute Nodes

Table 2: Details of Compute Nodes

|                           | Compute Nodes                          |
| ------------------------- | -------------------------------------- |
| Processor Type            | Intel Xeon 8352Y (Ice Lake)            |
| Sockets per node          | 2                                      |
| Cores per socket          | 32                                     |
| Cores per Node            | 64                                     |
| Hardware threads per core | 2                                      |
| Hardware threads per node | 128                                    |
| Clock rate                | 2.20GHz (3.40 GHz Max Turbo Frequency) |
| Memory                    | 256 GB DDR4-3200                       |
| Cache                     | 48 MB L3                               |
| Local Disk Space          | 3.84 TB NVMe (/tmp)                    |



GPUs can be added to compute nodes on the fly by using the “gres” option
in a Slurm script. A researcher can request up to 10 GPUs to create
these CPU-GPU nodes. The following GPUs will be composable to the
compute nodes.

  - 200 T4 16GB GPUs
  - 40 A100 40GB GPUs
  - 10 A10 24GB GPUs
  - 4 A30 24GB GPUs
  - 8 A40 48GB GPUs

## Login Nodes

<table>
<caption>Table 2: Details of Login Nodes</caption>
<thead>
<tr class="header">
<th></th>
<th><p>Login Nodes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hostnames</p></td>
<td><p>faster1.hprc.tamu.edu<br />
faster2.hprc.tamu.edu<br />
faster3.hprc.tamu.edu<br />
faster4.hprc.tamu.edu</p></td>
</tr>
<tr class="even">
<td><p>Processor Type</p></td>
<td><p>Intel Xeon 8352Y (Ice Lake)</p></td>
</tr>
<tr class="odd">
<td><p>Memory</p></td>
<td><p>256 GB DDR4-3200</p></td>
</tr>
<tr class="even">
<td><p>Total Nodes</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Cores/Node</p></td>
<td><p>64</p></td>
</tr>
<tr class="even">
<td><p>Interconnect</p></td>
<td><p>InfiniBand HDR100</p></td>
</tr>
<tr class="odd">
<td><p>Local Disk Space</p></td>
<td><p>3.84 TB (/tmp)</p></td>
</tr>
</tbody>
</table>

## Data Transfer Nodes

FASTER has two data transfer nodes that can be used to transfer data to
FASTER via Globus Connect web interface or Globus command line. Globus
Connect Server v5.4 is installed on the data transfer nodes. One data
transfer node is dedicated to XSEDE users and its collection is listed
as “XSEDE TAMU FASTER”.
