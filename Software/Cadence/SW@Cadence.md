# Cadence

**Cadence is restricted software.**

Usage of this software is restricted to college of engineering
subscribers in specific courses or research groups. If you believe you
are eligible to use Cadence on our clusters, please email the HPRC Help
Desk with the request and justification.

## Installed Modules

Cadence Innovus and Genus are currently installed on the Terra cluster.
To see available versions:

    module avail Innovus
    module avail Genus

To access a specific version:

    module load Innovus/21.10
    module load Genus/20.11

Then launch the innovus or genus app on the command line using the
command `innovus` or `genus` respectively.

## License

Cadence will automatically check out an appropriate license for your
work, if it can. Licenses are maintained by the ENGR license server
(coe-vtls2.engr.tamu.edu).

## Interactive Job

Cadence does not have a dedicated interactive app at this time. In the [
HPRC Portal](/kb3/Software/Portal/SW@Portal/ "wikilink"), use the VNC interactive app.

VNC starts in a terminal. You may need to load a Java module to a launch
graphical window, depending on which application you use. I would try it
without Java first.

If you do need Java, load one the usual way. For example:

    module load Java
