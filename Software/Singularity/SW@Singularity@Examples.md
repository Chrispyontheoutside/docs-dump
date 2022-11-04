# Singularity Example

## Popular Repositories

When looking for containerized software, try these repositories:

<span style="color:#FF0000">Notation</span>: \[ \] means optional, \< \>
means mandatory.

### [Docker Hub](https://hub.docker.com/)

Most popular general-purpose public repository. Docker is the most
common container image type.

Repository URLs in the form
https://hub.docker.com/r/\<source-group\>/\<source-name\>

    $ singularity pull [target-filename] docker://<source-group>/<source-name>[:<tag>]

### [Singularity Hub](https://singularity-hub.org/)

General-purpose public repository for singularity users.

Repository URLs in the form
https://singularity-hub.org/collections/\<collection-number\>

Each collection number corresponds to a [github](https://github.com/)
repository of the form <source-group>/<source-name>

    $ singularity pull [target-filename] shub://<source-group>/<source-name>[:<tag>]

### [Singularity Library](https://cloud.sylabs.io/library)

Curated repository of official builds of commonly-used software for
singularity users.

Repositories are organized by
<source-group>/<collection-name>/<source-name>

    $ singularity pull [target-filename] library://<source-group>/<collection-name>/<source-name>[:<tag>]

Note that you can search the Singularity Library from the command line:

    $ singularity search <source-name>

### [NVIDIA GPU Cloud](https://ngc.nvidia.com/catalog/containers)

High performance builds of GPU-enabled software.

Repository URLs in the form
https://ngc.nvidia.com/catalog/containers/\<source-group\>:\<source-name\>

    $ singularity pull [target-filename] docker://nvcr.io/<source-group>/<source-name>[:<tag>]

### [Quay.io](https://quay.io/)

Similar to Dockerhub but with more features for developers.

Repository URLs of the form
https://quay.io/repository/\<source-group\>/\<source-name\>

    $ singularity pull [target-filename] docker://quay.io/<source-group>/<source-name>[:<tag>]

### [BioContainers](https://biocontainers.pro/)

Curated repository of scientific software for biologists.

Repository URLs of the form
https://biocontainers.pro/tools/\<source-name\>

Image files have a <tag> in the form <version>--<nonsense>

    $ singularity pull [target-filename] https://depot.galaxyproject.org/singularity/<source-name>:<tag>

Biocontainers can also be found on Dockerhub and Quay.io (above).

### [IBM PowerAI](https://hub.docker.com/r/ibmcom/powerai) (Traverse only)

Repository name ibmcom/powerai on dockerhub (see above).

## Prebuilt images

HPRC provides (will provide) images using the steps below on ada/terra
in /scratch/data/Singularity/images if you want to use a prebuilt image.
At present(/soon) they include.

  - Fedora28-HPRCLAB-40GB.img - a Fedora 28 image based on HPRC lab
    workstations with room to work
      - Note: this will not work on ada. Various versions of Fedora from
        23 to 28 were tried and all failed on ada due to the older
        kernel in CentOS6.
  - CentOS6-XXGB.img - a CentOS 6 image populated with packages based on
    HPRCLAB workstations (where possible) with room to work
  - CentOS7-XXGB.img - a CentOS 7 image populated with packages based on
    HPRClab workstations (where possible) with room to work
  - lammps-stable\_29Oct2020\_ubuntu20.04\_openmpi\_py3.sif - an
    MPI-ready LAMMPS image from docker://lammps/lammps
  - tensorflow\_2.4.1-gpu.sif - a GPU-ready TensorFlow image from
    docker://tensorflow/tensorflow
  - tensorflow\_2.4.1-gpu-jupyter.sif - a GPU-ready TensorFlow image
    from docker://tensorflow/tensorflow
  - bcbio-nextgen-1.2.8.sif - a Biocontainer with RNA sequencing tools
    from docker://quay.io/biocontainers/bcbio-nextgen

Also check out the README on disk in the same location for more
information.

## Building your own images

In order to build Singularity images yourself you will need a system
with a modern Linux distribution (e.g. Ubuntu/Fedora/CentOS/etc) that
you have sudo/root on. HPRC users cannot do this on HPRC systems given
the lack of sudo.

### Fedora 28

#### Objective

The objective in this case is a Fedora28-HPRCLAB.img file that has space
for users to manuever around and install stuff:

1.  that we can provide to users, a Singularity .img file
    (self-contained), for them to update as needed (as root on their own
    workstations) that also runs on our clusters.
2.  is already populated with HPRCLAB RPMs
3.  has plenty of disk space for the user to add files (as non-root)
    while on the cluster
4.  Example below was created on HPRCLAB workstations.

#### Building an image on your Linux workstation

##### Gather information for package installation

  - Before you start, create a list of RPMs (rpmlist) you want to
    install. Also make a file (repoURLs) listing the URLs for the repo
    install RPMs. Then place both in /root/forFedora28 on the host/build
    system. These will be used later while in the sandbox shell. For
    Fedora 28 we will use the RPMFusion repos and the package list from
    current HPRC lab workstations.

<!-- end list -->

    # cat /root/forFedora28/repoURLs 
    https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-28.noarch.rpm
    https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-28.noarch.rpm
    
    # head -5 /root/forFedora28/rpmlist 
    a2ps
    a52dec
    aajohan-comfortaa-fonts
    aalib-libs
    aalto-xml

##### Create/start a shell in a "sandbox"

  - create a Singularity sandbox from one of Fedora's Docker images

<!-- end list -->

    sudo singularity build --sandbox Fedora28-HPRCLAB.sandbox docker://fedora:28

  - start a shell in the sandbox for the next steps

<!-- end list -->

    sudo singularity shell --writable Fedora28-HPRCLAB.sandbox/

  - go ahead and create bind points for HPRC cluster filesystems

<!-- end list -->

    mkdir /scratch /work

  - do **NOT** add users with useradd... if you do, be sure not to add
    your NetID or things will break on the HPRC clusters later.

##### Populate the sandbox with packages

  - Install the RPMFUSION repos (needed for below)

<!-- end list -->

    dnf -y install `cat /root/forFedora28/repoURLs`

  - populate the sandbox with all the RPMs (we do them in groups at
    first in case there a problems and then do all to see what those
    problems were. (get a snack, take a walk... it can take awhile)

<!-- end list -->

    for x in {a..z} ; do
      dnf -y --skip-broken install `grep ^$x /root/forFedora28/rpmlist`
    done
    dnf -y --skip-broken install `grep ^[A-Z] root/forFedora28/rpmlist`
    dnf -y --skip-broken install `cat /root/forFedora28/rpmlist`

There will still be packages that have "No match" due to not including
the repos for them.

  - do **NOT** add users with useradd... if you do, be sure not to add
    your NetID or things will break.
  - create bind directories for interfacing with HPRC clusters (Note:
    have to do this now while still in sudo shell)

<!-- end list -->

    mkdir /scratch /work

  - once you are happy with the sandbox log out from it
    (logout/exit/Ctrl-D).

##### Create an image (.img)

  - to make an .img file that provides space for the user to work in
    (e.g. download/install software). These steps do not require sudo
    since they don't really create anything in the image.
  - first, determine the installed size of the sandbox

\<pre du -hs Fedora28-HPRCLAB.sandbox/ 24G Fedora28-HPRCLAB.sandbox/

</pre>

  - Given that, add some space for the user to work in. In this case, we
    will use 40GB (approx. sandbox size + 15G).

<!-- end list -->

    singularity image.create Fedora28-HPRCLAB-40GB.img # create .img file
    singularity image.expand -s 40960 Fedora28-HPRCLAB-40GB.img # expand to 40GB, get another snack while you wait

Note: works because there is no real filesystem yet \[some ext3/4
filesystems seem to have a problem with expand\]

  - Now import the sandbox into the 40GB image (more snacks/time)

<!-- end list -->

    sudo tar -cvf - -C Fedora28-HPRCLAB.sandbox/ . | sudo singularity image.import Fedora28-HPRCLAB-40GB.img

(see the last/tar example in 'singularity image.import --help')

##### Test on host build system

  - open a non-sudo shell and see if you can do "things"

<!-- end list -->

    singularity shell Fedora28-HPRCLAB-40GB.img

### CentOS/Ubuntu/others

  - the steps to build images using other Linux distributions are mostly
    the same though there are some notable changes

#### CentOS

  - you'll need to use 'yum' instead of 'dnf'
  - you'll need to change the docker reference to something like:
    docker://centos:6
  - you'll want EPEL instead of RPMFusion. e.g.

<!-- end list -->

    # cat /root/forCentOS6/repoURLs 
    https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm

  - you'll have to develop your own rpmlist

#### Ubuntu

  - you'll need to use 'apt-get' instead of 'dnf'
  - you'll need to change the docker reference to something like
    docker://ubuntu:18 (just a guess)
  - not sure you need extra 'repos'
  - rpmlist is up to you
