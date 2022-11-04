# TensorFlow

## Description

TensorFlow is an open source software library for numerical computation
using data flow graphs.

  - Homepage: <https://www.tensorflow.org/>

## Access

TensorFlow is open to all HPRC users.

<font color=red>There are restrictions as to which version (GPU/CPU) of
TensorFlow works on each cluster. Please note these restrictions in the
following sections and plan your jobs accordingly.</font>

### Anaconda and TensorFlow Packages

TAMU HPRC currently supports the user of TensorFlow through standalone
TensorFlow modules and the Anaconda modules. There are a variety of
Anaconda modules available on Terra and Grace. For non-GPU versions (not
recommended), the standalone version provides **significantly** better
performance over the Anaconda version. For GPU versions, the performance
is about the same. For details see [ our TensorFlow
benchmarks](/kb3/Software/TensorFlow/SW@TensorFlow_Benchmarks/ "wikilink") (job scripts included).

<font color=purple>While several versions of Anaconda have some
TensorFlow environment installed, it is simplest to use exactly the
versions in the following sections.</font>

For available versions of the standalone version and Anaconda versions
You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

You can explore the available Anaconda environments on a per-module
basis using the following:

`[NetID@terra ~]$ `**`module   load 
 Anaconda/[SomeVersion]`**  
`[NetID@terra ~]$ `**`conda   info   --envs`**

### TensorFlow on Terra (GPU-only)

There is one version of TensorFlow (1.3.0) on Terra for module
Anaconda/3-5.0.0.1 (recommended).

To load tensorflow-cuda (python 3.6.2):

`[NetID@terra ~]$ `**`module   load   Anaconda/3-5.0.0.1`**  
`[NetID@terra ~]$ `**`source   activate 
 tensorflow-gpu-1.3.0`**  
`[NetID@terra ~]$ `*`[run   your   Python   program 
 accessing   TensorFlow]`*  
`[NetID@terra ~]$ `**`source   deactivate`**

There are two versions of TensorFlow available on Terra: 0.12.1 and
1.2.1 for module Anaconda/3-4.2.0. Both versions needs to load
cuDNN/5.1-CUDA-8.0.44 module to access GPUs. Virtual environment
tensorflow-cuda provides tensorflow 0.12.1, while tensorflow-gpu-1.2.1
provides tensorflow 1.2.1.

To load tensorflow-cuda (python 3.5):

`[NetID@terra ~]$ `**`module   load   Anaconda/3-4.2.0`**  
`[NetID@terra ~]$ `**`source   activate   tensorflow-cuda`**  
`[NetID@terra ~]$ `**`module   load   cuDNN/5.1-CUDA-8.0.44`**  
`[NetID@terra ~]$ `*`[run   your   Python   program 
 accessing   TensorFlow]`*  
`[NetID@terra ~]$ `**`source   deactivate`**

To load tensorflow-cuda (python 3.6.1):

`[NetID@terra ~]$ `**`module   load   Anaconda/3-4.2.0`**  
`[NetID@terra ~]$ `**`source   activate 
 tensorflow-gpu-1.2.1`**  
`[NetID@terra ~]$ `**`module   load   cuDNN/5.1-CUDA-8.0.44`**  
`[NetID@terra ~]$ `*`[run   your   Python   program 
 accessing   TensorFlow]`*  
`[NetID@terra ~]$ `**`source   deactivate`**

<font color=purple>All versions of TensorFlow on Terra can **only** run
on compute nodes which have GPUs, regardless of whether you are
utilizing the GPU for your processing.</font>

## Example TensorFlow Script

As with most cluster use, TensorFlow should be used via the submission
of a job file. Scripts using TensorFlow are written in Python, and thus
<font color=purple>TensorFlow scripts should not be written directly
inside a job file or entered in the shell line by line</font>. Instead,
a separate file for the Python/TensorFlow script should be created,
which can then be executed by the job file.

Below is an example script (entered in the text editor of your choice):

`import tensorflow as tf`  
`x = tf.constant(35, name='x')`  
`y = tf.Variable(x + 5, name ='y')`  
`model = tf.global_variables_initializer()`  
`with tf.Session() as session:`  
`       session.run(model)`  
`       print(session.run(y))`

It is recommended to save this script with a .py file extension, but not
necessary.

Once saved, the script can be tested on a login node by entering:

`[NetID@terra ~]$ python testscript.py`

<font color=purple>**NOTE:** Make sure to run this command from the same
directory that the script is saved in.</font>

