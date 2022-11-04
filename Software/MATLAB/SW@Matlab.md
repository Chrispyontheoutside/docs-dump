# Running Matlab interactively

Matlab is accessible to all HPRC users within the terms of our license
agreement. If you have particular concerns about whether specific usage
falls within the TAMU HPRC license, please send an email to HPRC
Helpdesk. You can start a Matlab session either directly on a login node
or through our portal

## Running Matlab on a login node

To be able to use Matlab, the Matlab module needs to be loaded first.
This can be done using the following command:

`[ netID@cluster ~]$ `**`module   load   Matlab/R2020b`**

This will setup the environment for Matlab version R2020b. To see a list
of all installed versions, use the following command:

`[ netID@cluster ~]$ `**`module   spider   Matlab`**

<font color=teal>**Note:** New versions of software become available
periodically. Version numbers may change.</font>

To start matlab, use the following command:

`[ netID@cluster ~]$ `**`matlab`**

Depending on your X server settings, this will start either the Matlab
GUI or the Matlab command-line interface. To start Matlab in
command-line interface mode, use the following command with the
appropriate flags:

`[ netID@cluster ~]$ `**`matlab   -nosplash   -nodisplay`**

By default, Matlab will execute a large number of built-in operators and
functions multi-threaded and will use as many threads (i.e. cores) as
are available on the node. Since login nodes are shared among all users,
HPRC restricts the number of computational threads to 8. This should
suffice for most cases. Speedup achieved through multi-threading depends
on many factors and in certain cases. To explicitly change the number of
computational threads, use the following Matlab command:

`>>feature('NumThreads',4);`

This will set the number of computational threads to 4.

To completely disable multi-threading, use the -singleCompThread option
when starting Matlab:

`[ netID@cluster ~]$ `**`matlab   -singleCompThread`**

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

## Running Matlab through the hprc portal

HPRC provides a portal through which users can start an interactive
Matlab GUI session inside a web browser. For more information how to use
the portal see our [ HPRC OnDemand Portal](/kb3/Software/Portal/SW@Portal/ "wikilink") section

# Running Matlab through the batch system

HPRC developed a tool named **matlabsubmit** to run Matlab simulations
on the HPRC compute nodes without the need to create your own batch
script and without the need to start a Matlab session. **matlabsubmit**
will automatically generate a batch script with the correct
requirements. In addition, **matlabsubmit** will also generate
boilerplate Matlab code to set up the environment (e.g. the number of
computational threads) and, if needed, will start a *parpool* using the
correct Cluster Profile (*local* if all workers fit on a single node and
a cluster profile when workers are distribued over multiple nodes)

To submit your Matlab script, use the following command:

    [ netID@cluster ~]$ matlabsubmit myscript.m

In the above example, **matlabsubmit** will use all default values for
runtime, memory requirements, the number of workers, etc. To specify
resources, you can use the command-line options of **matlabsubmmit**.
For example:

    [ netID@cluster ~]$ matlabsubmit -t 07:00 -s 4 myscript.m

will set the wall-time to 7 hours and makes sure Matlab will use 4
computational threads for its run ( **matlabsubmit** will also request 4
cores).

