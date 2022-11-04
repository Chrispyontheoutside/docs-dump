# TensorFlow Benchmarks (HPRC)

In order to compare different installations of TensorFlow on our
clusters (and with other clusters), we conducted a number of benchmarks.

# Overview

The benchmarks came from the git repository at [TensorFlow
Benchmarks](https://github.com/tensorflow/benchmarks) downloaded
February 8, 2018.

All runs were done in a single batch job on a single node on the
cluster. All runs used every CPU available on the node that was
allocated. All GPU runs used 2 GPUs (NVIDIA Tesla K20s on ada and NVIDIA
Tesla K80s on terra).

For Anaconda's Tensorflow, we used Anaconda3/5.1.0 with either
tensorflow/1.5.0 (CPU only) or tensorflow-gpu/1.4.1 (GPU). For locally
built versions, we used TensorFlow/1.5.0-foss-2017b-Python-3.6.3 (CPU
only) and TensorFlow/1.5.0-goolfc-2017b-Python-3.6.3 (GPU) \[Note: we do
not yet have a version built with Intel compilers. Nor have we managed
to build these on ada or curie yet\]

For non-GPU (CPU only) runs, we used:

    python tf_cnn_benchmarks.py --batch_size=32 --model=$model --variable_update=parameter_server --device=cpu --data_format=NHWC

For GPU runs, we used:

    python tf_cnn_benchmarks.py --batch_size=32 --model=$model --variable_update=parameter_server --num_gpus=2

# Summary

Unsurprising result \#1... the CUDA/GPU versions ran faster than the
non-CUDA versions .

In the end, we found, unsurprisingly, that in most cases, the
locally-built non-GPU version outperformed the Anaconda version by a
factor of three (x3) or more. This is due to taking advantage of CPU
extensions available for the cluster it was built on such as AVX.

Similarly unsurprisingly we found that the CUDA versions showed little
difference in performance. Since both use the same CUDA code the
difference on the CPU performance was not as significant an impact.

It should be noted we haven't entirely explored the CPU/GPU interaction
and how it could be utilized but given the results it would seem that if
CPU/GPU (hybrid) use is desired then the locally built version might
have better performance.

Regardless, for now, you should probably stick with the GPU versions.
The queues might be longer but the SUs saved and the turnaround once it
starts might outweigh the time needed to wait for a GPU.

# Results

## Terra

A complete description of Terra can be found in the [ Terra user's
guide](/kb3/User-Guides/Terra/Terra/ "wikilink").

| model         | CPUx28         | GPUx2         |
| ------------- | -------------- | ------------- |
| images/second | time (seconds) | images/second |
| local         | Anaconda       | local         |
| alexnet       | 18.87          | 5.94          |
| vgg11         | 2.58           | 0.71          |
| vgg16         | 1.33           | 0.36          |
| resnet50      | 3.33           | 0.58          |
| vgg19         | 1.05           | 0.29          |
| inception3    | 3.27           | 0.68          |
| resnet101     | 1.93           | 0.34          |
| resnet152     | 1.33           | 0.23          |
|               |                |               |


## HPE DL385 Gen 10

256GB memory, AMD EPYC 7451 24-Core Processor, one Advanced Micro
Devices, Inc. \[AMD/ATI\] Vega 10 \[Radeon Instinct MI25\] (rev 01) GPU
with 16GB memory

Tensorflow was run in a docker container as a natively installed app,
not using Anaconda.

| model         | CPUx24         | GPUx1 (MI25)  |
| ------------- | -------------- | ------------- |
| images/second | time (seconds) | images/second |
| local         | Anaconda       | local         |
| alexnet       | 10.20          | \-            |
| vgg11         | 1.25           | \-            |
| vgg16         | 0.62           | \-            |
| resnet50      | 0.97           | \-            |
| vgg19         | 0.50           | \-            |
| inception3    | 1.15           | \-            |
| resnet101     | 0.58           | \-            |
| resnet152     | 0.39           | \-            |
|               |                |               |

# Scripts

## Common run script

Referred to as **bmtf.sh** in the below job scripts.

    #!/bin/bash
    
    WITH_GPU=0
    if [ "$1" == "--with-gpu" ] ; then
      WITH_GPU=1
    fi
    
    RUN_SOURCE=1
    RUN_ANACONDA=1
    
    for model in alexnet vgg11 vgg16 resnet50 vgg19 inception3 resnet101 resnet152; do
      # Parameters to pass to the benchmark
      if [ 0 -ne $WITH_GPU ] ; then
        TFPARMS="--batch_size=32 --model=$model --variable_update=parameter_server --num_gpus=2"  # from the documentation
      else
        TFPARMS="--batch_size=32 --model=$model --variable_update=parameter_server --device=cpu --data_format=NHWC" # need last two for non-GPU
      fi
      echo -e "\n### `date` - Running on `hostname` with parameters: python tf_cnn_benchmarks.py $TFPARMS\n"
    
      # built from scratch
      if [ 0 -ne $RUN_SOURCE ] ; then
        echo -e "\n### Running locally built version of TensorFlow\n"
        ml purge
        if [ 0 -ne $WITH_GPU ] ; then
          ml TensorFlow/1.5.0-goolfc-2017b-Python-3.6.3
        else
          ml TensorFlow/1.5.0-foss-2017b-Python-3.6.3 # not available on ada yet
        fi
        ml
        which python
        /usr/bin/time -av python /scratch/group/hprc/TensorFlowBM/tensorflow_benchmarks-20180208/scripts/tf_cnn_benchmarks/tf_cnn_benchmarks.py $TFPARMS
      fi
      
      # installed by conda
      if [ 0 -ne $RUN_ANACONDA ] ; then
        echo -e "\n### Running Anaconda version of TensorFlow\n"
        ml purge
        ml Anaconda3/5.1.0
        if [ 0 -ne $WITH_GPU ] ; then
          source activate $SCRATCH/myAnaconda3/5.1.0-tensorflow-gpu
        else
          source activate $SCRATCH/myAnaconda3/5.1.0-tensorflow
        fi
        conda list
        which python
        /usr/bin/time -av python /scratch/group/hprc/TensorFlowBM/tensorflow_benchmarks-20180208/scripts/tf_cnn_benchmarks/tf_cnn_benchmarks.py $TFPARMS
        source deactivate
      fi
    done
    # EOF

## Batch job scripts

### Terra

#### GPU

    #!/bin/bash
    ## ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE             # Do not propagate environment
    #SBATCH --get-user-env=L          # Replicate login environment
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=bmtf-gpu
    #SBATCH --time=24:00:00
    #SBATCH --nodes=1                 # Request 1 node
    #SBATCH --ntasks-per-node=28      # Request all avail cores on node
    #SBATCH --mem=56G                 # Request all avail memory on node 
    #SBATCH --output=out.bmtf-gpu.%j
    #SBATCH --partition=staff         # Priority testing queue
    ## OPTIONAL JOB SPECIFICATIONS
    #JKPBATCH --account=123456        # Set billing account to 123456
    #JKPBATCH --mail-type=ALL         # Send email on all job events
    #JKPBATCH --mail-user=j-perdue@tamu.edu # Where to send email
    ## GPUS
    #SBATCH --gres=gpu:2
    
    echo -e "\n# Job submitted from $SLURM_SUBMIT_HOST:$SLURM_SUBMIT_DIR\n"
    echo "#################### Start: Job Script `basename $0` ###########################"
    cat $0
    cat bmtf.sh
    echo "#################### End Job Script `basename $0` ###########################"
    
    ./bmtf.sh --with-gpu
    
    echo "### Ending Job"
    # EOF

#### CPU-only

    #!/bin/bash
    ## ENVIRONMENT SETTINGS; CHANGE WITH CAUTION
    #SBATCH --export=NONE             # Do not propagate environment
    #SBATCH --get-user-env=L          # Replicate login environment
    ## NECESSARY JOB SPECIFICATIONS
    #SBATCH --job-name=bmtf
    #SBATCH --time=24:00:00
    #SBATCH --nodes=1                 # Request 1 node
    #SBATCH --ntasks-per-node=28      # Request all avail cores on node
    #SBATCH --mem=56G                 # Request all avail memory on node 
    #SBATCH --output=out.bmtf.%j
    #SBATCH --partition=staff         # Priority testing queue
    ## OPTIONAL JOB SPECIFICATIONS
    #JKPBATCH --account=123456        # Set billing account to 123456
    #JKPBATCH --mail-type=ALL         # Send email on all job events
    #JKPBATCH --mail-user=j-perdue@tamu.edu # Where to send email
    ## GPUS
    #SBATCH --gres=gpu:0
    
    echo -e "\n# Job submitted from $SLURM_SUBMIT_HOST:$SLURM_SUBMIT_DIR\n"
    echo "#################### Start: Job Script `basename $0` ###########################"
    cat $0
    cat bmtf.sh
    echo "#################### End Job Script `basename $0` ###########################"
    ./bmtf.sh
    echo "### Ending Job"
    # EOF

### Ada

#### GPU

    #!/bin/bash
    #BSUB -L /bin/bash
    #BSUB -J bmtf-gpu
    #BSUB -W 24:00 
    #BSUB -R 'span[ptile=20]'
    #BSUB -n 20
    #BSUB -R "rusage[mem=2500]"
    #BSUB -M 2500
    #BSUB -o out.bmtf-gpu.%J 
    #BSUB -q staff
    #BSUB -R 'select[gpu]'
    
    echo -e "\n# Job submitted from $LSB_SUBCWD (`pwd`) using $LSB_MCPU_HOSTS\n"
    echo "#################### Start: Job Script `basename $0` ($LSB_JOBNAME) ###########################"
    cat $0
    cat bmtf.sh
    echo "#################### End Job Script `basename $0` ($LSB_JOBnAME) ###########################"
    
    ./bmtf.sh --with-gpu
    
    echo "### Ending Job"
    # EOF

#### CPU-only

    #!/bin/bash
    #BSUB -L /bin/bash
    #BSUB -J bmtf
    #BSUB -W 24:00 
    #BSUB -R 'span[ptile=20]'
    #BSUB -n 20
    #BSUB -R "rusage[mem=2500]"
    #BSUB -M 2500
    #BSUB -o out.bmtf.%J 
    #BSUB -q staff
    #DISABLEBSUB -R 'select[gpu]'
    
    echo -e "\n# Job submitted from $LSB_SUBCWD (`pwd`) using $LSB_MCPU_HOSTS\n"
    echo "#################### Start: Job Script `basename $0` ($LSB_JOBNAME) ###########################"
    cat $0
    cat bmtf.sh
    echo "#################### End Job Script `basename $0` ($LSB_JOBnAME) ###########################"
    
    ./bmtf.sh
    
    echo "### Ending Job"
    # EOF