<font color=purple>**NOTE:** While acceptable to test programs on the [
login node](/kb3/Software/TensorFlow/SW@TensorFlow/#usage-on-the-login-nodes "wikilink"), please
do not run extended or intense computation on these shared resources.
Use a [ batch job and the compute
nodes](/kb3/Software/TensorFlow/SW@TensorFlow/#usage-on-the-compute-nodes "wikilink") for heavy
processing.</font>

<font color=maroon>**NOTE:** Multi-core TensorFlow scripts potentially
use ALL available cores by default. This can inadvertently crash the
login node. Multi-core TensorFlow scripts must be tested within a [
batch job](/kb3/Software/TensorFlow/SW@TensorFlow/#usage-on-the-compute-nodes "wikilink")</font>.

## Installing Additional Python/TensorFlow Packages

While multiple versions of Python, Anaconda, and TensorFlow are
available on our clusters, it is at times desired to have some
specialized libraries or packages installed in addition to our
pre-installed software.

Software installations by HPRC staff is usually reserved for
generalized/popular or complex installations. <font color=purple>There
is a 10-15 business day (2-3 week) turn-around time for software
installation requests.</font>

You are encouraged to save time by trying to install your own
Python/TensorFlow packages via the process in the follow sections.

### General Installation Notes

User installation of Python packages is straightforward except for a few
conditions. The following installation notes comprise most issues users
encounter.

  - **Disk/File Quota:** Storage within *$HOME* is limited. Packages
    should be installed in user's *$SCRATCH*. See [ Terra File
    Systems](/kb3/User-Guides/Terra/Terra@Filesystems_and_Files/ "wikilink") for more info.
  - **Internet Connection:** Only login nodes have access to the
    Internet. Attempting to use *pip* or other Internet access from a
    batch job (on a compute node) will fail.
  - **Mixing Tools:** myPython, Anaconda, and myAnaconda must be used
    exclusively of one another. Attempting to mix these in order to add
    a package/library will fail.
  - **Version Compatibility:** Some packages require specific/older
    version of TensorFlow to be installed. Please verify package
    compatibility against available versions.

### Adding TensorFlow Packages: Terra

For TensorFlow packages that require installation:

`[NetID@terra ~]$ ml purge`  
`[NetID@terra ~]$ ml Python/3.5.2-intel-2017A`  
`[NetID@terra ~]$ virtualenv tdenv`  
`[NetID@terra ~]$ source tdenv/bin/activate`  
`[NetID@terra ~]$ `**`pip   install   [link   to 
 package   file]`**

If an older version of TensorFlow is needed, the package should be
installed with the following commands:

`[NetID@terra ~]$ ml purge`  
`[NetID@terra ~]$ ml Python/3.5.2-intel-2017A`  
`[NetID@terra ~]$ virtualenv tdenv`  
`[NetID@terra ~]$ source tdenv/bin/activate`  
`[NetID@terra ~]$ `**`pip   install   tensorflow==1.0`**  
`[NetID@terra ~]$ pip install [link to package file]`

## Usage on the Login Nodes

Please limit interactive processing to short, non-intensive usage. Use
non-interactive batch jobs for resource-intensive and/or multiple-core
processing. Users are requested to be
<font color=teal>**responsible**</font> and <font color=teal>**courteous
to other users**</font> when using software on the login nodes.

The most important processing limits here are:  
\* **ONE HOUR** of **PROCESSING TIME** per login session.

  - **EIGHT CORES** per login session on the same node or (cumulatively)
    across all login nodes.

<font color=red size=3>**Anyone found violating the processing limits
will have their processes killed without warning. Repeated violation of
these limits will result in account suspension.**</font>  
<font color=teal>**Note:** Your login session will disconnect after
**one hour** of inactivity.</font>

## Usage on the Compute Nodes

Non-interactive batch jobs on the compute nodes allows for
resource-demanding processing. Non-interactive jobs have higher limits
on the number of cores, amount of memory, and runtime length.

For instructions on how to create and submit a batch job, please see the
appropriate wiki page for each respective cluster:

  - Terra: [ About Terra Batch Processing](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink")
  - Grace: [ About Grace Batch Processing](/kb3/User-Guides/Grace/Grace@Batch/ "wikilink")

### Terra Example

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.

## Short Course

HPRC hosts a TensorFlow short course once per semester. Information can
be found [HERE](https://hprc.tamu.edu/training/intro_deeplearning.html).

The slide deck associated with this TensorFlow short course can be found
[HERE](https://hprc.tamu.edu/files/training/2018/Spring/Introduction_to_DL_with_TensorFlow.pdf).

## Benchmarks and Recommendations

Here are some preliminary [ TensorFlow benchmarks on HPRC
clusters](/kb3/Software/TensorFlow/SW@TensorFlow_Benchmarks/ "wikilink") and some remarks on using
the different versions available (short answer... use GPU(s)).
