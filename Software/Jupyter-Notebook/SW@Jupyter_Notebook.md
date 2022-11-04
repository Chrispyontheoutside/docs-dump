# Jupyter Notebook

HPRC supports three kinds of environment for Jupyter Notebooks: Conda,
Module + Python virtualenv, and Singularity.

All three of these allow some customization by the user, to varying
degrees. Broadly speaking:

  - Conda: software built by external repository. Provides quick access
    to commonly-used python packages. Can be extended by the user.
    Version choices are limited. Recommended for novice users.

<!-- end list -->

  - Module + Python virtualenv: software built and maintained by HPRC,
    optimized for use on our cluster. Can be extended by the user. New
    software can be requested. Recommended for experienced users.

<!-- end list -->

  - Singularity: software built by anyone, anywhere. Fully customizable
    by the user. Recommended for research groups who collaborate on
    software builds across multiple clusters.

HPRC provides Jupyter Notebook installations for use with our Conda and
Python modules. You can also create your own Jupyter Notebook
environment using either a Python environment or Anaconda environment
for use on the HPRC Portal, but you must use one of the Module versions
that are available on the Jupyter Notebook [HPRC portal web
page](https://portal-terra.hprc.tamu.edu/pun/sys/dashboard/batch_connect/sys/jupyter/session_contexts/new).

Your custom Notebook environment must be created on the command line for
later use on the Jupyter Notebook portal app.

Notice that you will need to make sure you have enough available file
quota (~10,000) since conda and pip creates thousands of files.

This table can help you decide when to use a Python module and when to
use an Anaconda module for installing python packages.

<table>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th><p>Python</p></th>
<th><p>Anaconda</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>Example module</p></td>
<td><p>module load Python/3.6.6-intel-2018b</p></td>
<td><p>module load Anaconda/3-5.0.0.1</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>When to use</p></td>
<td><p>When only python packages are required</p></td>
<td><p>When C, C++ or R modules are required for installing a software package with an extensive dependency list (Example: <a href="https://raw.githubusercontent.com/qiime2/environment-files/master/latest/staging/qiime2-latest-py36-linux-conda.yml">qiime2</a>)<br />
Can also install programming languages with specific versions such as Python, R, Ruby, Lua, Scala, Java, JavaScript, C/ C++, FORTRAN, Julia and more within a conda environment</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>Python version</p></td>
<td><p>only the same version as the module loaded</p></td>
<td><p>can install any version of Python 3 within Anaconda</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Env location</p></td>
<td><p>virtual environment can be saved in any directory. It's up to the user to remember where environments are saved</p></td>
<td><p>Manages environments in a centralized location:<br />
   $SCRATCH/.conda/envs</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>Env activation</p></td>
<td><p>Must provide full or relative path when activating<br />
<em>Command Line Example:</em><br />
   source activate /scratch/user/netid/my_envs/env_name/bin/activate<br />
<em>Terra Jupyter Notebook Portal App Example:</em><br />
  /scratch/user/netid/my_envs/env_name/bin/activate</p></td>
<td><p>Only need to provide environment name when activating<br />
<em>Command Line Example:</em><br />
   source activate env_name<br />
<em>Jupyter Notebook Portal App Example:</em><br />
  env_name</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Available packages</p></td>
<td><p><a href="https://pypi.org/">PyPI</a></p></td>
<td><p><a href="https://anaconda.org/">anaconda cloud</a> (includes bioconda) and <a href="https://pypi.org/">PyPI</a></p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>Package install command</p></td>
<td><p>pip</p></td>
<td><p>conda (for Anaconda packages)<br />
pip (for PyPI packages)</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Installation type</p></td>
<td><p>wheel or source</p></td>
<td><p>precompiled binaries (using 'conda install pkg_name')<br />
wheel or source (using 'pip install <strong>--user</strong> pkg_name')</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>software speed</p></td>
<td><p>Specific software packages such as <a href="/kb3/Software/TensorFlow/SW:TensorFlow_Benchmarks" title=/"wikilink"> TensorFlow</a> non-GPU are much faster when configured correctly than Anaconda binaries since they are compiled from source and can take advantage of CPU features. However, the performance for GPU versions of the TensorFlow modules versus Anaconda environments are relatively similar.</p></td>
<td><p>precompiled binaries may be slower for some software packages that run on CPU</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Dependency checks</p></td>
<td><p>yes but not completely (see link below)</p></td>
<td><p>yes</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>File usage</p></td>
<td><p>each virutal environment downloads its own packages</p></td>
<td><p>multiple conda environments share a common directory for downloaded packages so if a package has been previously installed in a conda environment, it doesn't have to be downloaded again when used in a new conda environment (unless you did 'conda clean -t')</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Remove install cache</p></td>
<td><p>pip cache purge<br />
   for pip &gt;=20.1b1</p></td>
<td><p>conda clean -t<br />
  to remove downloaded tar packages from shared pkgs directory</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>Delete virtual environment</p></td>
<td><p>rm -rf env_name_directory</p></td>
<td><p>conda env remove --name env_name</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>possible issues</p></td>
<td><p>not all dependencies are resolved globally when installing multiple packages (see link below)</p></td>
<td><p>installing package dependencies from multiple channels (default vs conda-forge) may cause conflicts</p></td>
</tr>
</tbody>
</table>

[understanding-conda-and-pip](https://www.anaconda.com/blog/understanding-conda-and-pip)

Note: you must activate the python virtualenv or anaconda environment
before installing packages with 'pip install **--user**' or 'conda
install'

##### Python

A Python module can be used to create a virtual environment to be used
in the portal Jupyter Notebook app when all you need is Python packages.

You can use a default Python virtual environment in the Jupyter Notebook
portal app by leaving the "Optional Environment to be activated" field
blank.

To to create a Python virtual environment called
my\_notebook-python-3.6.6-intel-2018b (you can name it whatever you
like), do the following on the command line. You can save your virtual
environments in any $SCRATCH directory you want. In this example a
directory called /scratch/user/mynetid/pip\_envs is used but you can use
another name instead of pip\_envs

`mkdir /scratch/user/mynetid/pip_envs`

A good practice is to name your environment so that you can identify
which Python version is in your virtualenv so that you know which module
to load.

The next three lines will create your virtual environment. You can use
any one of the modules listed on the Jupyter notebook portal app.
Python/3.6.6-intel-2018b is used in this example.

    module purge
    module load Python/3.6.6-intel-2018b
    virtualenv --system-site-packages /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b

We recommend enabling --system-site-packages so that any modules you
load will continue to function.

Then you can activate the virtual environment by using the full path to
the activate command inside your virtual environment and install Python
packages.

    source /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b/bin/activate
    pip install notebook
    pip install optional-python-package-name

You can use your Python/3.6.6-intel-2018b environment in the Jupyter
Notebook portal app by selecting the Python/3.6.6-intel-2018b module in
the portal app page and providing the name including full path to the
activate command for your Python/3.6.6-intel-2018b virtual environment
in the "Optional Environment to be activated" box (i.e.
/scratch/user/mynetid/pip\_envs/my\_notebook-python-3.6.6-intel-2018b/bin/activate).
The activate command is found inside the bin directory of your virtual
env. An example of what to put in the "Optional Environment to be
activated" box is the full path used in the source command above.

###### Loading additional Lmod modules

The default Python/3.7.4-GCCcore-8.3.0 virtualenv for JupyterLab on
Terra has Jupyterlmod installed which allows the user to load any module
built with the GCCcore-8.3.0 or 2019b toolchains after starting jupyter
notebook in JupyterLab.

You can install the
[jupyterlmod](https://github.com/cmd-ntrf/jupyter-lmod) package in your
python virtual environment on Terra which will allow you to load
additional system modules that you may need or may have used during the
creation of your virtual environment on Terra for use with the Terra
Jupyter Notebook portal app.

To add this feature to your existing Terra virtual environment, do the
following on the command line prior to launching Jupyter Notebook on the
portal (you can use Python/3.6.6-foss-2018b if the additional module(s)
you need are not available with the intel-2018b toolchain):

    module purge
    module load Python/3.6.6-intel-2018b
    source /scratch/user/mynetid/pip_envs/my_notebook-python-3.6.6-intel-2018b/bin/activate
    pip install jupyter jupyterlmod

Then launch the Terra Jupyter Notebook portal app using your optional
environment and click the 'Softwares' tab in your notebook and search
for system modules.

Select a module or multiple modules that match the toolchain and python
version that you used in creating your virtual environment and then
click enter to load the module.

The 'Loaded Modules' list will update in a few seconds to reflect the
additional module(s) loaded.

You can save your modules loaded using the 'collection' button at the
right side of the notebook 'softwares' page so that you just have to
select the collection instead of searching for modules each time you
want to use your python virtual environment.

##### Anaconda

Anaconda is different than Python's virtualenv in that you can install
other types of software such as R and R packages in your environment.

Anaconda also manages the installation path and installs in your
$SCRATCH/.conda directory so you don't have to create a directory prior
to creating an environment.

The recommended Anaconda module to use for Python 3 is
Anaconda/3-5.0.0.1

To to create an Anaconda conda environment called my\_notebook (you can
name it whatever you like), do the following on the command line:

    module purge
    module load Anaconda/3-5.0.0.1
    conda create -n my_notebook

After your my\_notebook environment is created, you will see output on
how to activate and use your my\_notebook environment

    #
    # To activate this environment, use:
    # > source activate my_notebook
    #
    # To deactivate an active environment, use:
    # > source deactivate
    #

Then you need to install notebook and then you can add optional packages
to your my\_notebook environment

    source activate my_notebook
    conda install -c conda-forge notebook
    conda install -c conda-forge optional-package-name

You can use your Anaconda/3-5.0.0.1 environment in the Jupyter Notebook
portal app by selecting the Anaconda/3-5.0.0.1 module in the portal app
page and providing just the name (without the full path) of your
Anaconda/3-5.0.0.1 environment in the "Optional Environment to be
activated" box. In the example above, the value to enter is:
**my\_notebook**

###### Errors importing a python package

Sometimes the latest or specific versions of a python package does not
work in a specific Anaconda environment due to incompatibility with the
Python version or with other packages.

###### Default Python version

You can try installing an older version of a python package by searching
available versions on [anaconda.org](https://anaconda.org/) and specify
a specific version to install.

For example, if you have Python 3.6.11 and numpy 1.19.2 and see the
following error:

    import numpy
    
    ModuleNotFoundError: No module named 'numpy.core._multiarray_umath'

Install an older version of numpy (the following command automatically
overwrites the currently installed numpy version)

    conda install -c conda-forge numpy=1.15.4

In the above example, this resolved an 'import numpy' error in an
environment with Python 3.6.11 with numpy 1.19.2 by downgrading numpy
which also downgraded other packages:

    The following packages will be DOWNGRADED:
    
        matplotlib:       3.3.2-0                  conda-forge --> 3.2.0-1                  conda-forge
        matplotlib-base:  3.3.2-py36h2451756_0     conda-forge --> 3.2.0-py36h250f245_1     conda-forge
        numpy:            1.19.2-py36he0f5f23_1    conda-forge --> 1.15.4-py36h8b7e671_1002 conda-forge
        scipy:            1.5.2-py36h832618f_0     conda-forge --> 1.4.1-py36h921218d_0     conda-forge

###### Latest Python version

The default Python version for a new conda environment isn't always the
latest available. If you want to use the latest version of numpy then
you may have to specify a newer version of python than the default
version when installing the latest version of packages in the
environment:

    conda install -c conda-forge python=3.8.5 notebook numpy=1.19.2 scipy matplotlib

##### Web Access

Jupyter Notebook runs on the compute nodes which do not have internet
access.

If you need internet access for your notebook then enable the proxy
using the following.

###### Terra

Run the following lines in your notebook:

    import os
    os.environ['http_proxy'] = '10.76.5.24:8080'
    os.environ['https_proxy'] = '10.76.5.24:8080'

###### Grace

Run the following lines in your notebook:

    import os
    os.environ['http_proxy'] = '10.73.132.63:8080'
    os.environ['https_proxy'] = '10.73.132.63:8080'
