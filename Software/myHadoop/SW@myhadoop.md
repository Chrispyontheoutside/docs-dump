# myhadoop

This page describe how to run Hadoop on Ada via
[myHadoop](https://github.com/glennklockwood/myhadoop). You will prepare
a job file with hadoop commands and then submit this job file like
regular HPC jobs.

### Example: Word Counting

Load the myhadoop module and copy the example job file

    module load myHadoop
    cp $MYHADOOP_HOME/examples/lsf.qsub .

Here is content of lsf.qsub.

    #!/bin/bash
    ################################################################################
    #  lsf - A sample submit script for LSF that illustrates how to
    #    spin up a Hadoop cluster for a map/reduce task using myHadoop
    #
    #  Based on pbs.qsub by Glenn K. Lockwood, San Diego Supercomputer Center, Feb 2014
    #
    #  T. Mark Huang, High Performance Research Computing, Texas A & M University  April 2016
    ################################################################################
    #BSUB -J myHadoop               # Job name (modify as needed)
    #BSUB -L /bin/bash              # login shell
    #BSUB -W 0:15                   # wall-clock limit (modify as needed)
    #BSUB -n 60                     # total number of processor cores (modify as needed)
    #BSUB -R "span[ptile=20]"       # number of processs cores per node (modify as needed)
    #BSUB -o myHadoop.output.%J     # stdout (modify as needed)
    
    # set up warning action for clean up
    #BSUB -wa INT                   # set warning action (SIGINT)
    #BSUB -wt 5                     # warning time limit (5 min before end of walltime)
    
    ## load modules
    module load myHadoop
    
    # set trap for cleaning up processes and files before gotten killed
    trap "{ echo 'Job got SIGINT'; date; $HADOOP_HOME/sbin/stop-all.sh; date; myhadoop-cleanup.sh; date; }" SIGINT
    trap "{ echo 'Job got SIGTERM'; date; $HADOOP_HOME/sbin/stop-all.sh; date; myhadoop-cleanup.sh; date; }" SIGTERM
    trap "{ echo 'Job got SIGKILL'; date; $HADOOP_HOME/sbin/stop-all.sh; date; myhadoop-cleanup.sh; date; }" SIGKILL
    
    ## set local hadoop config dir
    export HADOOP_CONF_DIR=$LS_SUBCWD/hadoop-conf.$LSB_JOBID
    
    ## update TMPDIR
    export TMPDIR=/work/$LSB_JOBID.tmpdir
    
    ## uncomment these lines to supress Hadoop log output
    #export HADOOP_ROOT_LOGGER=INFO,RFA
    #export HADOOP_MAPRED_ROOT_LOGGER=INFO,RFA
    #export YARN_ROOT_LOGGER=INFO,RFA
    #export ZOO_LOG4J_PROP=INFO,ROLLINGFILE
    #export HBASE_ROOT_LOGGER=INFO,RFA
    
    ## set local scratch with "-s";
    ##      /work is local to compute node;
    ##      /work/$LSB_JOBID.tmpdir will be removed after compute job terminates
    myhadoop-configure.sh -s $TMPDIR
    
    ## start Hadoop
    $HADOOP_HOME/sbin/start-all.sh
    
    ## create input data directory
    $HADOOP_HOME/bin/hadoop dfs -mkdir /data
    
    
    ## ========== Beginning of custom code; modify as needed ==========
    
    ## copy/download intput file (remove or comment out this section if you don't need to use sample data)
    if [ ! -f ./pg2701.txt ]; then
      if [ -f $MYHADOOP_HOME/examples/pg2701.txt ]; then
        cp $MYHADOOP_HOME/examples/pg2701.txt .
      else
        echo "*** Retrieving some sample input data"
        wget 'http://www.gutenberg.org/cache/epub/2701/pg2701.txt'
      fi
    fi
    
    ## copy input to data directory
    $HADOOP_HOME/bin/hadoop dfs -put ./pg2701.txt /data/
    ## list data directory
    $HADOOP_HOME/bin/hadoop dfs -ls /data
    
    ## run map reduce example
    $HADOOP_HOME/bin/hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar wordcount /data /wordcount-output
    
    ## list output directory
    $HADOOP_HOME/bin/hadoop dfs -ls /wordcount-output
    ## copy ouput directory back to local
    $HADOOP_HOME/bin/hadoop dfs -get /wordcount-output ./
    
    ## ========== End of custom code ==========
    
    
    ## stop Hadoop
    $HADOOP_HOME/sbin/stop-all.sh
    
    ## clean up myHadoop and copy logs to local config dir
    myhadoop-cleanup.sh

Modify processor, memory and walltime requirement. The example uses 60
cores (3 nodes, each with 20 cores per node), default 2.5 GB memory per
core (set implicitly), and wall clock time of 15 minutes. See
[Terra:Batch](/kb3/User-Guides/Terra/Terra@Batch/ "wikilink") for more details.

Then submit sample job file by

    bsub < lsf.qsub

The input file is "pg2701.txt". The result will be in the directory
"wordcount-output". The Hadoop config and log files are in
"hadoop-conf.<jobid>".

### Options for myhadoop-configure.sh

    $ myhadoop-configure.sh
    No resource manager detected.  Aborting.
    Usage: myhadoop-configure.sh [options]
        -n <num> 
            specify number of nodes to use.  (default: all nodes from resource 
            manager)
    
        -p <dir> 
            use persistent HDFS and store namenode and datanode state on the shared 
            filesystem given by <dir> (default: n/a)
    
        -c <dir>
            build the resulting Hadoop config directory in <dr> (default: from 
            user environment's HADOOP_CONF_DIR or myhadoop.conf)
    
        -s <dir>
            location of node-local scratch directory where datanode and tasktracker
            will be stored.  (default: user environment's MH_SCRATCH_DIR or 
            myhadoop.conf)
    
        -h <dir>
            location of Hadoop installation containing the myHadoop configuration
            templates in <dir>/conf and the 'hadoop' executable in <dir>/bin/hadoop
            (default: user environment's HADOOP_HOME or myhadoop.conf)
    
        -i <regular expression>
            transformation (passed to sed -e) to turn each hostname provided by the
            resource manager into an IP over InfiniBand host.  (default: "")
    
        -?
            show this help message

Example above sets local scratch "-s /work/$LSB\_JOBID.tmpdir", which is
resided on local disk of the compute node. You can set up persistent
directory with "-p /scratch/user/$USERID/myHadoop\_persistent\_dir",
which is on GPFS storage accessible from all compute nodes.

### References

  - myHadoop GitHub page: <https://github.com/glennklockwood/myhadoop>
