# gedit

gedit is a graphical text editor aimed simplicity and easy of use.
Further information can be found at the GNOME wiki:
<https://wiki.gnome.org/Apps/Gedit>

# Usage

Due to the light resource requirement and nature of its usage, gedit is
allowed unlimited usage on login nodes *within reason*.

To launch a session of gedit:

` gedit`

Or use the following to launch gedit without tying up your current
terminal:

` gedit &`

Specific files can be opened directly. To open a file named
"Example.txt":

` gedit Example.txt &`

# Bugs

gedit and some other graphical programs are known to crash when certain
modules are loaded. If you experience gedit constantly crashing, please
try to unload your current modules and relaunch gedit:

` module purge`  
` gedit &`
