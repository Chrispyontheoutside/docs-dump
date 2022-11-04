# Singularity

Containers are a way to package an environment along with an executable
so that no additional installation or setup is required to run it on a
different machine. Singularity (https://sylabs.io/singularity/) is a
container solution that is designed specifically for use on HPC
clusters. If you have a software that depends on a different software
environment than what is installed on our HPRC clusters, Singularity
could be a solution to you.

The basic element of a container solution is an **image**. An image is a
file that includes a self-contained environment with both installed
executables and the system libraries they depend on. The container
**runtime** mediates between the libraries in the image and the
libraries on the host system. In the case of HPRC, the container runtime
software is Singularity. It can read many common container image file
formats, including Docker.

This page describe how to run Singularity container on Terra.

### Why use Containers

  - **Shareability**: you can share your container image file with
    others by uploading it to a public repository, and download files
    shared by others.

<!-- end list -->

  - **Portability**: you can use image files made for any computer with
    the same architecture (x84-64).

<!-- end list -->

  - **Reproducibility**: cluster environments can change whenever the
    locally installed software gets updated. Container users are largely
    unaffected by this.

### Why use Singularity

  - **Security**: Singularity grants the user no additional privileges
    or permissions, so you can't harm the cluster by using singularity,
    nor can other users harm you.

<!-- end list -->

  - **Independence**: Singularity does not require root permission to
    run, so you don't need to ask your administrators for help
    installing anything.

<!-- end list -->

  - **Speed**: Singularity was designed to run "close to the hardware".
    It can take advantage of high-performance cluster technologies like
    Infiniband and GPUs.

## Getting a container image

Container images are found in both public and private repositories
available on the internet, such as dockerhub and singularityhub.
Singularity *pull* can automatically download and convert those images
to the singularity file format. Read more about singularity pull on
[singularity user
guide](https://sylabs.io/guides/3.7/user-guide/singularity_and_docker.html#making-use-of-public-images-from-docker-hub).
See our [ detailed
examples](/kb3/Software/Singularity/SW@Singularity@Examples/#popular-repositories "wikilink") page
for other popular repositories.

<span style="color:#FF0000">Caution</span>: dockerhub and singularityhub
are public repositories; do not trust unverified sources\!

<span style="color:#FF0000">Warning</span>: downloading a large image
file is resource-intensive and takes a long time.

### Read this before using Singularity pull commands on HPRC clusters

On HPRC, singularity commands must be executed on compute nodes because
they are too resource-intensive for login nodes. To use a compute node
interactively for command line use, on Terra or Grace: use the Slurm
command *srun* with option *--pty*. Details about the options are in the
[Slurm Manual](https://slurm.schedmd.com/) and [LSF
Manual](https://hprc.tamu.edu/softwareDocs/lsf/9.1.2/) respectively.

  - Terra or Grace interactive example
        srun --nodes=1 --ntasks-per-node=1 --mem=512m --time=01:00:00 --pty bash -i

Singularity stores data in a cache directory named *.singularity* to
make future commands faster. By default, this cache will be in your
/home directory, which will quickly use up your file quota. Recommended
to tell singularity to use a directory in your /scratch space instead.

    export SINGULARITY_CACHEDIR=$SCRATCH/.singularity

Some Singularity commands require internet access. In order to access
the internet from compute nodes, follow the [Web
Proxy](/kb3/Software/Web-Proxy/SW@WebProxy/ "wikilink") instructions.

    module load WebProxy 

### Singularity pull examples

#### Example on Terra, interactive job

Example container image located on dockerhub at
<https://hub.docker.com/_/hello-world> . The file will be named
hello-world.sif and it will be in $SCRATCH.

    [username@login]$ srun --nodes=1 --ntasks-per-node=4 --mem=2560M --time=01:00:00 --pty bash -i
    (wait for job to start)
    [username@compute]$ cd $SCRATCH
    [username@compute]$ export SINGULARITY_CACHEDIR=$SCRATCH/.singularity
    [username@compute]$ module load WebProxy
    [username@compute]$ singularity pull hello-world.sif docker://hello-world
    (wait for download and convert)
    [username@compute]$ exit

#### Example on Terra, batch job

Example container image located on dockerhub at
<https://hub.docker.com/_/hello-world> . The file will be named
hello-world.sif and it will be in $SCRATCH.

    #!/bin/bash
    ##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE                #Do not propagate environment
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=sing_pull            #Set the job name to "sing_pull"
    #SBATCH --time=01:00:00              #Set the wall clock limit to 1hr 
    #SBATCH --ntasks=4                   #Request 4 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=sing_pull.%j           #Send stdout/err to "sing_pull.[jobID]"
    
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address
    
    # set up environment for download 
    cd $SCRATCH
    export SINGULARITY_CACHEDIR=$SCRATCH/.singularity
    module load WebProxy
    
    # execute download
    singularity pull hello-world.sif docker://hello-world

## Interact with container

When a container image file is in place at HPRC, it can be used to
control your environment for doing computation tasks.

### Shell

The shell command allows you to spawn a new shell within your container
and interact with it as though it were a small virtual machine.

    singularity shell hello-world.sif

Don't forget to *exit* when you're done.

### Executing commands

The *exec* command allows you to execute a custom command within a
container by specifying the image file.

    singularity exec hello-world.sif ls -l /
    singularity exec hello-world.sif /scratch/user/userid/myprogram

### Running a container

Execute the default
[runscript](https://sylabs.io/guides/3.7/user-guide/quick_start.html#running-a-container)
defined in the container

    singularity run hello-world.sif

## Running Singularity container on HPRC clusters

### Files in and outside a container

The filesystem inside the container is isolated from the filesystem
outside the container. In order to access your files on a real, physical
filesystem, you have to ensure that filesystem's directory is mounted.
By default, Singularity will mount the $HOME directory as well as the
current working directory $PWD if it can. To specify additional
directories, use the SINGULARITY\_BINDPATH environment variable or the
*--bind* command line option.

Recommended: bind your $SCRATCH directory for data files and $TMPDIR for
temporary files. $TMPDIR may vary from machine to machine, so it's best
to leave it as a variable.

    export SINGULARITY_BINDPATH="/scratch,$TMPDIR"

or

    singularity --bind "/scratch,$TMPDIR" [commands]

Read more at:

  - <https://sylabs.io/guides/3.7/user-guide/bind_paths_and_mounts.html>

### GPU in a container

If your container has been compiled with CUDA version \>= 9, it should
work with the local GPUs. Just add the *--nv* flag to your singularity
command.

Example

    singularity exec --nv tensorflow-gpu.sif python3

### Sample job script for Terra

This job script requests 4 cores and 2.5 GB memory per node. It launches
a container with Centos 6 system libraries.

    #!/bin/bash
    ##ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE                #Do not propagate environment
    
    ##NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=test              #Set the job name to "JobExample1"
    #SBATCH --time=00:10:00              #Set the wall clock limit to 1hr and 30min
    #SBATCH --ntasks=4                   #Request 4 task
    #SBATCH --mem=2560M                  #Request 2560MB (2.5GB) per node
    #SBATCH --output=test.%j             #Send stdout/err to "Example1Out.[jobID]"
    
    ##OPTIONAL JOB SPECIFICATIONS
    ##SBATCH --account=123456             #Set billing account to 123456
    ##SBATCH --mail-type=ALL              #Send email on all job events
    ##SBATCH --mail-user=email_address    #Send all emails to email_address
    
    export SINGULARITY_BINDPATH="/scratch,$TMPDIR"
    
    # execute the default runscript defined in the container 
    singularity run centos6_bootstrapped.img
    
    # execute a command within container
    #  the command should include absolute path if the command is not in the default search path
    singularity exec centos6_bootstrapped.img /scratch/user/netid/runme.sh

### Interactive apps via Portal

Some of the Graphical Interactive Apps in [ HPRC
Portal](/kb3/Software/Portal/SW@Portal/ "wikilink") support the use of Singularity
environments. Currently:

  - [ Jupyter Notebook](/kb3/Software/Portal/SW@Portal/#jupyter-notebook "wikilink"). You must
    provide a singularity image that has a working Jupyter app installed
    in it.

You can request other apps to be supported in this way. We intend to
increase this list going forward.

## Saving Data in the Container Filesystem

### Why Overlay

Have any of these problems?

  - Need to install additional software in a container (i.e. `pip
    install` )

<!-- end list -->

  - Wish to save your work persistently

<!-- end list -->

  - Millions of files and running out of quota

In Docker-like container environments, the user has root privileges
during runtime. Thus, the user is free to modify the container
filesystem at-will. However, in Singularity this is not the case.
Generally, a singularity user will not have root privileges during
runtime, and singularity images are treated as read-only. The container
filesystem is ephemeral and disappears when the runtime shuts down. A
solution to this problem is called an **overlay file**, which extends
the filesystem inside the container. When you use an overlay, any files
you create in the container filesystem will be saved persistently in the
overlay file. As far as the real, physical file system is concerned, the
whole overlay is a single file: it counts as 1 towards your quota.

### Create an Overlay file

Creation of an overlay file requires the use of a tool named
`mkfs.ext3`, which is not installed on Terra or Grace. However, it is
installed in a standard Ubuntu container. Example:

  - Image file: ubuntu-18.04.sif
  - From docker://ubuntu:18.04
  - Located at /scratch/data/Singularity/images

Creation of an overlay file must be done on the /tmp file system on
Grace because the Lustre filsystem (/scratch, etc) lacks some necessary
features. `$TMPDIR` points to a job-specific location in /tmp.

Creation of an overlay filesystem begins with setting up a pair of empty
directories named `upper` and `work`. Creating these directories
manually is the only way to ensure they have the correct ownership and
permissions.

Creation of an overlay file also means pre-filling the virtual disk with
initial data, which is easiest if it's all zeros. The tool `dd` does
this task.

Choose a size for your overlay file and a block size (recommended: 1M).
Divide the two to get the number of blocks. Example:

  - Overlay size: 200 MB
  - Block size: 1 MB
  - Block count: 200

Assuming you start from a login node, execute the following commands.
Substitute your *size* choices and the `/path/to/final/location`
(recommended: `$SCRATCH`).

    $ srun --mem=512m --time=01:00:00 --pty bash -i
    $ singularity shell ubuntu-18.04.sif
    > cd $TMPDIR
    > mkdir -p overlay_tmp/upper overlay_tmp/work
    > dd if=/dev/zero of=my_overlay count=200 bs=1M
    > mkfs.ext3 -d overlay_tmp my_overlay 
    > cp my_overlay /path/to/final/location/

### Use an Overlay file

Whenever you execute a singularity command, you can add `--overlay`
option along the with the path to an overlay file. For example:

    $ singularity shell --overlay my_overlay ubuntu-18.04.sif 
    > mkdir /new_dir
    > touch /new_dir/new_file
    > exit 
    $ singularity shell --overlay my_overlay ubuntu-18.04.sif 
    > ls /new_dir
    new_file

Only one running process can access an overlay file at a given time, so
if you have multiple batch jobs, you will need to do some extra steps.

## Build and Modify your own containers

User should install Singularity on their desktop/laptop to create/modify
the container. Building and modifying containers usually requires *sudo*
with root privileges, which is not available to users on HPRC for
security reasons. Users should prepare Singularity container on their
desktop or laptop, where they have *sudo* right to modify the
Singularity container. Then upload the prepared image to their scratch
directory on the cluster.

### Instructions

  - External guide [Build images from
    scratch](https://www.sylabs.io/guides/3.7/user-guide/quick_start.html#build-images-from-scratch).

<!-- end list -->

  - Also see our [ detailed
    examples](/kb3/Software/Singularity/SW@Singularity@Examples/#building-your-own-images "wikilink")
    page.

### Passing in filesystems

**Optional:** To access cluster filesystem in the container, it is
convenient to pre-create these folders in your container

    /general
    /scratch
    /work

**Optional**: Also, replace /home with a symbolic link

    mv /home /home.orig
    ln -s /general/home /home

## Examples

We have some [ detailed examples](/kb3/Software/Singularity/SW@Singularity@Examples/ "wikilink")
available.

## Additional Documents

  - [Singularity
    Documentation](https://sylabs.io/guides/3.7/user-guide/index.html)
  - [Singularity Quick Start
    Guide](https://www.sylabs.io/guides/3.7/user-guide/quick_start.html)
  - [Singularity User
    Guide](https://www.sylabs.io/guides/3.7/user-guide/index.html)
  - [Singularity@TACC](https://tacc.github.io/CSC2017Institute/docs/day4/singularity.html)
  - [From Docker to
    Singularity](https://github.com/TACC/TACC-Singularity/blob/master/docs/from-docker-to-singularity.md)
