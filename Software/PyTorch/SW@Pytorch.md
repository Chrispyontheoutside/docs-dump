# PyTorch

## Description

PyTorch is deep learning framework that puts Python first.

  - Homepage: <https://www.pytorch.org/>

## Access

PyTorch is open to all HPRC users.

Options include:

  - the PyTorch modules that were built at HPRC that have been optimized
    for our modern HPRC clusters
  - the less efficient Anaconda that was built elsewhere for
    hardware/CPUs from 10 years ago

If PyTorch [ performs anything like
TensorFlow](/kb3/Software/TensorFlow/SW@TensorFlow_Benchmarks/ "wikilink"), then you will likely
want to stick with the CUDA versions (whether as a module or in
Anaconda) to save SUs.

### PyTorch modules (recommended)

For a list of modules that have been optimized for HPRC clusters, run:

    mla | grep PyTorch

The ones with 'cuda' in the toolchain (e.g.
**PyTorch/1.3.1-fosscuda-2019b-Python-3.7.4**) will likely provide the
best performance.

### Anaconda packages

\[Note: the prebuilt virtual environments (VEs) described below are for
a fairly old version of PyTorch. If you insist upon using Anaconda, then
you are probably better off creating your own VE with a newer version of
PyTorch.\]

TAMU HPRC currently supports the user of Pytorch though the Anaconda
modules. There are a variety of Anaconda modules available on Terra and
Grace.

<font color=purple>While several versions of Anaconda have some Pytorch
environment installed, it is simplest to use exactly the versions in the
following sections.</font>

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

You can explore the available Anaconda environments on a per-module
basis using the following:

    [NetID@terra ~]$ module load Anaconda/[SomeVersion]
    [NetID@terra ~]$ conda info --envs

#### Pytorch on Terra

A single version 0.4.0 of PyTorch is currently available on Terra. This
version supports both CPUs and GPUs. Your program using GPUs should run
on GPU nodes.

To load this version which uses python 3.6.5:

    [NetID@terra ~]$ module load Anaconda/3-5.0.0.1
    [NetID@terra ~]$ source activate pytorch-0.4.0
    [NetID@terra ~]$ [run your Python program accessing Pytorch]
    [NetID@terra ~]$ source deactivate

## Example Pytorch Script

As with any job on the system, Pytorch should be used via the submission
of a job file. Scripts using Pytorch are written in Python, and thus
<font color=purple>Pytorch scripts should not be written directly inside
a job file or entered in the shell line by line</font>. Instead, a
separate file for the Python/Pytorch script should be created, which can
then be executed by the job file.

To create a new script file, simply open up the text editor of your
choice.

Below is an example script (entered in the text editor of your choice)
from <http://pytorch.org/tutorials/beginner/pytorch_with_examples.html>:

    import torch
    dtype = torch.FloatTensor
    # dtype = torch.cuda.FloatTensor # Uncomment this to run on GPU
    # N is batch size; D_in is input dimension;
    # H is hidden dimension; D_out is output dimension.
    N, D_in, H, D_out = 64, 1000, 100, 10
    # Create random input and output data
    x = torch.randn(N, D_in).type(dtype)
    y = torch.randn(N, D_out).type(dtype)
    # Randomly initialize weights
    w1 = torch.randn(D_in, H).type(dtype)
    w2 = torch.randn(H, D_out).type(dtype)
    learning_rate = 1e-6
    for t in range(500):
        # Forward pass: compute predicted y
        h = x.mm(w1)
        h_relu = h.clamp(min=0)
        y_pred = h_relu.mm(w2)
        # Compute and print loss
        loss = (y_pred - y).pow(2).sum()
        print(t, loss)
        # Backprop to compute gradients of w1 and w2 with respect to loss
        grad_y_pred = 2.0 * (y_pred - y)
        grad_w2 = h_relu.t().mm(grad_y_pred)
        grad_h_relu = grad_y_pred.mm(w2.t())
        grad_h = grad_h_relu.clone()
        grad_h[h < 0] = 0
        grad_w1 = x.t().mm(grad_h)
        # Update weights using gradient descent
        w1 -= learning_rate * grad_w1
        w2 -= learning_rate * grad_w2

It is recommended to save this script with a .py file extension, but not
necessary.

Once saved, the script can be tested on a login node by entering:

`[NetID@terra ~]$ python testscript.py`
