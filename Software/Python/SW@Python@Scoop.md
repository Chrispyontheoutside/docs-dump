# Scoop

Scoop is a way to parallelize python code across multiple nodes without
the need for MPI. This works best for applications that need to do a lot
of independent operations, such as by iterating over a list of items.

## Instructions

These instructions developed for use on the TERRA Cluster:

1.  Ensure that id\_rsa.pub is copied to the authorized\_keys file
      - Your id\_rsa.pub should already exist and live under ~/.ssh
      - Create the authorized\_keys file under ~/.ssh if necessary
      - Try `cat id_rsa.pub >> authorized_keys`
2.  Load your python toolchain (`module load`)
3.  Set up a virtual environment and pip install SCOOP in that
    environment
      - See instructions for virtualenv
        [SW:Python](/kb3/Software/Python/SW@Python/ "wikilink")
4.  Make sure that you have SCOOP version 0.7.1.1 or higher. Previous
    versions do not parse the hostnames correctly
      - If needed, you can download the latest version
        <https://pypi.org/project/scoop/> and replace the scoop folder
        in your virtual environment's site-packages directory with the
        new version
5.  Create a SLURM batch script like the following to launch your
    program. (Replace the example names with your own)
      - The example python program is named Run.py
      - The example python module is named Python/3.7.4-GCCcore-8.3.0
      - The example virtualenv is located at gcc/bin/activate relative
        to the current directory.

<!-- end list -->

    #!/bin/bash
    ##ENVIRONMENT SETTINGS
    
    ##NECESSARY JOB SPECIFICATIONS
    
    ##LOAD YOUR PYTHON MODULE(S) AND ACTIVATE YOUR VIRTUAL ENVIRONMENT
    module load Python/3.7.4-GCCcore-8.3.0
    source gcc/bin/activate
    
    ##CREATE A WRAPPER FOR SSH TO USE TO LOAD YOUR ENVIRONMENT ONTO EACH WORKER NODE
    echo '#!/bin/bash' > scoop_wrapper.sh
    echo module load Python/3.7.4-GCCcore-8.3.0 >> scoop_wrapper.sh
    echo cd $(pwd) >> scoop_wrapper.sh
    echo source gcc/bin/activate >> scoop_wrapper.sh
    echo export SLURM_NTASKS=$SLURM_NTASKS >> scoop_wrapper.sh
    echo python '$@' >> scoop_wrapper.sh
    chmod +x scoop_wrapper.sh
    
    ##EXECUTE YOUR PYTHON SCRIPT
    python -m scoop -n $SLURM_NTASKS -v --python-interpreter=$(pwd)/scoop_wrapper.sh Run.py 

Use sbatch command to run your job
