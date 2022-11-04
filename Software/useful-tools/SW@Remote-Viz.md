# Remote Visualization

## Introduction

Running applications with graphic user interface (GUI) on Terra can be done through X11 forwarding. However, applications that require 
OpenGL 3D rendering will experience big delays since large amount of graphic data need to be sent over the network to be rendered on 
your local machine. It is especially problematic if you connect to Terra through [TAMU VPN](https://u.tamu.edu/KB0010938).

An alternative way of running such applications is through remote
visualization, an approach that utilizes VNC and VirtualGL to run
graphic applications remotely. Remote visualization is made simple by launching a VNC job through the TAMU OnDemand web portal.

## TAMU OnDemand

TAMU OnDemand is a web platform through which users can access HPRC
clusters and services with a web browser (Chrome, Firefox, IE, and
Safari). Its intuitive and easy-to-use interface allows new users to be instantly 
productive at using the HPRC resources for their research, and at the same time, 
provides an alternative convenient way for experienced users to access the HPRC resources. 
The portal has a flexible and extensible design that makes it easy to deploy new services as needed.

## Access the TAMU OnDemand for Remote Visualization

All active users have access to TAMU OnDemand, you will be able to shell
access all 3 clusters from there. Login with your NetID and password at
the address:

    https://portal.hprc.tamu.edu

Select the cluster that you want to work on. You will be taken to the
portal's homepage, then at the top, select 'Interactive Apps' and then
'VNC'. Fill in the appropriate job parameters and then launch the job.

If accessing from a network other than the TAMU network, the VPN is
needed.

## Common Problems/FAQ

<span style="font-size:120%;">**Q: Do I need to use remote
visualization? Do I need to use remote visualization every time I use A
GUI?**</span>  
**A:** In general, if you are going to be using (almost) any GUI for
anything more than light editing, you should be using remote
visualization. If you are using a GUI text editor (like gedit) or are
only changing a few parameters, for example, you do not need to use
remote visualization.

<span style="font-size:120%;">**Q: What VNC client do I use and where do
I get it?**</span>  
**A:** You can use pretty much any VNC client, it does not matter. A few
examples are [RealVNC](https://www.realvnc.com/),
[TurboVNC](https://sourceforge.net/projects/turbovnc/), and
[TigerVNC](http://tigervnc.org/), all of which can be downloaded from
the appropriately linked pages.

<span style="font-size:120%;">**Q: What does "bind: Address already in
use" mean?**</span>  
**A:** This error refers to port 10000 already being in use. There are
two main causes of this issue.

  - You are trying to SSH to the compute node (the long SSH command to
    the GPU node) from Terra. This is incorrect, you need to SSH to the
    compute node from your computer.
      - **SOLUTION:** open a NEW terminal/tab and do NOT connect to
        Terra. From the NEW terminal/tab try to SSH again.
  - You have recently used a remote visualization session and have not
    fully closed your terminal/MobaXterm window so there is still a
    tunnel between your computer and the compute node on Terra.
      - **SOLUTION:** You will need to COMPLETELY close out your
        terminal/MobaXterm window in order to close the connection.
        After the connection is closed, open a new terminal/MobaXterm
        window and try to SSH again.
