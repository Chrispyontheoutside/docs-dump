# Service Unit

A ***'Service Unit***' (SU) is charged to a job when the job uses one
***'effective\_core***' for one hour (walltime).  
The calculation of effective\_core depends on whether a job is a
exclusive job or not ('-x' specified or not).

SUs are allocated on a per-cluster basis and can **not** be transferred
between clusters. Additionally, SUs expire each fiscal year and can
**not** be extended to the new fiscal year.

### Exclusive Job

When an exclusive job runs on a node with m cores.  
***'effective\_core = m***'  
Note that the effective\_core for an exclusive job on a node is
independent how many cores are requested by the job.  
Once the effective\_core on a node is calculated, the effective\_core
for the job is simply the sum of the effective\_core on all nodes where
the job runs.

### Non-Exclusive Job

The effective cores on a node is calculated by considering requested
memory. When a job requests xxx memory by "--mem=xxx" and the node has m
cores, then for that requested memory, we have  
***'memory\_equivalent\_core = min(m, ceil(xxx/total\_memory*m))***'  
where total\_memory is the total memory on a node available to users on
that node.  

#### Example 1

`   A compute node has 48 cores and around 351.5G memory available to users. `  
`   When a job requests 13G memory and 2 cores, the job uses `*`memory_equivalent_core`*` of min(48, ceil(13/351.5625*48))=2 core. `

#### Example 2

`   A compute node has 48 cores and around 351.5G memory available to users. `  
`   When the job requests 20G memory and 2 cores, the job uses `*`memory_equivalent_core`*` of min(48, ceil(20/351.5625*48))=3 cores.`

#### Example 3

`   A compute node has 48 cores and around 351.5G memory available to users. `  
`   When the job requests 150G memory and 10 cores, the job uses `*`memory_equivalent_core`*` of min(48, ceil(150/351.5625*48))=21 cores.`

Once the memory\_equivalent\_core is calculated, the effective\_core on
a node where a job request yyy cores can be calculated as below:  
effective\_core = max(yyy, memory\_equivalent\_cores)

Finally, the *effective\_core* for a job is the sum of the
*effective\_core* on all nodes where the job runs.

### SUs for Jobs Requesting GPUs

A job requesting GPUs is considered as an exclusive job. That is, the
SUs consumed by the job is calculated based on all CPUs on GPU nodes.
For example, if a job requests one CPU and a GPU, then the job is a GPU
job. The SUs for the GPU job is calculated as for 28 or 48 CPUs (all
CPUs on a GPU node). *Note that this policy will soon be changing. Come
back for updates.*
