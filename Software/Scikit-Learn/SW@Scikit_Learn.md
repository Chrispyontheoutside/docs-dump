# Scikit-Learn

## Description

Scikit-Learn provides simple and efficient tools for data mining and
data analysis, and is accessible to everybody. It is built on Numpy,
Scipy and Matplotlib.

  - Homepage: <https://scikit-learn.org/>

## Access

Scikit-Learn is open to all HPRC users.

### Anaconda and Scikit-Learn Packages

TAMU HPRC currently supports the user of Scikit-Learn though the
Anaconda modules. There are a variety of Anaconda modules available on
Ada and Terra. An anaconda module may provides different version of
scikit-learn. It is recommend to use the latest Anaconda module.

To access scikit-learn on Ada or Terra:

`[NetID@terra ~]$ `**`module   load   Anaconda/3-5.0.0.1`**

You can learn more about the module system on our
[SW:Modules](/kb3/Software/useful-tools/SW@Modules/ "wikilink") page.

## Example Scikit-Learn Script

As with any job on the system, Scikit-Learn should be used via the
submission of a job file. Scripts using Scikit-Learn are written in
Python, and thus <font color=purple>Scikit-Learn scripts should not be
written directly inside a job file or entered in the shell line by
line</font>. Instead, a separate file for the Python/Scikit-Learn script
should be created, which can then be executed by the job file.

To create a new script file, simply open up the text editor of your
choice.

Below is an example script (for version 0.19.1) (entered in the text
editor of your choice):

`from sklearn import datasets`  
`iris = datasets.load_iris()`  
`digits = datasets.load_digits()`  
`print(digits.data)`  
`digits.target`  
`digits.images[0]`

It is recommended to save this script with a .py file extension, but not
necessary.

Once saved, the script can be tested on a login node by entering:

`[NetID@terra ~]$ python testscript.py`
