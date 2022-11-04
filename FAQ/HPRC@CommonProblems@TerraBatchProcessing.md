# Terra Batch Processing

### Q: Why is my job pending?

**A:** There can be many reasons why a job would be pending:

  - **The job would run over the maximum runtime for the queue**
      - If a job asks for more than 7 days, the job will remain pending.
      - If a queue was reqested in the job file and the requested
        runtime is longer than the maximum of that queue, the job will
        remain pending.
      - Queue information, including maximum runtime, can be found on
        our Terra [Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/#queues "wikilink")
        page.
      - **SOLUTION:** Kill the job and resubmit with a shorter runtime
        or in a different queue.

<!-- end list -->

  - **There are no job slots available**
      - If the job requires the usage of the 128GB (GPU) nodes, it might
        be pending for longer than usual.
      - If the cluster usage is particularly high right now, jobs might
        be pending for longer than usual. The System Load Levels are
        available on our [Home Page](https://hprc.tamu.edu/).

<!-- end list -->

  - **Your job will run into / through a scheduled maintenance time.
    Check the [HPRC web site for any scheduled
    maintenance.](https://hprc.tamu.edu)**
      - If your job's wall time schedules your job into / through a
        scheduled maintenance it will be stuck pending.
      - **SOLUTION:** Kill the job and resubmit with a wall time which
        ends before the scheduled maintenance or resubmit after the
        maintenance has finished.

### Q: Why does my job fail?

**A:** There can be many reasons why a job fails. ALWAYS check the job
output file that is created by the batch system and any program output
files for information regarding why a job might have failed.

  - **Wrong file format**
      - If a file has been edited on a Windows computer prior to using
        it on our clusters, the file may be in the wrong format.
      - **TIP:** Use the **file** command to check if the file has CRLF
        line terminators. If it does, the file is in the wrong format.
      - **SOLUTION:** Try the [ dos2unix](/kb3/Software/useful-tools/SW@dos2unix/ "wikilink")
        utility on the file and submit again.

`[NetID@cluster ~]$ `**`file   `*`myFile`***  
`myFile: ASCII English text, with CRLF line terminators`  
`[NetID@cluster ~]$ `**`dos2unix   `*`myFile`***  
`dos2unix: converting file myFile to UNIX format ...`  
`[NetID@cluster ~]$ `**`file   `*`myFile`***  
`myFile: ASCII English text`

  - **The job ran out of time**
      - If "CANCELLED ... DUE TO TIME LIMIT" appears in the job output
        file, the job ran out of time.
      - **SOLUTION:** Increase the wall time specification **\#SBATCH -t
        HH:MM:SS** and submit again.

<!-- end list -->

  - **The job ran out of memory**
      - If "CANCELLED ... DUE TO MEMORY LIMIT" appears in the job output
        file, the job ran out of memory.
      - **SOLUTION:** Increase the memory specification **\#SBATCH
        --mem=XX** and submit again.

<!-- end list -->

  - **Not enough space**
      - If "DISK QUOTA EXCEEDED" appears in the output file, there is
        not enough disk space to complete the job.
      - All users are encouraged to check their quotas regularly with
        **showquota**.
      - **SOLUTION:** See the question [
        here](/kb3/FAQ/HPRC@CommonProblems@Other/ "wikilink")
        for how to deal with **DISK QUOTA EXCEEDED** errors.

### Q: Why is my job unable to reach the Internet?

**A:** For policy reasons, we do not allow cluster compute nodes to
communicate with the Internet. If you need to download something from
the Internet (such as downloading software or cloning a git repo), you
must do so from a cluster login node.

### Q: What if I want to run a program interactively? (GUI)

**A:** Although most computation on our clusters is done
non-interactively, we support several options for interactive
programming and visualization.

  - **Use Open OnDemand (Recommended Method)**
      - Open OnDemand is a web-based interface for creating, launching,
        and visualizing jobs on Terra. There are several applications
        you can launch via Open OnDemand such as ABAQUS and MatLab. You
        can find Open OnDemand at the following URL:
        <https://portal.hprc.tamu.edu>
      - You can read more about Open OnDemand on the Portal Wiki page: [
        Open OnDemand Wiki Page](/kb3/Software/Portal/SW@Portal/ "wikilink")

<!-- end list -->

  - Submit a VNC Job 
      - You can submit a VNC job to open a GUI on Terra. There is an
        in-depth guide on launching Remote Visualization job on Terra: [
        Terra VNC Guide](/kb3/Software/useful-tools/SW@Remote-Viz/ "wikilink")

<!-- end list -->

  - Run from Login Node with X11 forwarding 
      - You can launch the GUI of certain applications from the login
        nodes. Keep in mind the Acceptable Use Policy while running on
        the login nodes. These limitations include:
          - **ONE HOUR** of PROCESSING TIME per login session.
          - **EIGHT CORES** per login session on the same node or
            (cumulatively) across all login nodes
      - A detailed guide for launching GUI's from the Login nodes can be
        found at: [ Access Guide](/kb3/Helpful-Pages/Access/HPRC@Access/ "wikilink")

### Q: Why is my program slow?

**A: While using one core:**

  - Supercomputers ("clusters") are not large single-core entities. A
    cluster is a collection of CPUs. Each CPU is likely similar to what
    one would use in most "regular" computers. A huge performance gain
    should not be expected when using a single core on one of our
    clusters versus a "regular" computer. In order to see a performance
    gain, programs and simulations will need to be parallelized to run
    on multiple cores.

**A: While using multiple cores:**

  - If a program or simulation is running particularly slowly, it may be
    experiencing parallel slowdown. This happens when the overhead from
    communication is greater than the time spent running a program.
    Trying to further parallelize the program will continue to slow it
    down.
  - **SOLUTION:** Reduce the amount of parallelization in the program
    until the program's "sweet spot" in which it has the most
    significant speed-up. If no speed-up can be achieved from
    parallelization, it might be best to run the program serially.
  - **IMPORTANT NOTE:** If the program or simulation is not written to
    be parallelized, it will either not work at all and/or waste SUs.