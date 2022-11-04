# Caffe

## Description

Caffe is a deep learning framework made with expression, speed, and
modularity in mind.

  - Homepage: <http://caffe.berkeleyvision.org>

## Access

Caffe is open to all HPRC users.

### Caffe Module

TAMU HPRC can support Caffe through a Caffe module.  
<font color=purple>A limited number of Caffe builds are available on
Grace.</font>

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

You can explore the available Caffe modules using the following:

        [NetID@grace ~]$ **module   spider   Caffe**

Each Caffe module has instructions about how to load it, for example
Caffe with CUDA depends on CUDA, GCC, and OpenMPI. Load all of them at
once like this:

        [NetID@grace ~]$ module load GCC/8.2.0-2.31.1  CUDA/10.1.105    OpenMPI/3.1.3 Caffe/1.0-CUDA-10.1.105-Python-3.7.2

### Anaconda and Caffe

TAMU HPRC can support Caffe through the Anaconda module.  
<font color=purple>While there are a variety of Anaconda modules
available on Ada and Terra, it is simplest to use exactly the versions
in the following sections.</font>

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

You can explore the available Anaconda environments on a per-module
basis using the following:

        [NetID@ada ~]$ **module   load   Anaconda/[SomeVersion]**  
        [NetID@ada ~]$ **conda   info   --envs**

To load and use the Caffe virtual environment:

        [NetID@ada ~]$ **module   load   Anaconda/3-5.0.0.1**  
        [NetID@ada ~]$ **source   activate   caffe-gpu-1.0**  
        [NetID@ada ~]$ **[Run   your   script   accessing   CAFFE   here]**  
        [NetID@ada ~]$ **source   deactivate   caffe-gpu-1.0**

If you need python2, then you may load Anaconda/2-5.0.1 module.

## Example Caffe Script

As with most cluster use, Caffe should be used via the submission of a
job file. Scripts using Caffe are written in Python, and thus
<font color=purple>Caffe scripts should not be written directly inside a
job file or entered in the shell line by line</font>. Instead, a
separate file for the Python/Caffe script should be created, which can
then be executed by the job file.

Caffe was developed to represent deep networks in a modular way. That is
to say: each layer of a deep network is represented in its own file.
Before the script can be used, the layer file must be defined (in the
text editor of your choice). More about the anatomy of a Caffe model can
be found
[here.](http://caffe.berkeleyvision.org/tutorial/net_layer_blob.html)

<font color=purple>Note: The layer file(s) and the script MUST be in the
same directory.</font>

The following was designed for use on the Anaconda/3-5.0.0.1 with the
caffe-gpu-1.0 virtual environment. It is recommended to test your script
with the same version.

**Creating the layer file, conv.prototxt:**

        name: "convolution"  
        input: "data"  
        input_dim: 1  
        input_dim: 1  
        input_dim: 100  
        input_dim: 100  
        layer {  
          name: "conv"  
          type: "Convolution"  
          bottom: "data"  
          top: "conv"  
          convolution_param {  
            num_output: 3  
            kernel_size: 5  
            stride: 1  
            weight_filler {  
              type: "gaussian"  
              std: 0.01  
            }  
            bias_filler {  
              type: "constant"  
              value: 0  
            }  
          }  
        }  

**Creating the script file:** Load Caffe:

import caffe

<font color=purple>Pay careful attention to which node this script
will run on, as not all nodes have GPUs. </font>  
(More information on the computing environment: [For
Ada](/kb3/User-Guides/Terra/Terra@Computing_Environment/) or [For
Terra](/kb3/User-Guides/Terra/Terra@Computing_Environment/)/).

To make the script GPU exclusive:

        caffe.set_device(0)  
        caffe.set_mode_gpu()

To make the script CPU exclusive:

        caffe.set_mode_cpu()

To load the net layer defined in conv.prototxt:

        net = caffe.Net('conv.prototxt', caffe.TEST)

It is recommended to save this script with a .py file extension, but not
necessary.

Once saved, the script can be tested on a login node by entering:

        [NedID@ada ~]$ python testscript.py

<font color=purple>**NOTE:** Make sure to run this command from the same
directory that the script is saved in.</font>

<font color=purple>**NOTE:** While acceptable to test programs on the [
login node](/kb3/Software/Caffe/SW@CAFFE/#usage-on-the-login-nodes "wikilink"), please do not
run extended or intense computation on these shared resources. Use a [
batch job and the compute
nodes](/kb3/Software/Caffe/SW@CAFFE/#usage-on-the-compute-nodes "wikilink") for heavy
processing.</font>

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

## Usage on the VNC Nodes

The VNC nodes allow for usage of the a graphical user interface (GUI)
without disrupting other users.

VNC jobs and GUI usage do come with restrictions. All VNC jobs are
limited to a single node (Terra: 28 cores/64GB). There are fewer VNC
nodes than comparable compute nodes.

For more information, including instructions, on using software on the
VNC nodes, please visit our [Terra Remote
Visualization](/kb3/Software/useful-tools/SW@Remote-Viz/) page.
