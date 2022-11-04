# Conda/Bioconda

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Description

You can create your own personal conda environment using Anaconda which
installs conda and bioconda packages.

You can install software that supports conda/bioconda installation
inside the conda environment you create.

Once you create a conda environment, you can continue to install other
packages into that environment.

You can create more than one environment in case you need specific
versions of tools.

## Initialization

**Before you begin,** you will need to contact the HPRC helpdesk
(help@hprc.tamu.edu) to request a $SCRATCH file quota increase because
creating a conda environment will add thousands of files to your
$SCRATCH space.

After you get your file quota increase, the next thing you need to do is
to add a few conda channels which contain certain bioinformatics tools.

You only need to do this step once in order to add the conda-forge and
bioconda channels:

    module purge
    module load Anaconda/3-5.0.0.1
    conda config --add channels defaults
    conda config --add channels conda-forge
    conda config --add channels bioconda
    conda config --set auto_activate_base False

## Create a new conda environment

### Anaconda

To to create an Anaconda conda environment called bio, do the following
on the command line:

    module purge
    module load Anaconda/3-5.0.0.1
    conda create -n bio

After your bio environment is created, you will see output on how to
activate and use your bio environment

    #
    # To activate this environment, use:
    # > source activate bio
    #
    # To deactivate an active environment, use:
    # > source deactivate
    #

Then you can add packages to your bio environment

    source activate bio
    conda install -c bioconda bwa

### Miniconda

## Description

You can create your own personal conda environment using miniconda which
you can use to install conda and bioconda packages.

You can install software that supports conda/bioconda installation
inside the conda environment you create.

Once you create a conda environment, you can continue to install other
packages into that environment.

You can create more than one environment in case you need specific
versions of tools.

## Relocate the default install directory

By default, miniconda will save environments in your $HOME/.conda
directory but since space is limited in your $HOME directory, you will
either need to move your $HOME/.conda directory to $SCRATCH or specify
the full path of your miniconda environment.

    cd
    mv .conda $SCRATCH
    ln -s $SCRATCH/.conda

## Create a new conda environment

Once you have moved your .conda directory to $SCRATCH, you can create a
new environment.

    module purge
    module load Miniconda3/4.7.10
    conda create -n my_miniconda_env

You will see a message similar to the following, even though the
location shows /home, the symlink created in the previous step will be
saving the environment in $SCRATCH/.conda

    Collecting package metadata (current_repodata.json): done         
    Solving environment: done
    
    ## Package Plan ##
    
      environment location: /home/your_netid/.conda/envs/my_miniconda_env
    
    
    Proceed ([y]/n)?

Hit enter which accepts the default yes indicated by \[y\] then you will
see the following

    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    #
    # To activate this environment, use
    #
    #     $ conda activate my_miniconda_env
    #
    # To deactivate an active environment, use
    #
    #     $ conda deactivate

Type 'conda activate my\_miniconda\_env' to activate the environment and
then install packages specifying versions if needed If you see a message
like the following:

`CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.`

then use 'source activate my\_miniconda\_env' instead of conda activate.

    source activate my_miniconda_env
    conda install matplotlib numpy

After installing packages, type the following to exit the environment

`conda deactivate`

## See available environments and installed packages

To see available miniconda environments (you don't need to activate an
environment to see available environments):

`module load Miniconda3/4.7.10`  
`conda env list`

To see what packages and versions are installed in an environment (after
activating an environment):

`module load Miniconda3/4.7.10`  
`source activate my_miniconda_env`  
`conda list`

## Installing specific package versions

You can specify the package version when installing packages including
the Python version, either at the time of creation for the python
version:

`conda create -n my_miniconda_env python=3.8.2`

or after sourcing an already created environment for other packages:

`conda install matplotlib=3.2.1`

## Install conda/bioconda packages into an existing environment

If you want to install packages such as fastq-multx and bwa into your
bio environment (notice the (bio) indicating you are within the bio
environment):

`[net_id@ada7 any_directory]$ `**`module   purge`**  
`[net_id@ada7 any_directory]$ `**`module   load 
 Anaconda/3-5.0.0.1`**  
`[net_id@ada7 any_directory]$ `**`source   activate   bio`**  
`(bio) [net_id@ada7 any_directory]$ `**`conda   install 
 fastq-multx   bwa`**

### Debug Failed Installation

Although Anaconda is configured to install in the user's $SCRATCH/.conda
directory, some anaconda packages may utilize the $HOME/.local directory
during installation which could cause you to reach your file quota for
your $HOME directory. To resolve this issue, move your ~/.local
directory to your $SCRATCH directory and create a symbolic link in your
home directory to the .local scratch directory:

    cd
    mv .local $SCRATCH
    ln -s $SCRATCH/.local

## Using your conda Environment

To use your bio environment in a job script, you must first activate the
bio environment and then run tool commands (fastq-multx in this
example). Here is a sample job script (excluding the \#SBATCH headers)

    module load Anaconda/3-5.0.0.1
    source activate bio
    fastq-multx -l barcodes.grp seq2.fastq.gz seq1.fastq.gz -o n/a -o out%.fq
    source deactivate

<hr>
