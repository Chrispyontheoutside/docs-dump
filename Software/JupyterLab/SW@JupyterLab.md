# JupyterLab

##### Anaconda

###### Default conda environment

You can use the default conda environment in the JupyterLab portal app
by selecting Anaconda/3-5.0.0.1 or Anaconda3/2020.07 and leaving the
'Optional Conda Environment to be activated' field blank.

The default environment for Anaconda/3-5.0.0.1 is
jupyterlab-v1.2.3\_R-3.6.1 which has the R console installed.

The default environment for Anaconda3/2020.07 is
/sw/hprc/sw/Anaconda3/2020.07/envs/jupyterlab\_v2.2.9\_R-3.6.1 which has
the R console installed.

###### Custom Anaconda/3-5.0.0.1 conda environment

You can create your own JupyterLab conda environment using Anaconda for
use on the HPRC portal but you must use one of the Anaconda versions
that are on the JupyterLab [HPRC portal
webpage](https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new).

Notice that you will need to make sure you have enough available file
quota (~30,000) since conda creates thousands of files.

To to create an Anaconda conda environment called jupyterlab, do the
following on the command line:

    module purge
    module load Anaconda/3-5.0.0.1
    conda create -n jupyterlab

After your jupyterlab environment is created, you will see output on how
to activate and use your jupyterlab environment

    #
    # To activate this environment, use:
    # > source activate jupyterlab
    #
    # To deactivate an active environment, use:
    # > source deactivate
    #

Then you can install jupyterlab (specifying a version if needed) and add
packages to your jupyterlab environment

    source activate jupyterlab
    conda install -c conda-forge jupyterlab
    conda install -c conda-forge package-name

You can specify a specific package version with the install command. For
example to install pandas version 1.1.3:

`conda install -c conda-forge pandas=1.1.3`

To remove downloads after packages are installed.

`conda clean -t`

When using Anaconda/3-5.0.0.1, use just the environment name in the
'Optional Environment to be activated' field which in this example will
be **jupyterlab**

###### Custom Anaconda3/2020.07 conda environment

You can create your own JupyterLab conda environment using Anaconda for
use on the HPRC portal but you must use one of the Anaconda versions
that are on the JupyterLab [HPRC portal
webpage](https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new).

Notice that you will need to make sure you have enough available file
quota (~30,000) since conda creates thousands of files.

When using Anaconda3/2020.07, you will need to move your ~/.conda
directory to $SCRATCH and make a symbolic link since Anaconda3 may fill
up your $HOME disk quota:

    cd
    mv .conda $SCRATCH
    ln -s $SCRATCH/.conda

To to create an Anaconda conda environment called jupyterlab, do the
following on the command line:

    module purge
    mkdir -p /scratch/user/your_netid/Anaconda3/2020.07/envs
    module load Anaconda3/2020.07
    conda create --prefix /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab

After your jupyterlab environment is created, you will see output on how
to activate and use your jupyterlab environment. You can use 'source
activate' instead of 'conda activate'

    #
    # To activate this environment, use:
    # > conda activate /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab
    #
    # To deactivate an active environment, use:
    # > conda deactivate
    #

Then you can install jupyterlab (specifying a version if needed) and add
packages to your jupyterlab environment

    source activate /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab
    conda install -c conda-forge jupyterlab
    conda install -c conda-forge package-name

You can specify a specific package version with the install command. For
example to install pandas version 1.1.3:

`conda install -c conda-forge pandas=1.1.3`

To remove downloads after packages are installed.

`conda clean -t`

When using Anaconda3/2020.07, you must use the full path to the
environment in the 'Optional Environment to be activated' field. In this
example it will be
**/scratch/user/your\_netid/Anaconda3/2020.07/envs/jupyterlab**

**NOTE: When using Anaconda3/2020.07 to create a virtualenv, the
installation will add lines to your ~/.bashrc file that you should
delete since these lines which automatically load your virtualenv which
will interfere with other jobs and modules.**

##### Python

###### Default python virtualenv

You can use the default virtualenv in the JupyterLab portal app by
selecting Python/3.7.4-GCCcore-8.3.0 and leaving the 'Optional Conda
Environment to be activated' field blank.

The default virtualenv has
[Jupyterlmod](https://github.com/cmd-ntrf/jupyter-lmod) installed which
allows you to load compatible software modules to use in your notebook.

Type 'toolchains' on the Terra command line to see a table of compatible
toolchains.

To load additional software modules, click the 'Softwares' icon in the
left most part of your JupyterLab notebook. Search for modules with a
compatible toolchain (such as TensorFlow/2.2.0-foss-2019b-Python-3.7.4)
and click 'Load' once and wait for the LOADED MODULES section to
refresh.

If you have already started your notebook before loading modules, you
will need to restart the kernel in order for the loaded module to be
available by clicking Kernel -\> Restart Kernel... in the top JupyterLab
menu or click the 'Restart the kernel' icon at the top of the notebook.

If you get 'Server Connection Error' messages after restarting the
kernel, stop all other notebooks you have running by clicking the
'Running Terminals and Kernels' button in the left panel menu and then
'SHUT DOWN' all other running KERNEL SESSIONS.

###### Custom python virtualenv

You can create your own virtualenv to use with the JupyterLab portal app
but in most cases the default virtualenv should work for you.

You must create your virtualenv using one of the Python modules listed
on the JupyterLab [HPRC portal
webpage](https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new).

Here is an example of creating your own virtualenv on a login node.

    module load Python/3.7.4-GCCcore-8.3.0
    mkdir -p /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0
    cd /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0
    virtualenv jupyterlab
    source /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0/jupyterlab/bin/activate
    pip install juypter
    pip install jupyterlab
    pip install additional_packages

Then in the JupyterLab portal app, select the Python/3.7.4-GCCcore-8.3.0
Module and enter the **full path** of the activate command found in your
virtualenv into the 'Optional Conda Environment to be activated' field.

Example of what to enter in the 'Optional Conda Environment to be
activated' field:

    /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0/jupyterlab/bin/activate

##### Web Access

Although compute nodes do not have access to the internet, the
JupyterLab app uses a proxy server by default which allows your
JupyterLab session to have access to the internet.
