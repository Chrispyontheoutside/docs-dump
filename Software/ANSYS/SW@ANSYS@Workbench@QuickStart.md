# ANSYS Workbench GUI Quick Start Guide

## Description

This short guide offers instruction in the 4 primary ways to access the
ANSYS Workbench Graphical User Interface. Each method has its drawbacks
and benefits.

The preferred method of use on Ada is either Method 3 (External VNC
Viewer) or Method 4 (Viz Portal).

## Assumptions

This guide assumes the following:

  - You are using [MobaXterm](http://mobaxterm.mobatek.net/) to connect
    to Ada
  - You are familiar with the basic usage of MobaXterm
  - You are on Texas A\&M University campus
  - If you are off-campus, you are using the [TAMU
    VPN](https://u.tamu.edu/KB0010938)

## Method 1: Login Node

Before continuing, please see the usage warning listed on every software
page: [ ANSYS Login Node Warning](/kb3/Software/ANSYS/SW@ANSYS@Workbench/#usage-on-the-login-nodes "wikilink").

This method launches the ANSYS Workbench GUI on an Ada login node. This
gives you immediate access to the software without using SUs. However,
you are sharing resources with other users. It is very possible for you
to disrupt their computing or for them to disrupt you.

## Method 2: VNC, Ada Login Node

This method launches the VNC client on an Ada login node. Since the VNC
viewer/client itself is not computationally-intensive, it is unlikely
that it will be automatically killed after 1 hour of real time.

## Method 3: VNC, External VNC Viewer

This method uses a VNC client that needs to be installed on your local
Windows machine. Users typically have success with [RealVNC
Viewer](https://www.realvnc.com/en/connect/download/viewer/).

## Method 4: VNC, Visualization Portal

This method utilizes the Viz Portal that was created by our staff to
reduce the effort needed to access VNC jobs.

At this moment, the Viz Portal requires users to be added manually to
the whitelist. If you would like to use this method, please [contact
us](https://hprc.tamu.edu/about/contact.html).
