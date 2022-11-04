# Moose

Multiphysics Object-Oriented Simulation Environment - An open-source,
parallel finite element framework

## Building the MOOSE framework in your $SCRATCH

    cd $SCRATCH # where to install
    module purge # clear module environment
    module load MOOSE/moose-dev-gcc-ompi # load the MOOSE development module
    time $EBROOTMOOSE/install-moose.sh build # get/build/test MOOSE

This will download and build the MOOSE framework in $SCRATCH/moose. It
runs a script called update\_and\_rebuild\_libmesh.sh that takes the
majority of the time. After that, it will switch to the
$SCRATCH/moose/test directory and run 'make' and 'run\_tests' to finish
the build.

## Testing your MOOSE framework

At this point, to do further testing of your installation you can build
all the exercises with:

    ml purge
    ml MOOSE/moose-dev-gcc-ompi # make sure module is loaded
    cd $SCRATCH/moose/examples
    make -j 8 # build

For descriptions, and instructions on how to run the examples, see the
[MOOSE Examples](https://mooseframework.org/examples/index.html) page.

Do do some very extensive, and lengthy, testing, you can build all the
MOOSE modules and run their tests.

    ml purge
    ml MOOSE/moose-dev-gcc-ompi # make sure module is loaded
    cd $SCRATCH/moose/modules
    make -j 8 # build
    ./run_tests -j 8 # run

## Using your MOOSE framework

(This needs more work... see the MOOSE web page for more details after
the framework is installed)

### latest notes

See Create an Application and Compile and Test Your Application at the
[MOOSE Getting Started
page](https://mooseframework.inl.gov/getting_started/index.html).
Replace all instances of **~/projects** with **$SCRATCH**

### old notes

(you should probably try the above first)

Now you can build your model with the moose framework. Do as follows.

    ml MOOSE/moose-dev-gcc-ompi # make sure module is loaded
    cp -rp /path/to/my_module $SCRATCH/moose/modules # copy your module to framework
    cd $SCRATCH/moose/modules/my_module
    # MIGHT NEED A STEP HERE TO USE MOOSE TO CREATE A Makefile
    make

## Sample job scripts on Terra

Sample 1

    #!/bin/bash
    #SBATCH -J moose-sample1       #Set the job name to "moose-sample1"
    #SBATCH -t 1:00:00             #Set the wall clock limit to 1hr 
    #SBATCH -N 20                  #Request 20 node
    #SBATCH --ntasks-per-node=28   #Request 28 tasks per node
    #SBATCH --mem=56G              #Request 56G per node
    #SBATCH -o moose-sample1.%j    #Send stdout/err to "Example1Out.[jobID]"
    
    module load MOOSE/moose-dev-gcc-ompi
    mpirun /path/to/moose-opt -i moose.i

Sample 2 Use half of the cores per node such that each core can have
2G\*2=4G memory to use. This is useful for models that need large amount
of memory.

    #!/bin/bash
    #SBATCH -J  moose-sample2      #Set the job name to "moose-sample2"
    #SBATCH -t 1:00:00             #Set the wall clock limit to 1hr 
    #SBATCH -N 20                  #Request 20 node
    #SBATCH --ntasks-per-node=28   #Request 28 tasks per node
    #SBATCH --mem=56G              #Request 56G per node
    #SBATCH -o moose-sample2.%j    #Send stdout/err to "moose-sample2.[jobID]"
    
    module load MOOSE/moose-dev-gcc-ompi
    mpirun -np 280 -npernode 14 /path/to/moose-opt -i moose.i

## Sample job script on Ada

Sample 1

    #BSUB -J moose-sample1
    #BSUB -o moose-sample1.%J
    #BSUB -e error.%J
    #BSUB -L /bin/bash
    #BSUB -W 20:00
    #BSUB -n 400
    #BSUB -M 2700
    #BSUB -R "span[ptile=20]"
    #BSUB -R "rusage[mem=2700]"
    
    module load MOOSE/moose-dev-gcc-ompi
    mpirun /path/to/moose-opt -i moose.i

Sample 2: Use half of the cores per node such that each core can have
2700x2=5400M memory to use. This is useful for models that need large
amount of memory.

    #BSUB -J moose-sample2
    #BSUB -o moose-sample2.%J
    #BSUB -e error.%J
    #BSUB -L /bin/bash
    #BSUB -W 20:00
    #BSUB -n 400
    #BSUB -M 2700
    #BSUB -R "span[ptile=20]"
    #BSUB -R "rusage[mem=2700]"
    
    module load MOOSE/moose-dev-gcc-ompi
    mpirun -np 200 -npernode 10 /path/to/moose-opt -i moose.i
