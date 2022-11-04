# Anaconda
Anaconda is a leading open data science platform powered by [Python][1]. It provides a collection of over 720 open source packages, and is a package and virtual environment manager. More details on Anaconda: [https://docs.continuum.io/anaconda/][2]. Next several important concepts are discussed, and then we discuss Anaconda modules on Terra.
## Important Concepts

### Package
A package is a collection of programs. For example, numpy is a package, tensorflow is a package, etc. Over 150 packages are automatically installed with Anaconda installation. Over 250 additional open source packages can be installed from the Anaconda repository with the 'conda install' command. Moreover, thousands of other packages are available from Anaconda cloud.

### Virtual Environment
A virtual environment is a named collection of packages. For example, a virtual environment named 'test_environment' is a collection of python 3.5, basemap 1.0.7, and shapely 1.5.16. A user may create one virtual environment per project if each project needs different collection of software. Therefore, virtual environments avoid problems of version conflicting between different user projects. The command 'conda' is used to create and manage virtual environments in Anaconda. Note that other than 'conda', the command 'pip' can also be used to install python packages into a virtual environment. The 'pip' command facilitates to access more python packages. However, 'pip' does not resolve package dependency well, while 'conda' does a much better job._

## Versions available on Terra/Grace
The most up to date listing of available versions on the cluster you are using can be found with:

```php
module avail Anaconda
```

This will show all available versions of below (plus some of the **myAnaconda** modules described on the [Python page][3]).

### Anaconda Modules on Terra
Run command 'module spider Anaconda' to list Anaconda modules which include Anaconda/2-4.3.1 and Anaconda/3-5.0.0.1

Module Anaconda/2-4.3.1 is for Python 2.7, while Anaconda/3-5.0.0.1 is for Python 3.6.

Anaconda/3-5.0.0.1 is recommended for users without legacy issues.

### Anaconda Modules on Grace
Run command 'module spider Anaconda' to list Anaconda modules which include Anaconda2/5.3.0 and Anaconda3/5.3.0

Module Anaconda2/5.3.0 is for Python 2.7, while Anaconda3/5.3.0 is for Python 3.6.

Anaconda3/5.3.0 is recommended for users who needs Python 3, while Anaconda2/5.3.0 is recommended for users who needs Python 2.

## Managing Anaconda Virtual Environments
Information about environment management can be found on this page.

```php
https://conda.io/docs/user-guide/tasks/manage-environments.html
```

### Using Anaconda
Anaconda/3-5.0.0.1 is recommended on Terra.

#### List Anaconda Virtual Environments
A user may list all shared virtual environments and your own private virtual environments using the command:

```php
conda info --env
```

We have many shared environment related to specific tasks. For example, the tensorflow-gpu, keras-gpu environments can be useful for machine learning applications.

#### Virtual Environment Types
* **Shared Virtual Environments** The command 'conda create -n virtual_environment_name python=x.x' creates a virtual environment named as 'virtual_environment_name' (a user should change the virtual environment name) in anaconda. On our clusters, users do not have write permission to where anaconda root environment is. So users cannot use this command to create a virtual environment using the Anaconda modules on our clusters. Instead, we may create a virtual environment for user(s). Note that all virtual environment created by this command are accessible to all users.
	* Note: A list of available virtual environments (currently 76) can be discerned from the files in /sw/local/etc/Anaconda/venvs/. e.g. on terra, using Anaconda/3-5.0.0.1, one should be able to activate the VE "tensorflow-gpu-1.4.1" as needed.
* Private Virtual Environment A user can create a private virtual environment using the command 'conda create -n virtual_environment_name package_to_install' where package_to_install is optional. Such a virtual environment is only accessible to the user who creates it. The private virtual environment is located at $SCRATCH/.conda/envs. <span style="color:red"> NOTE: private virtual environment works only for Anaconda/3-4.4.0 and later version (e.g., 3.5.0.0.1)  </span>

#### Create a Private Anaconda Virtual Environment
Make scratch directory as your current directory and follow the commands in order to create your own virtual environment.

<span style="color:red"> NOTE: Do not create an environment in your home directory. You will exceed your home directory file limit. 
Do not create an environment named 'base' since this is the default base environment used by all environments. </span>

```php
[NetID@cluster NetID]$ cd $SCRATCH                                     # Make scratch your current directory
[NetID@cluster NetID]$ module load Anaconda/3-5.0.0.1                  # Load Anaconda module
[NetID@cluster NetID]$ conda config --set auto_activate_base False     # run once to disable auto Anaconda loading
[NetID@cluster NetID]$ conda create --name myenv                       # Create environment 
```

Now "conda info --env" command will also show your private environment.

#### Access an Anaconda Virtual Environment
To activate a virtual environment user has to first load anaconda and follow these steps

```php
[NetID@cluster NetID]$ module load Anaconda/3-5.0.0.1          # Load Anaconda module
[NetID@cluster NetID]$ source activate myenv                   # Activate environment 
(myenv) [NetID@cluster NetID]$ python myprogram.py             # Run your programs/commands (activated environment name will show on left of command line)
(myenv) [NetID@cluster NetID]$ source deactivate               # Deactivate environment                 
[NetID@cluster NetID]$                                         # Command line changes to normal
```


Normally a user needs to load Anaconda module and any other modules needed for your virtual environment, source activate virtual environment, and then user can run a program or commands which access the packages in the activated virtual environment. After the program or commands finished, the user should source deactivate the virtual environment. Actually, the last step 'source deactivate virtual_environment_name' is not necessary if you do not need to clean your path environment. Below are the summaries on how to access a virtual environment.

1. module load Anaconda/xxx
2. module load any_other_module_needed
3. source activate your_virtual_environment_name
4. run your programs/commands
5. source deactivate

Note: if you have a virtual environment not in the output of 'conda info --env', then you need the full path of the virtual environment in the source activate command. For example: source activate /scratch/user/uncommon/test.

#### Check Packages in an Anaconda Virtual Environment
To check the list of packages in a Anaconda environment user first can follow these steps on command line.

```php
[NetID@cluster NetID]$ module load Anaconda/3-5.0.0.1          # Load Anaconda module
[NetID@cluster NetID]$ source activate myenv                   # Activate environment
(myenv) [NetID@cluster NetID]$ conda list                      # Conda list command to check installed packages; for example to see if numpy is installed
```

If you don't activate an environment and use "conda list" command then it will show packages in root environment.

#### Install/Uninstall Packages in a Anaconda Virtual Environment
<span style="color:red"> NOTE: Users can only install/uninstall packages in their private environment. Users don't have access to install/uninstall packages in root and shared environments. </span>

To install/uninstall packages in private environments users first need to activate them. For example, next few steps show how to install and uninstall numpy package in the "myenv" private environment.

```php
[NetID@cluster NetID]$ module load Anaconda/3-5.0.0.1          # Load Anaconda module
[NetID@cluster NetID]$ source activate myenv                   # Activate environment
(myenv) [NetID@cluster NetID]$ conda install numpy             # Command to install numpy package
(myenv) [NetID@cluster NetID]$ conda list                      # Conda list command to check packages
(myenv) [NetID@cluster NetID]$ conda uninstall numpy           # Command to uninstall numpy package
```

If you see the following error after installing a software package in Anaconda:

```php
This system lists a couple of UTF-8 supporting locales that
you can pick from.  The following suitable locales were
discovered: aa_DJ.utf8, aa_ER.utf8, aa_ET.utf8, af_ZA.utf8, am_ET.utf8, an_ES.utf8, ar_AE.utf8, ar_BH.utf8, ar_DZ.utf8, ar_EG.utf8, ar_IN.utf8, ar_IQ.utf8, ar_JO.utf8, ar_KW.utf8, ar_LB.utf8, ar_LY.utf8, ar_MA.utf8, ar_OM.utf8, ar_QA.utf8, ar_SA.utf8, ar_SD.utf8, ar_SY.utf8, ar_TN.utf8, ar_YE.ut
```

Then copy the activate_utf.sh file to you conda environment substituting USERNAME and ENVIRONMENTNAME with your netid and environment name:_

```php
Terra:
cp /sw/hprc/sw/Anaconda/activate_utf.sh /scratch/user/USERNAME/.conda/envs/ENVIRONMENTNAME/etc/conda/activate.d/
```

Or if that doesn't work, run the following commands after activating your environment

```php
export LANGUAGE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

#### Clean and Remove a Virtual Environment
Anaconda downloads packages to your computer before software packages are installed. Those downloaded packages consume your disk quota. You may run 'conda clean --all' after your software packages are installed. To complete remove your private virtual environment myenv when you no longer need it, run the command "conda remove --name myenv --all"

### JupyterLab
#### Anaconda
##### Default conda environment

You can use the default conda environment in the JupyterLab portal app by selecting Anaconda/3-5.0.0.1 or Anaconda3/2020.07 and leaving the 'Optional Conda Environment to be activated' field blank.

The default environment for Anaconda/3-5.0.0.1 is jupyterlab-v1.2.3_R-3.6.1 which has the R console installed.

The default environment for Anaconda3/2020.07 is /sw/hprc/sw/Anaconda3/2020.07/envs/jupyterlab_v2.2.9_R-3.6.1 which has the R console installed.

##### Custom Anaconda/3-5.0.0.1 conda environment
You can create your own JupyterLab conda environment using Anaconda for use on the HPRC portal but you must use one of the Anaconda versions that are on the JupyterLab [HPRC portal webpage][4].

Notice that you will need to make sure you have enough available file quota (30,000) since conda creates thousands of files.

To to create an Anaconda conda environment called jupyterlab, do the following on the command line:

```php
module purge
module load Anaconda/3-5.0.0.1
conda create -n jupyterlab
```

After your jupyterlab environment is created, you will see output on how to activate and use your jupyterlab environment

```php
#
# To activate this environment, use:
# > source activate jupyterlab
#
# To deactivate an active environment, use:
# > source deactivate
#
```

Then you can install jupyterlab (specifying a version if needed) and add packages to your jupyterlab environment

```php
source activate jupyterlab
conda install -c conda-forge jupyterlab
conda install -c conda-forge package-name
```

You can specify a specific package version with the install command. For example to install pandas version 1.1.3:

```php
conda install -c conda-forge pandas=1.1.3
```

To remove downloads after packages are installed.

```php
conda clean -t
```


When using Anaconda/3-5.0.0.1, use just the environment name in the 'Optional Environment to be activated' field which in this example will be **jupyterlab**

##### Custom Anaconda3/2020.07 conda environment
You can create your own JupyterLab conda environment using Anaconda for use on the HPRC portal but you must use one of the Anaconda versions that are on the JupyterLab [HPRC portal webpage][5].

Notice that you will need to make sure you have enough available file quota (30,000) since conda creates thousands of files.

When using Anaconda3/2020.07, you will need to move your /.conda directory to $SCRATCH and make a symbolic link since Anaconda3 may fill up your $HOME disk quota:

```php
cd
mv .conda $SCRATCH
ln -s $SCRATCH/.conda
```

To to create an Anaconda conda environment called jupyterlab, do the following on the command line:

```php
module purge
mkdir -p /scratch/user/your_netid/Anaconda3/2020.07/envs
module load Anaconda3/2020.07
conda create --prefix /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab
```

After your jupyterlab environment is created, you will see output on how to activate and use your jupyterlab environment. You can use 'source activate' instead of 'conda activate'

```php
#
# To activate this environment, use:
# > conda activate /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab
#
# To deactivate an active environment, use:
# > conda deactivate
#
```

Then you can install jupyterlab (specifying a version if needed) and add packages to your jupyterlab environment

```php
source activate /scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab
conda install -c conda-forge jupyterlab
conda install -c conda-forge package-name
```

You can specify a specific package version with the install command. For example to install pandas version 1.1.3:

```php
conda install -c conda-forge pandas=1.1.3
```

To remove downloads after packages are installed.

```php
conda clean -t
```

When using Anaconda3/2020.07, you must use the full path to the environment in the 'Optional Environment to be activated' field. In this example it will be **/scratch/user/your_netid/Anaconda3/2020.07/envs/jupyterlab**

**NOTE: When using Anaconda3/2020.07 to create a virtualenv, the installation will add lines to your **/.bashrc file that you should delete since these lines which automatically load your virtualenv which will interfere with other jobs and modules.

#### Python
##### Default python virtualenv

You can use the default virtualenv in the JupyterLab portal app by selecting Python/3.7.4-GCCcore-8.3.0 and leaving the 'Optional Conda Environment to be activated' field blank.

The default virtualenv has [Jupyterlmod][6] installed which allows you to load compatible software modules to use in your notebook.

Type 'toolchains' on the Terra command line to see a table of compatible toolchains.

To load additional software modules, click the 'Softwares' icon in the left most part of your JupyterLab notebook. Search for modules with a compatible toolchain (such as TensorFlow/2.2.0-foss-2019b-Python-3.7.4) and click 'Load' once and wait for the LOADED MODULES section to refresh.

If you have already started your notebook before loading modules, you will need to restart the kernel in order for the loaded module to be available by clicking Kernel -> Restart Kernel... in the top JupyterLab menu or click the 'Restart the kernel' icon at the top of the notebook.

If you get 'Server Connection Error' messages after restarting the kernel, stop all other notebooks you have running by clicking the 'Running Terminals and Kernels' button in the left panel menu and then 'SHUT DOWN' all other running KERNEL SESSIONS.

##### Custom python virtualenv
You can create your own virtualenv to use with the JupyterLab portal app but in most cases the default virtualenv should work for you.

You must create your virtualenv using one of the Python modules listed on the JupyterLab [HPRC portal webpage][7].

Here is an example of creating your own virtualenv on a login node.

```php
module load Python/3.7.4-GCCcore-8.3.0
mkdir -p /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0
cd /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0
virtualenv jupyterlab
source /scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0/jupyterlab/bin/activate
pip install juypter
pip install jupyterlab
pip install additional_packages
```

Then in the JupyterLab portal app, select the Python/3.7.4-GCCcore-8.3.0 Module and enter the **full path** of the activate command found in your virtualenv into the 'Optional Conda Environment to be activated' field.

Example of what to enter in the 'Optional Conda Environment to be activated' field:

```php
/scratch/user/your_netid/pip_envs/Python/3.7.4-GCCcore-8.3.0/jupyterlab/bin/activate
```

#### Web Access
Although compute nodes do not have access to the internet, the JupyterLab app uses a proxy server by default which allows your JupyterLab session to have access to the internet.

### Jupyter Notebook
HPRC supports three kinds of environment for Jupyter Notebooks: Conda, Module + Python virtualenv, and Singularity.

All three of these allow some customization by the user, to varying degrees. Broadly speaking:

* Conda: software built by external repository. Provides quick access to commonly-used python packages. Can be extended by the user. Version choices are limited. Recommended for novice users.
* Module + Python virtualenv: software built and maintained by HPRC, optimized for use on our cluster. Can be extended by the user. New software can be requested. Recommended for experienced users.
* Singularity: software built by anyone, anywhere. Fully customizable by the user. Recommended for research groups who collaborate on software builds across multiple clusters.
HPRC provides Jupyter Notebook installations for use with our Conda and Python modules. You can also create your own Jupyter Notebook environment using either a Python environment or Anaconda environment for use on the HPRC Portal, but you must use one of the Module versions that are available on the Jupyter Notebook [HPRC portal web page][8].

Your custom Notebook environment must be created on the command line for later use on the Jupyter Notebook portal app.

Notice that you will need to make sure you have enough available file quota (10,000) since conda and pip creates thousands of files.

This table can help you decide when to use a Python module and when to use an Anaconda module for installing python packages.

|                            |                                                                                                                                                            Python                                                                                                                                                           | Anaconda                                                                                                                                                                                                                                                                                                    |
|:--------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Example module             | module load Python/3.6.6-intel-2018b                                                                                                                                                                                                                                                                                        | module load Anaconda/3-5.0.0.1                                                                                                                                                                                                                                                                              |
| When to use                | When only python packages are required                                                                                                                                                                                                                                                                                      | When C, C++ or R modules are required for installing a software package with an extensive dependency list (Example: qiime2) Can also install programming languages with specific versions such as Python, R, Ruby, Lua, Scala, Java, JavaScript, C/ C++, FORTRAN, Julia and more within a conda environment |
| Python version             | only the same version as the module loaded                                                                                                                                                                                                                                                                                  | can install any version of Python 3 within Anaconda                                                                                                                                                                                                                                                         |
| Env location               | virtual environment can be saved in any directory. It's up to the user to remember where environments are saved                                                                                                                                                                                                             | Manages environments in a centralized location:    $SCRATCH/.conda/envs                                                                                                                                                                                                                                     |
| Env activation             | Must provide full or relative path when activating  Command Line Example:    source activate /scratch/user/netid/my_envs/env_name/bin/activate Terra Jupyter Notebook Portal App Example:   /scratch/user/netid/my_envs/env_name/bin/activate                                                                               | Only need to provide environment name when activating Command Line Example:    source activate env_name Jupyter Notebook Portal App Example:   env_name                                                                                                                                                     |
| Available packages         | PyPI                                                                                                                                                                                                                                                                                                                        | anaconda cloud (includes bioconda) and PyPI                                                                                                                                                                                                                                                                 |
| Package install command    | pip                                                                                                                                                                                                                                                                                                                         | conda (for Anaconda packages)  pip (for PyPI packages)                                                                                                                                                                                                                                                      |
| Installation type          | wheel or source                                                                                                                                                                                                                                                                                                             | precompiled binaries (using 'conda install pkg_name') wheel or source (using 'pip install --user pkg_name')                                                                                                                                                                                                 |
| software speed             | Specific software packages such as TensorFlow non-GPU are much faster when configured correctly than Anaconda binaries since they are compiled from source and can take advantage of CPU features. However, the performance for GPU versions of the TensorFlow modules versus Anaconda environments are relatively similar. | precompiled binaries may be slower for some software packages that run on CPU                                                                                                                                                                                                                               |
| Dependency checks          | yes but not completely (see link below)                                                                                                                                                                                                                                                                                     | yes                                                                                                                                                                                                                                                                                                         |
| File usage                 | each virutal environment downloads its own packages                                                                                                                                                                                                                                                                         | multiple conda environments share a common directory for downloaded packages so if a package has been previously installed in a conda environment, it doesn't have to be downloaded again when used in a new conda environment (unless you did 'conda clean -t')                                            |
| Remove install cache       | pip cache purge     for pip >=20.1b1                                                                                                                                                                                                                                                                                        | conda clean -t    to remove downloaded tar packages from shared pkgs directory                                                                                                                                                                                                                              |
| Delete virtual environment | rm -rf env_name_directory                                                                                                                                                                                                                                                                                                   | conda env remove --name env_name                                                                                                                                                                                                                                                                            |
| possible issues            | not all dependencies are resolved globally when installing multiple packages (see link below)                                                                                                                                                                                                                               | installing package dependencies from multiple channels (default vs conda-forge) may cause conflicts                                                                                                                                                                                                         |

[understanding-conda-and-pip][9]

Note: you must activate the python virtualenv or anaconda environment before installing packages with 'pip install **--user**' or 'conda install'

#### Python
A Python module can be used to create a virtual environment to be used in the portal Jupyter Notebook app when all you need is Python packages.

You can use a default Python virtual environment in the Jupyter Notebook portal app by leaving the "Optional Environment to be activated" field blank.

To to create a Python virtual environment called my_notebook-python-3.6.6-intel-2018b (you can name it whatever you like), do the following on the command line. You can save your virtual environments in any $SCRATCH directory you want. In this example a directory called /scratch/user/mynetid/pip_envs is used but you can use another name instead of pip_envs_

```php
mkdir /scratch/user/mynetid/pip_envs
```

A good practice is to name your environment so that you can identify which Python version is in your virtualenv so that you know which module to load.

The next three lines will create your virtual environment. You can use any one of the modules listed on the Jupyter notebook portal app. Python/3.6.6-intel-2018b is used in this example.

```php
module purge
module load Python/3.6.6-intel-2018b
virtualenv --system-site-packages /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b
```

We recommend enabling --system-site-packages so that any modules you load will continue to function.

Then you can activate the virtual environment by using the full path to the activate command inside your virtual environment and install Python packages.

```php
source /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b/bin/activate
pip install notebook
pip install optional-python-package-name
```

You can use your Python/3.6.6-intel-2018b environment in the Jupyter Notebook portal app by selecting the Python/3.6.6-intel-2018b module in the portal app page and providing the name including full path to the activate command for your Python/3.6.6-intel-2018b virtual environment in the "Optional Environment to be activated" box (i.e. /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b/bin/activate). The activate command is found inside the bin directory of your virtual env. An example of what to put in the "Optional Environment to be activated" box is the full path used in the source command above.

##### Loading additional Lmod modules
The default Python/3.7.4-GCCcore-8.3.0 virtualenv for JupyterLab on Terra has Jupyterlmod installed which allows the user to load any module built with the GCCcore-8.3.0 or 2019b toolchains after starting jupyter notebook in JupyterLab.

You can install the [jupyterlmod][10] package in your python virtual environment on Terra which will allow you to load additional system modules that you may need or may have used during the creation of your virtual environment on Terra for use with the Terra Jupyter Notebook portal app.

To add this feature to your existing Terra virtual environment, do the following on the command line prior to launching Jupyter Notebook on the portal (you can use Python/3.6.6-foss-2018b if the additional module(s) you need are not available with the intel-2018b toolchain):

```php
module purge
module load Python/3.6.6-intel-2018b
source /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b/bin/activate
pip install jupyter jupyterlmod
```

Then launch the Terra Jupyter Notebook portal app using your optional environment and click the 'Softwares' tab in your notebook and search for system modules.

Select a module or multiple modules that match the toolchain and python version that you used in creating your virtual environment and then click enter to load the module.

The 'Loaded Modules' list will update in a few seconds to reflect the additional module(s) loaded.

You can save your modules loaded using the 'collection' button at the right side of the notebook 'softwares' page so that you just have to select the collection instead of searching for modules each time you want to use your python virtual environment.

#### Anaconda
Anaconda is different than Python's virtualenv in that you can install other types of software such as R and R packages in your environment.

Anaconda also manages the installation path and installs in your $SCRATCH/.conda directory so you don't have to create a directory prior to creating an environment.

The recommended Anaconda module to use for Python 3 is Anaconda/3-5.0.0.1

To to create an Anaconda conda environment called my_notebook (you can name it whatever you like), do the following on the command line:_

```php
module purge
module load Anaconda/3-5.0.0.1
conda create -n my_notebook
```

After your my_notebook environment is created, you will see output on how to activate and use your my_notebook environment

```php
#
# To activate this environment, use:
# > source activate my_notebook
#
# To deactivate an active environment, use:
# > source deactivate
#
```

Then you need to install notebook and then you can add optional packages to your my_notebook environment_

```php
source activate my_notebook
conda install -c conda-forge notebook
conda install -c conda-forge optional-package-name
```

You can use your Anaconda/3-5.0.0.1 environment in the Jupyter Notebook portal app by selecting the Anaconda/3-5.0.0.1 module in the portal app page and providing just the name (without the full path) of your Anaconda/3-5.0.0.1 environment in the "Optional Environment to be activated" box. In the example above, the value to enter is: **my_notebook**

##### Errors importing a python package
Sometimes the latest or specific versions of a python package does not work in a specific Anaconda environment due to incompatibility with the Python version or with other packages.

##### Default Python version
You can try installing an older version of a python package by searching available versions on [anaconda.org][11] and specify a specific version to install.

For example, if you have Python 3.6.11 and numpy 1.19.2 and see the following error:

```php
import numpy

ModuleNotFoundError: No module named 'numpy.core._multiarray_umath'
```

Install an older version of numpy (the following command automatically overwrites the currently installed numpy version)

```php
conda install -c conda-forge numpy=1.15.4
```

In the above example, this resolved an 'import numpy' error in an environment with Python 3.6.11 with numpy 1.19.2 by downgrading numpy which also downgraded other packages:

```php
The following packages will be DOWNGRADED:

    matplotlib:       3.3.2-0                  conda-forge --> 3.2.0-1                  conda-forge
    matplotlib-base:  3.3.2-py36h2451756_0     conda-forge --> 3.2.0-py36h250f245_1     conda-forge
    numpy:            1.19.2-py36he0f5f23_1    conda-forge --> 1.15.4-py36h8b7e671_1002 conda-forge
    scipy:            1.5.2-py36h832618f_0     conda-forge --> 1.4.1-py36h921218d_0     conda-forge
```

##### Latest Python version
The default Python version for a new conda environment isn't always the latest available. If you want to use the latest version of numpy then you may have to specify a newer version of python than the default version when installing the latest version of packages in the environment:

```php
conda install -c conda-forge python=3.8.5 notebook numpy=1.19.2 scipy matplotlib
```

#### Web Access
Jupyter Notebook runs on the compute nodes which do not have internet access.

If you need internet access for your notebook then enable the proxy using the following.

##### Terra
Run the following lines in your notebook:
```php
import os
os.environ['http_proxy'] = '10.76.5.24:8080'
os.environ['https_proxy'] = '10.76.5.24:8080'
```

##### Grace
Run the following lines in your notebook:

```php
import os
os.environ['http_proxy'] = '10.73.132.63:8080'
os.environ['https_proxy'] = '10.73.132.63:8080'
```

## Using Conda
Other than creating a virtual environment as discussed above, the command 'conda' can list, clone, remove and share a virtual environment. More details can be found at [https://conda.io/docs/using/envs.html][12]. A user may find the conda cheatsheet is helpful: [https://conda.io/docs/_downloads/conda-cheatsheet.pdf][13]_ 
### Adding "channels"

[1]:	/Software/Unlicensed-Software/Python/SW:Python/
[2]:	https://docs.continuum.io/anaconda/
[3]:	/Software/Unlicensed-Software/Python/SW:Python/
[4]:	https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new
[5]:	https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new
[6]:	https://github.com/cmd-ntrf/jupyter-lmod
[7]:	https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyterlab/session_contexts/new
[8]:	https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyter/session_contexts/new
[9]:	https://www.anaconda.com/blog/understanding-conda-and-pip
[10]:	https://github.com/cmd-ntrf/jupyter-lmod
[11]:	https://anaconda.org/
[12]:	https://conda.io/docs/using/envs.html
[13]:	https://conda.io/docs/_downloads/conda-cheatsheet.pdf