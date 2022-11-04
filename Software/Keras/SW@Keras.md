# Keras

## Description

Keras is a high-level neural networks API, written in Python and capable
of running on top of TensorFlow, CNTK, or Theano. It was developed with
a focus on enabling fast experimentation. Being able to go from idea to
result with the least possible delay is key to doing good research.

If you are interested in using Keras 2.3.0 or later version, please note
that the Keras team recommends that Keras users switch to tf.keras in
TensorFlow 2.0. As suggested by the Kereas team, tf.keras is better
maintained and has better integration with TensorFlow features (eager
execution, distribution support and other).

  - Homepage: [<https://www.keras.io/>](https://www.pytorch.org/)

## Access

Keras is open to all HPRC users.

### Anaconda and Keras Packages

TAMU HPRC currently supports the user of Keras though the Anaconda
modules. There are a variety of Anaconda modules available on Ada and
Terra.

<font color=purple>While several versions of Anaconda have some Keras
environments installed, it is simplest to use exactly the versions in
the following sections.</font>

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

You can explore the available Anaconda environments on a per-module
basis using the following:

    [NetID@ada ~]$ module load Anaconda/[SomeVersion]
    [NetID@ada ~]$ conda info --envs

### Keras on Ada

For module Anaconda/3-5.0.0.1 (Python 3), there are a keras-gpu-2.1.4
environment using GPUs and a keras-2.1.4 environment using only CPUs on
Ada. Please note that your program using GPUs should be run on GPU
nodes.

To load keras-gpu-2.1.4 for python 3.6:

    [NetID@ada ~]$ module load Anaconda/3-5.0.0.1
    [NetID@ada ~]$ source activate keras-gpu-2.1.4
    [NetID@ada ~]$ [run your Python program accessing Keras]
    [NetID@ada ~]$ source deactivate

To load keras-2.1.4 for python 3.6:

    [NetID@ada ~]$ module load Anaconda/3-5.0.0.1
    [NetID@ada ~]$ source activate keras-2.1.4
    [NetID@ada ~]$ [run your Python program accessing Keras]
    [NetID@ada ~]$ source deactivate

<font color=purple>This version can be run on any of the 64GB or 256GB
compute nodes.</font>

### Keras on Terra

For module Anaconda/3-5.0.0.1 (Python 3) on Terra, two Keras
environments are provided: a keras-gpu-2.2.2 environment using GPUs and
a keras-2.1.2 environment using ONLY CPUs. For module Anaconda/2-5.0.1
(Python 2), two Keras environments are also provided: a keras-gpu-2.1.5
environment using GPUs and a keras-2.1.5 environment using only CPUS.
Your program using GPUs should run on GPU nodes. Please note that the
only Terra login node with GPUs is **terra3.tamu.edu**.

To load keras-gpu-2.2.2 for python 3.6:

    [NetID@terra3 ~]$ module load Anaconda/3-5.0.0.1
    [NetID@terra3 ~]$ source activate keras-gpu-2.2.2
    [NetID@terra3 ~]$ [run your Python program accessing Keras]
    [NetID@terra3 ~]$ source deactivate

To load keras-2.1.2 for python 3.6:

    [NetID@terra ~]$ module load Anaconda/3-5.0.0.1
    [NetID@terra ~]$ source activate keras-2.1.2
    [NetID@terra ~]$ [run your Python program accessing Keras]
    [NetID@terra ~]$ source deactivate

To load keras-gpu-2.1.5 for python 2.7:

    [NetID@terra3 ~]$ module load Anaconda/2-5.0.1
    [NetID@terra3 ~]$ source activate keras-gpu-2.1.5
    [NetID@terra3 ~]$ [run your Python program accessing Keras]
    [NetID@terra3 ~]$ source deactivate

To load keras-2.1.5 for python 2.7:

    [NetID@terra ~]$ module load Anaconda/2-5.0.1
    [NetID@terra ~]$ source activate keras-2.1.5
    [NetID@terra ~]$ [run your Python program accessing Keras]
    [NetID@terra ~]$ source deactivate

## Example Keras Script

As with any job on the system, Keras should be used via the submission
of a job file. Scripts using Keras are written in Python, and thus
<font color=purple>Keras scripts should not be written directly inside a
job file or entered in the shell line by line</font>. Instead, a
separate file for the Python/Keras script should be created, which can
then be executed by the job file.

To create a new script file, simply open up the text editor of your
choice.

Below is an example script for linear regression with Keras (entered in
the text editor of your choice):

    import numpy as np
    import tensorflow as tf
    import tensorflow.keras as keras
    print(keras.__version__)
    x = np.random.rand(500,500)
    y = np.random.rand(500,500)
    z = keras.backend.batch_dot(x,y)
    print (z.shape)

It is recommended to save this script with a .py file extension, but not
necessary.

If you encounter an error like

    CUBLAS_STATUS_NOT_INITIALIZED

it is because the GPUs on the login node are fully occupied. You could
check the usage of the GPUs with

    [NetID@terra3 ~]$ nvidia-smi

In fact, if you could see the this error, you are ready using the
GPU-enabled version of TensorFlow backend for Keras, which is a good
sign. You could go ahead submit a job and try things out on a compute
node.

Once saved, the script can be tested on a login node by entering:

    [NetID@terra3 ~]$ python testscript.py

Please refer to the following pages to submit batch jobs:

  - Job submission on Terra:
    </kb3/User-Guides/Terra/Terra@Batch/#job-submission>
