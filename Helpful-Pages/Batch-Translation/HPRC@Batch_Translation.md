# Batch Job Translation Guide


## Translation Tables

### User Commands

The table below contains commands that would be run from the login nodes
of the cluster for job control and monitoring purposes.

| User Commands        | LSF                     | Slurm                    | PBS/Torque              |
| -------------------- | ----------------------- | ------------------------ | ----------------------- |
| Job submission       | bsub [script_file]   | sbatch [script_file]  | qsub [script_file]   |
| Job deletion         | bkill [job_id]       | scancel [job_id]      | qdel [job_id]        |
| Job status (by job)  | bjobs [job_id]       | squeue --job [job_id] | qstat [job_id]       |
| Job status (by user) | bjobs -u [user_name] | squeue -u [user_name] | qstat -u [user_name] |
| Queue list           | bqueues                 | squeue                   | qstat -Q                |

### Environment Variables

The table below lists environment variables that can be useful inside
job files.

| Environment Variables | LSF          | Slurm              | PBS/Torque       |
| --------------------- | ------------ | ------------------ | ---------------- |
| Job ID                | $LSB_JOBID  | $SLURM_JOBID      | $PBS_JOBID      |
| Submit Directory      | $LSB_SUBCWD | SLURM_SUBMIT_DIR | $PBS_O_WORKDIR |

### Job Specifications

The table below lists various directives that set characteristics and
resources requirements for jobs.

<table>
<thead>
<tr class="header">
<th><p>Job Specification</p></th>
<th><p>LSF</p></th>
<th><p>Slurm</p></th>
<th><p>PBS/Torque</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Script directive</p></td>
<td><p>#BSUB</p></td>
<td><p>#SBATCH</p></td>
<td><p>#PBS</p></td>
</tr>
<tr class="even">
<td><p>Node Count</p></td>
<td><p>N/A<br />
( Calculated from: CPUs/CPUs_per_node )</p></td>
<td><p>-N [min[-max]]</p></td>
<td><p>-l nodes=[count]</p></td>
</tr>
<tr class="odd">
<td><p>CPUs Per Node</p></td>
<td><p>-R "span[ptile=count]"</p></td>
<td><p>--ntasks-per-node=[count]</p></td>
<td><p>-l ppn=[count]</p></td>
</tr>
<tr class="even">
<td><p>CPU Count</p></td>
<td><p>-n [count]</p></td>
<td><p>-n [count]</p></td>
<td><p>N/A<br />
( Calculated from: CPUs_per_node * Nodes )</p></td>
</tr>
<tr class="odd">
<td><p>Wall Clock Limit</p></td>
<td><p>-W [hh:mm]</p></td>
<td><p>-t [min] or -t[days-hh:mm:ss]</p></td>
<td><p>-l walltime=[hh:mm:ss]</p></td>
</tr>
<tr class="even">
<td><p>Memory Per Core</p></td>
<td><p>-M [mm] AND<br />
-R "rusage[mem=mm]"<br />
* Where mm is in MB</p></td>
<td><p>--mem-per-cpu=mem[M/G/T]</p></td>
<td><p>-l mem=[mm]<br />
* Where mm is in MB</p></td>
</tr>
<tr class="odd">
<td><p>Standard Output File</p></td>
<td><p>-o [file_name]</p></td>
<td><p>-o [file_name]</p></td>
<td><p>-o [file_name]</p></td>
</tr>
<tr class="even">
<td><p>Standard Error File</p></td>
<td><p>-e [file_name]</p></td>
<td><p>-e [file_name]</p></td>
<td><p>-e [file_name]</p></td>
</tr>
<tr class="odd">
<td><p>Combine stdout/err</p></td>
<td><p>(use -o without -e)</p></td>
<td><p>(use -o without -e)</p></td>
<td><p>-j oe (both to stdout) OR -j eo (both to stderr)</p></td>
</tr>
<tr class="even">
<td><p>Event Notification</p></td>
<td><p>-B and/or -N<br />
* For Begin and/or End</p></td>
<td><p>--mail-type=[ALL/END]<br />
* See 'man sbatch' for all types</p></td>
<td><p>-m [a/b/e]<br />
* For Abort, Begin, and/or End</p></td>
</tr>
<tr class="odd">
<td><p>Email Address</p></td>
<td><p>-u [address]</p></td>
<td><p>--mail-user=[address]</p></td>
<td><p>-M [address]</p></td>
</tr>
<tr class="even">
<td><p>Job Name</p></td>
<td><p>-J [name]</p></td>
<td><p>--job-name=[name]</p></td>
<td><p>-N [name]</p></td>
</tr>
<tr class="odd">
<td><p>Account to charge</p></td>
<td><p>-P [account]</p></td>
<td><p>-account=[account]</p></td>
<td><p>-l billto=[account]</p></td>
</tr>
<tr class="even">
<td><p>Queue</p></td>
<td><p>-q [queue]</p></td>
<td><p>-q [queue]</p></td>
<td><p>-p [queue]</p></td>
</tr>
</tbody>
</table>

## Advanced Documentation

This guide only covers the most commonly used options and useful
commands.

For more information on **LSF** batch options: [Official LSF V9.1.2
Documentation](https://www.ibm.com/support/knowledgecenter/SSETD4_9.1.2/lsf_welcome.html)

Or see easier-to-read **LSF** docs: [LSF V9.1.2
Documentation](https://hprc.tamu.edu/softwareDocs/lsf/9.1.2/)

For more information on **Slurm** batch options: [Official Slurm
Documentation](http://slurm.schedmd.com/documentation.html)
