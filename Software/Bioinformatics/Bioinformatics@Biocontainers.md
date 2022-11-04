# Biocontainers

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Downloading and Building

The following describes using Singularity for downloading biocontainers
on a compute node using the VNC portal app. Once a biocontainer is
downloaded, it can be used in a job script.

  - Singularity is available on the compute nodes not login nodes.
  - Singularity can be used to download images from a docker repository
    and convert to a singularity image (container).
      - Singularity can convert most docker images to singularity
        images.
  - You can use the HPRC VNC portal app to launch an interactive session
    on a compute node and download docker images (containers) using
    singularity.
  - The following example commands are for the VNC terminal not a login
    node since singularity is not available on the login nodes.
      - You need to enable the proxy in the VNC terminal in order to
        connect a compute node to the internet. Enter the following in
        the VNC terminal:

`module load WebProxy`

  - Singularity downloads include the .sif image as well as a cached
    copy both the same size of around 1GB but the size depends on the
    contents of the container.
      - By default, singularity uses your home directory to store a
        cached copy of downloaded docker images. This can cause you to
        reach your home quota during a download.
      - You can use the $TMPDIR to store the cached copy as well as
        singularity registry in order to avoid reaching your home
        directory quota
      - The $TMPDIR is about 750GB and exists only at job runtime on the
        compute node and does not exist on the login nodes.

`export SREGISTRY_DATABASE=$TMPDIR`  
`export SINGULARITY_CACHEDIR=$TMPDIR`

  - If you see a warning message about the XGD\_RUNTIME\_DIR variable,
    you can unset it.

`unset XDG_RUNTIME_DIR`

  - Search the [biocontainers](https://hub.docker.com/u/biocontainers)
    website for available containers
  - Here is an example of downloading containers
      - the following will create a singularity image file named
        blast\_2.2.31.sif

`singularity pull docker://biocontainers/blast:2.2.31`

  - if the install directions show a docker command like

*`docker   pull 
 registry.gitlab.com/cgps/ghru/pipelines/dsl2/pipelines/assembly:latest`*

add docker:// before the URL when using singularity:

*`singularity   pull 
 `**`docker://`**`registry.gitlab.com/cgps/ghru/pipelines/dsl2/pipelines/assembly:latest`*

to build a specific version, change latest to the version:

*`singularity   pull 
 `**`docker://`**`registry.gitlab.com/cgps/ghru/pipelines/dsl2/pipelines/assembly:2.0.0`*

## Running container commands

  - Since singularity is not available on the login nodes, you can use
    the HPRC VNC portal app to launch an interactive session on a
    compute node and run commands found in the container using
    singularity.

<!-- end list -->

  - Execute a command that is available in the singularity image file:

`singularity exec /sw/hprc/sw/bio/containers/blast_2.2.31.sif blastp -h`

  - Run the image file to explore available software (not used to update
    the image)
      - this will start a prompt so you can test software commands that
        are found in the image

`singularity run /sw/hprc/sw/bio/containers/blast_2.2.31.sif`

## Usage in a job script

  - Once you figure out the commands you want to use, you can create a
    job script and use singularity to run the software command available
    in the container. (using full or relative path for the .sif file or
    just the .sif file name if it is located in the same directory as
    your job script)

`singularity exec /sw/hprc/sw/bio/containers/blast_2.2.31.sif blastp -query seqs.fa -db hg19 -outfmt 10 -out blastout.csv -num_threads 28`

  - There are some available biocontainers on Grace at

`/sw/hprc/sw/bio/containers/`
