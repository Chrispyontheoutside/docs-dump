# cctools

The Cooperative Computing Tools
([cctools](http://ccl.cse.nd.edu/software/)) is a software package for
enabling large scale distributed computing on clusters, clouds, and
grids. It is used primarily for attacking large scale problems in
science and engineering. "parrot\_run" can be used to access
[CVMFS](https://cernvm.cern.ch/portal/filesystem).

### Parrot

[Parrot](https://ccl.cse.nd.edu/software/parrot/) is a tool for
attaching existing programs to remote I/O systems through the filesystem
interface. Parrot "speaks" a variety of remote I/O services include
HTTP, FTP, GridFTP, iRODS, CVMFS, and Chirp on behalf of ordinary
programs.

Parrot cache dir is set to /scratch/user/YourNetID/parrot\_cache. User
can change it's location by updating environment variable
*PARROT\_CVMFS\_ALIEN\_CACHE* prior running "parrot\_run" command

export PARROT_CVMFS_ALIEN_CACHE=/scratch/user/YourNetID/my_favorite_cache_dir

#### Access Parrot

Parrot is available on Terra cluster and it's working on both login
nodes and compute nodes. HPRC compute nodes do not have access to
internet, thus a proxy server is used when running on the compute nodes.

To access parrot, user can load cctools module

    module load cctools/7.0.22-Python-2.7

Alternatively, user can load cctools with Python 3.6 toolchain via

    module load cctools/7.0.22-Python-3.7

#### Parrot examples

In the following examples, the commands are listed in bold face.

User can list CVMFS file system using "parrot\_run"

    [user@terra1 ~]$ **parrot_run   ls   -lad 
    /cvmfs/cms.cern.ch/slc6_amd64_gcc530**  
    LibCvmfs version 2.4, revision 25  
    drwxr-xr-x 1 root root 44 Dec 19 05:10 /cvmfs/cms.cern.ch/slc6_amd64_gcc530

User can get a shell with "parrot\_run". Please ignore the error of
"bash: /usr/bin/mount: Permission denied"

    [user@terra1 ~]$ **parrot_run   bash**  
    2020/02/19 15:03:46.07 parrot_run[17105] <child:17149> notice: warning: system call 316 (renameat2) not supported for program /usr/bin/mv  
    2020/02/19 15:03:46.38 parrot_run[17105] <child:17178> notice: cannot execute the program /usr/bin/mount because it is setuid.  
    bash: /usr/bin/mount: Permission denied  
    [user@terra1 ~]$ **ls   -l   /cvmfs/atlas.cern.ch**  
    LibCvmfs version 2.4, revision 25  
    total 1  
    drwxr-xr-x 1 root root 3 Dec  5 08:41 repo

User will get a warning message when running "parrot\_run" inside
"parrot\_run bash"

    [user@terra1 ~]$ **parrot_run   bash**  
    sorry, parrot_run cannot be run inside of itself.  
    version already running is 7.0.22 FINAL.

User can check if "parrot\_run" is running via "parrot\_run
--is-running" command. If "parrot\_run" is not running, no output will
be given, otherwise version number will be printed.

    [user@terra1 ~]$ **parrot_run   --is-running**  
    7.0.22 FINAL

User can change prompt for parrot\_run to indicate that you are inside a
parrot\_run shell.

    [user@terra1 ~]$ **PS1="(Parrot)   [\u@terra1   \W]$ 
    "   parrot_run   bash   --login   --noprofile**  
    (Parrot) [user@terra1 ~]$ <b>ls -l /cvmfs/atlas.cern.ch</b>  
    LibCvmfs version 2.4, revision 25  
    total 1  
    drwxr-xr-x 1 root root 3 Dec  5 08:41 repo  
    (Parrot) [user@terra1 ~]$ **exit**  
    logout

Show which filesystems are supported by parrot\_run

    [user@terra1 ~]$ **parrot_run   --help   |   grep 
    Enabled**  
    Enabled filesystems are: chirp ftp cvmfs multi http hdfs grow anonftp

### Sample job script for Terra

The sample job script below shows two methods to run parrot\_run with
list of commands. The first method uses commands listed in an external
script and the second methods uses pipe and heredoc (Here document).

    #!/bin/bash
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=parrot_test       #Set the job name to "parrot_test"
    #SBATCH --time=00:10:00              #Set the wall clock limit to 10min
    #SBATCH --ntasks=1                   #Request 1 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=parrot_test.%j      #Send stdout/err to "parrot_test.[jobID]"
    
    echo "start testing..."
    
    # load module
    module load cctools
    
    # execute commands listed in "mycommands.sh"
    parrot_run $SHELL mycommands.sh
    
    # pipe commands using heredoc (Here document); "EOF" is the delimiting identifier
    parrot_run $SHELL << EOF
    echo "# test: 'ls /cvmfs/geant4.cern.ch' ..."
    ls /cvmfs/geant4.cern.ch
    EOF
    
    echo "end of testing..."

### References

  - CCL software page: <https://ccl.cse.nd.edu/software/>
  - Parrot User Manual:
    <https://cctools.readthedocs.io/en/latest/parrot/>