To see all options for **matlabsubmit** use the **-h** flag

    [ netID@cluster ~]$ matlabsubmit -h
    Usage: /sw/hprc/sw/Matlab/bin/matlabsubmit [options] SCRIPTNAME
    
    This tool automates the process of running Matlab codes on the compute nodes.
    
    OPTIONS:
      -h Shows this message
      -m set the amount of requested memory in MEGA bytes(e.g. -m 20000)
      -t sets the walltime; form hh:mm (e.g. -t 03:27)
      -w sets the number of ADDITIONAL workers
      -g indicates script needs GPU  (no value needed)
      -b sets the billing account to use 
      -s set number of threads for multithreading (default: 8 ( 1  when -w > 0)
      -p set number of workers per node
      -f run function call instead of script
      -x add explicit batch scheduler option
      
    DEFAULT VALUES:
      memory   : 2000 per core 
      time     : 02:00
      workers  : 0
      gpu      : no gpu 
      threading: on, 8 threads

**NOTE** when using the **-f** flag to execute a function instead of a
script, the function call must be enclosed with double quotes when it
contains parentheses. For example: **matlabsubmit -f "myfunc(21)"**

  
When executing, **matlabsubmit** will do the following:

  - generate boilerplate Matlab code to setup the Matlab environment
    (e.g. \#threads, \#workers)  
  - generate a batch script with all resources set correctly and the
    command to run Matlab  
  - submit the generated batch script to the batch scheduler and return
    control back to the user  

For detailed examples on using matlabsubmit see the [ examples
](/kb3/Software/MATLAB/SW@Matlab_matlabsubmit/ "wikilink") section.

# Using Matlab Parallel Toolbox on HPRC Resources

In this section, we will focus on utilizing the Parallel toolbox on HPRC
cluster. For a general intro to the Parallel Toolbox see the [parallel
toolbox](https://www.mathworks.com/help/parallel-computing/index.html?s_tid=CRUX_lftnav)
section on the Mathworks website. Here we will discuss how to use Matlab
Cluster profiles to distribute workers over multiple nodes.

## Cluster Profiles

Matlab uses the concept of *Cluster Profiles* to create parallel pools.
When Matlab creates a parallel pool, it uses the cluster profile to
determine how many workers to use, how many threads every worker can
use, where to store meta-data, as well as some other meta-data. There
are two kinds of profiles.

  - local profiles: parallel processing is limited to the same node the
    Matlab client is running.
  - cluster profiles: parallel processing can span multiple nodes;
    profile interacts with a batch scheduler (e.g. SLURM on terra).

**NOTE:** we will not discuss *local profiles* any further here.
Processing using a local profile is exactly the same as processing using
cluster profiles.

TAMU HPRC provides a framework, to easily manage and update cluster
profiles. The central concept in most of the discussion below is the
**TAMUClusterProperties** object. The TAMUClusterProperties object keeps
track of all the properties needed to successfully create a parallel
pool. That includes typical Matlab properties, such as the number of
Matlab workers requested as well as batch scheduler properties such as
wall-time and memory. **TAMUClusterProperties**.

### Importing Cluster Profile

For your convenience, HPRC already created a custom Cluster Profile.
Using the profile, you can define how many workers you want, how you
want to distribute the workers over the nodes, how many computational
threads to use, how long to run, etc. Before you can use this profile
you need to import it first. This can be done using by calling the
following Matlab function.

    >>tamuprofile.importProfile()

This function imports the cluster profile and it creates a directory
structure in your scratch directory where Matlab will store
meta-information during parallel processing. The default location is
*/scratch/$USER/MatlabJobs/TAMU\<VERSION*, where <VERSION> represents
the Matlab version. For example, for Matlab R2020b, it will be
*/scratch/$USER/MatlabJobs/TAMU2020b*

### Getting the Cluster Profile Object

To get a **TAMUClusterProperties** object you can do the following:

    >> tp=TAMUClusterProperties;

**tp** is an object of type **TAMUClusterProperties** with default
values for all the properties. To see all the properties, you can just
print the value of **tp**. You can easily change the values using the
convenience methods of **TAMUClusterProperties**

For example, suppose you have Matlab code and want to use 4 workers for
parallel processing.

    >> tp=TAMUClusterProperties;
    >> tp.workers(4);

## Creating a Parallel Pool

To start a parallel pool you can use the HPRC convenience function
**tamuprofile.parpool**. It takes as argument a
**TAMUClustrerProperties** object that specifies all the resources that
are requested.

For example:

    mypool = tamuprofile.parpool(tp)
        :
    delete(mypool)

This code starts a worker pool using the default cluster profile, with 4
additional workers.

NOTE: only instructions within parfor and spmd blocks are executed on
the workers. All other instructions are executed on the client.

NOTE: all variables declared inside the parpool block will be destroyed
once the block is finished.

#### Alternative approach to create parallel pool

Matlab already provides functions to create parallel pools, namely:
*parcluster(<string clustername>)* and *parpool(<parcluster object>)*.
You can use these functions as well, but it will be a more complicated
to set all the properties correct ( we will not discuss how to do that
here). To create a parallel pool using the basic Matlab functions, you
can do the following:

    cp = parcluster('TAMU2020b')
    % add code to set the number of workers manually. There is no uniform way to do this and might depend on the type of cluster profile and the batch scheduler (e.g. Slurm)
    mypool = parpool(cp);
       ;
    delete(mypool)

For convenience, TAMU HPRC also provides a convenience function to
return a fully populated *parcluster* object that can be passed into a
Matlab *parpool* function. See below for an example that creates a pool
with 4 workers:

    tp = TAMUClusterProperties();
    tp.workers(4);
    cp = tamuprofile.parcluster();
    mypool = parpool(cp)
       :
    delete(mypool)
