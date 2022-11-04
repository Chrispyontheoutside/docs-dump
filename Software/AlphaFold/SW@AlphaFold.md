# AlphaFold

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [grace
(monomer 2.1.2)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_alphafold_2.1.2_a100_monomer_ptm_grace.sh)

## Description

AlphaFold is an AI system that predicts a protein’s 3D structure from
its amino acid sequence.

AlphaFold [homepage](https://github.com/deepmind/alphafold)

AlphaFold is available on Grace as a singularity container based on
[catgumag/alphafold](https://hub.docker.com/r/catgumag/alphafold)

/sw/hprc/sw/bio/containers/alphafold/alphafold_2.2.0.sif

The AlphaFold databases are found in the following directory (for
versions 2.2.0+)

 /scratch/data/bio/alphafold/

Run alphafold using the following command while using the VNC portal app
or from within your job script. Tested on A100 GPU.

Be sure to select a GPU when launching the VNC app.

 singularity exec /sw/hprc/sw/bio/containers/alphafold/alphafold_2.2.0.sif python /app/alphafold/run_alphafold.py --helpfull

See the Biocontainers [wiki
page](/kb3/Software/Bioinformatics/Bioinformatics@Biocontainers/) for
additional details on how to use .sif image files.

  - notice that version 2.1.2 now requires the option --use\_gpu\_relax

## Example Job Scripts

Example IL2Y amino acid sequence for a 30 minute prediction:

NLYIQWLKDGGPSSGRPPPS

### Monomer

    #!/bin/bash  
    #SBATCH --job-name=alphafold        # job name  
    #SBATCH --time=2-00:00:00           # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24          # CPUs (threads) per command  
    #SBATCH --mem=180G                  # total memory per node  
    #SBATCH --gres=gpu:a100:1           # request 1 A100 GPU  
    #SBATCH --output=stdout.%x.%j       # save stdout to file  
    #SBATCH --error=stderr.%x.%j        # save stderr to file  
      
    module purge  
      
    export SINGULARITYENV_TF_FORCE_UNIFIED_MEMORY=1  
    export SINGULARITYENV_XLA_PYTHON_CLIENT_MEM_FRACTION=4.0  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.2  
  
    # run gpustats in the background (&) to monitor gpu usage in order to create a graph later  
    gpustats &  
      
    singularity exec **--nv** /sw/hprc/sw/bio/containers/alphafold_2.1.2.sif python /app/alphafold/run_alphafold.py  \  
     **--use_gpu_relax** \  
     --data_dir=$DOWNLOAD_DIR  \  
     --uniref90_database_path=$DOWNLOAD_DIR/uniref90/uniref90.fasta  \  
     --mgnify_database_path=$DOWNLOAD_DIR/mgnify/mgy_clusters_2018_12.fa  \  
     --bfd_database_path=$DOWNLOAD_DIR/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt  \  
     --uniclust30_database_path=$DOWNLOAD_DIR/uniclust30/uniclust30_2021_03/UniRef30_2021_03 \  
     --pdb70_database_path=$DOWNLOAD_DIR/pdb70/pdb70  \  
     --template_mmcif_dir=$DOWNLOAD_DIR/pdb_mmcif/mmcif_files  \  
     --obsolete_pdbs_path=$DOWNLOAD_DIR/pdb_mmcif/obsolete.dat \  
     --model_preset=**monomer** \  
     --max_template_date=2022-1-1 \  
     --db_preset=full_dbs \  
     --output_dir=out_alphafold \  
     --fasta_paths=**/scratch/data/bio/alphafold/example_data/T1050.fasta**  
      
    # run gpustats to create a graph of gpu usage for this job  
    gpustats

### Multimer

    #!/bin/bash  
    #SBATCH --job-name=alphafold        # job name  
    #SBATCH --time=2-00:00:00           # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24          # CPUs (threads) per command  
    #SBATCH --mem=180G                  # total memory per node  
    #SBATCH --gres=gpu:a100:1           # request 1 A100 GPU  
    #SBATCH --output=stdout.%x.%j       # save stdout to file  
    #SBATCH --error=stderr.%x.%j        # save stderr to file  
      
    module purge  
      
    export SINGULARITYENV_TF_FORCE_UNIFIED_MEMORY=1  
    export SINGULARITYENV_XLA_PYTHON_CLIENT_MEM_FRACTION=4.0  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.2  
      
    # run gpustats in the background (&) to monitor gpu usage in order to create a graph later  
    gpustats &  
      
    singularity exec **--nv** /sw/hprc/sw/bio/containers/alphafold_2.1.2.sif python /app/alphafold/run_alphafold.py  \  
     **--use_gpu_relax** \  
     --data_dir=$DOWNLOAD_DIR  \  
     --uniref90_database_path=$DOWNLOAD_DIR/uniref90/uniref90.fasta  \  
     --mgnify_database_path=$DOWNLOAD_DIR/mgnify/mgy_clusters_2018_12.fa  \  
     --bfd_database_path=$DOWNLOAD_DIR/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt  \  
     --uniclust30_database_path=$DOWNLOAD_DIR/uniclust30/uniclust30_2021_03/UniRef30_2021_03 \  
     **--pdb_seqres_database_path=**$DOWNLOAD_DIR/pdb_seqres/pdb_seqres.txt  \  
     --template_mmcif_dir=$DOWNLOAD_DIR/pdb_mmcif/mmcif_files  \  
     --obsolete_pdbs_path=$DOWNLOAD_DIR/pdb_mmcif/obsolete.dat \  
     --uniprot_database_path=$DOWNLOAD_DIR/uniprot/uniprot.fasta \  
     --model_preset=**multimer** \  
     --max_template_date=2022-1-1 \  
     --db_preset=full_dbs \  
     --output_dir=out_alphafold \  
     --fasta_paths=**/scratch/data/bio/alphafold/example_data/T1083_T1084_multimer.fasta**  
      
    # run gpustats to create a graph of gpu usage for this job  
    gpustats

### Multiple Monomers

If you have multiple protein sequences from the same organism, running
multiple monomers in one job script will significantly speed up
processing.

The following job script uses the AlphaFold/2.1.1 module instead of the
singularity image.

The AlphaFold/2.1.1 module is usually one version behind the singularity
image.

    #!/bin/bash  
    #SBATCH --job-name=alphafold_multi-monomer  # job name  
    #SBATCH --time=2-00:00:00                   # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1                 # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24                  # CPUs (threads) per command  
    #SBATCH --mem=180G                          # total memory per node  
    #SBATCH --gres=gpu:a100:1                   # request one a100 GPU  
    #SBATCH --output=stdout.%x.%j               # save stdout to file  
    #SBATCH --error=stderr.%x.%j                # save stderr to file  
      
    module purge  
    module load GCC/10.2.0  CUDA/11.1.1  OpenMPI/4.0.5  AlphaFold/2.1.1  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.1  
      
    # start a process to monitor GPU usage  
    gpustats &  
      
    run_alphafold.py  \  
    --data_dir=$DOWNLOAD_DIR  \  
    --uniref90_database_path=$DOWNLOAD_DIR/uniref90/uniref90.fasta  \  
    --mgnify_database_path=$DOWNLOAD_DIR/mgnify/mgy_clusters_2018_12.fa  \  
    --bfd_database_path=$DOWNLOAD_DIR/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt  \  
    --uniclust30_database_path=$DOWNLOAD_DIR/uniclust30/uniclust30_2021_03/UniRef30_2021_03 \  
    --pdb70_database_path=$DOWNLOAD_DIR/pdb70/pdb70  \  
    --template_mmcif_dir=$DOWNLOAD_DIR/pdb_mmcif/mmcif_files  \  
    --obsolete_pdbs_path=$DOWNLOAD_DIR/pdb_mmcif/obsolete.dat \  
    --model_preset=monomer \  
    --max_template_date=2022-1-1 \  
    --db_preset=full_dbs \  
    --output_dir=out_alphafold_2.1.1_multi-monomer \  
    --fasta_paths=T1083.fasta,T1084.fasta  
      
    # create a graph of GPU resource usage stats  
    gpustats

  - **The only parameter you need to change in the example job script is
    the path to your fasta file: --fasta\_paths=**

<!-- end list -->

  - **You can also change these: --max\_template\_date and
    --output\_dir**

<!-- end list -->

  - **Use the lines that have $DOWNLOAD\_DIR exactly as they are and do
    not change these.**

***The run\_alphafold.py command initially starts running on CPU but
later only runs on a single GPU so specify one GPU in the \#SBATCH
--gres parameter and half of the system memory and cores so someone else
can use the the other GPU.***

***The example\_data/T1050.fasta takes 16 hours on CPU.***

 
    GPU         Runtime
    A100       4 hr  9 min
    RTX 6000   3 hr 58 min
    T4         5 hr 12 min

    all GPUs used about 62GB of system memory


JAX memory allocation is explained
[here](https://jax.readthedocs.io/en/latest/gpu_memory_allocation.html)

***Note: if you do not use the --nv option, AlphaFold will run on CPU
only***

## Visualize Results

[AlphaPickle](https://github.com/mattarnoldbio/alphapickle) can be used
to create graphs for visualizing each of the model .pkl files.

    #!/bin/bash  
    #SBATCH --job-name=alphafold        # job name  
    #SBATCH --time=2-00:00:00           # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1         # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24          # CPUs (threads) per command  
    #SBATCH --mem=180G                  # total memory per node  
    #SBATCH --gres=gpu:a100:1           # request 1 A100 GPU  
    #SBATCH --output=stdout.%x.%j       # save stdout to file  
    #SBATCH --error=stderr.%x.%j        # save stderr to file  
      
    module purge  
    **module   load   GCC/10.2.0   CUDA/11.1.1 
    OpenMPI/4.0.5   AlphaPickle/1.4.1**  
      
    export SINGULARITYENV_TF_FORCE_UNIFIED_MEMORY=1  
    export SINGULARITYENV_XLA_PYTHON_CLIENT_MEM_FRACTION=4.0  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.2  
      
    # run gpustats in the background (&) to monitor gpu usage in order to create a graph later  
    gpustats &  
      
    singularity exec --nv /sw/hprc/sw/bio/containers/alphafold_2.1.2.sif python /app/alphafold/run_alphafold.py  \  
     **--use_gpu_relax** \  
     --data_dir=$DOWNLOAD_DIR  \  
     --uniref90_database_path=$DOWNLOAD_DIR/uniref90/uniref90.fasta  \  
     --mgnify_database_path=$DOWNLOAD_DIR/mgnify/mgy_clusters_2018_12.fa  \  
     --bfd_database_path=$DOWNLOAD_DIR/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt  \  
     --uniclust30_database_path=$DOWNLOAD_DIR/uniclust30/uniclust30_2021_03/UniRef30_2021_03 \  
     --pdb70_database_path=$DOWNLOAD_DIR/pdb70/pdb70  \  
     --template_mmcif_dir=$DOWNLOAD_DIR/pdb_mmcif/mmcif_files  \  
     --obsolete_pdbs_path=$DOWNLOAD_DIR/pdb_mmcif/obsolete.dat \  
     --model_preset=monomer \  
     --max_template_date=2022-1-1 \  
     --db_preset=full_dbs \  
     --output_dir=**out_alphafold** \  
     --fasta_paths=/scratch/data/bio/alphafold/example_data/**T1050**.fasta  
      
    # run gpustats to create a graph of gpu usage for this job  
    gpustats  
      
    # run AlphaPickle to create a graph for each model .pkl file.  
    # Name the -od directory based on how you named --output_dir and --fasta_paths in the run_alphafold.py command  
    **run_AlphaPickle.py   -od   out_alphafold/T1050**

## Database directory

The AlphaFold database directory is structured as follows:

    /scratch/data/bio/alphafold/2.2.0
    ├── [4.0K]  bfd
    │   ├── [1.4T]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_a3m.ffdata
    │   ├── [1.7G]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_a3m.ffindex
    │   ├── [ 16G]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_cs219.ffdata
    │   ├── [1.6G]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_cs219.ffindex
    │   ├── [304G]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_hhm.ffdata
    │   └── [124M]  bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt_hhm.ffindex
    ├── [4.0K]  example_data
    │   ├── [ 828]  T1050.fasta
    │   ├── [ 106]  T1083.fasta
    │   └── [ 187]  test_multimer.fasta
    ├── [4.0K]  mgnify
    │   ├── [ 64G]  mgy_clusters_2018_12.fa
    │   └── [  23]  mgy_clusters.fa -> mgy_clusters_2018_12.fa
    ├── [4.0K]  params
    │   ├── [ 20K]  LICENSE
    │   ├── [356M]  params_model_1_multimer.npz
    │   ├── [356M]  params_model_1.npz
    │   ├── [356M]  params_model_1_ptm.npz
    │   ├── [356M]  params_model_2_multimer.npz
    │   ├── [356M]  params_model_2.npz
    │   ├── [356M]  params_model_2_ptm.npz
    │   ├── [356M]  params_model_3_multimer.npz
    │   ├── [354M]  params_model_3.npz
    │   ├── [355M]  params_model_3_ptm.npz
    │   ├── [356M]  params_model_4_multimer.npz
    │   ├── [354M]  params_model_4.npz
    │   ├── [355M]  params_model_4_ptm.npz
    │   ├── [356M]  params_model_5_multimer.npz
    │   ├── [354M]  params_model_5.npz
    │   └── [355M]  params_model_5_ptm.npz
    ├── [4.0K]  pdb70
    │   ├── [ 410]  md5sum
    │   ├── [ 53G]  pdb70_a3m.ffdata
    │   ├── [2.0M]  pdb70_a3m.ffindex
    │   ├── [6.6M]  pdb70_clu.tsv
    │   ├── [ 21M]  pdb70_cs219.ffdata
    │   ├── [1.5M]  pdb70_cs219.ffindex
    │   ├── [3.2G]  pdb70_hhm.ffdata
    │   ├── [1.8M]  pdb70_hhm.ffindex
    │   └── [ 19M]  pdb_filter.dat
    ├── [4.0K]  pdb_mmcif
    │   ├── [9.1M]  mmcif_files
    │   └── [140K]  obsolete.dat
    ├── [4.0K]  pdb_seqres
    │   └── [208M]  pdb_seqres.txt
    ├── [4.0K]  uniclust30
    │   ├── [4.0K]  uniclust30_2018_08
    │   └── [4.0K]  uniclust30_2021_03
    ├── [4.0K]  uniprot
    │   └── [ 97G]  uniprot.fasta
    └── [4.0K]  uniref90
        └── [ 58G]  uniref90.fasta

### 2.1.1 usage

    Full AlphaFold protein structure prediction script.
    flags:
    
    /app/alphafold/run_alphafold.py:
      --[no]benchmark: Run multiple JAX model evaluations to obtain a timing that excludes the compilation time, which should be more
        indicative of the time required for inferencing many proteins.
        (default: 'false')
      --bfd_database_path: Path to the BFD database for use by HHblits.
      --data_dir: Path to directory of supporting data.
      --db_preset: <full_dbs|reduced_dbs>: Choose preset MSA database configuration - smaller genetic database config (reduced_dbs) or
        full genetic database config  (full_dbs)
        (default: 'full_dbs')
      --fasta_paths: Paths to FASTA files, each containing a prediction target. Paths should be separated by commas. All FASTA paths
        must have a unique basename as the basename is used to name the output directories for each prediction.
        (a comma separated list)
      --hhblits_binary_path: Path to the HHblits executable.
        (default: '/usr/bin/hhblits')
      --hhsearch_binary_path: Path to the HHsearch executable.
        (default: '/usr/bin/hhsearch')
      --hmmbuild_binary_path: Path to the hmmbuild executable.
        (default: '/usr/bin/hmmbuild')
      --hmmsearch_binary_path: Path to the hmmsearch executable.
        (default: '/usr/bin/hmmsearch')
      --is_prokaryote_list: Optional for multimer system, not used by the single chain system. This list should contain a boolean for
        each fasta specifying true where the target complex is from a prokaryote, and false where it is not, or where the origin is
        unknown. These values determine the pairing method for the MSA.
        (a comma separated list)
      --jackhmmer_binary_path: Path to the JackHMMER executable.
        (default: '/usr/bin/jackhmmer')
      --kalign_binary_path: Path to the Kalign executable.
        (default: '/usr/bin/kalign')
      --max_template_date: Maximum template release date to consider. Important if folding historical test sets.
      --mgnify_database_path: Path to the MGnify database for use by JackHMMER.
      --model_preset: <monomer|monomer_casp14|monomer_ptm|multimer>: Choose preset model configuration - the monomer model, the monomer
        model with extra ensembling, monomer model with pTM head, or multimer model
        (default: 'monomer')
      --obsolete_pdbs_path: Path to file containing a mapping from obsolete PDB IDs to the PDB IDs of their replacements.
      --output_dir: Path to a directory that will store the results.
      --pdb70_database_path: Path to the PDB70 database for use by HHsearch.
      --pdb_seqres_database_path: Path to the PDB seqres database for use by hmmsearch.
      --random_seed: The random seed for the data pipeline. By default, this is randomly generated. Note that even if this is set,
        Alphafold may still not be deterministic, because processes like GPU inference are nondeterministic.
        (an integer)
      --small_bfd_database_path: Path to the small version of BFD used with the "reduced_dbs" preset.
      --template_mmcif_dir: Path to a directory with template mmCIF structures, each named <pdb_id>.cif
      --uniclust30_database_path: Path to the Uniclust30 database for use by HHblits.
      --uniprot_database_path: Path to the Uniprot database for use by JackHMMer.
      --uniref90_database_path: Path to the Uniref90 database for use by JackHMMER.
      --[no]use_precomputed_msas: Whether to read MSAs that have been written to disk. WARNING: This will not check if the sequence,
        database or configuration have changed.
        (default: 'false')
    
    absl.app:
      -?,--[no]help: show this help
        (default: 'false')
      --[no]helpfull: show full help
        (default: 'false')
      --[no]helpshort: show this help
        (default: 'false')
      --[no]helpxml: like --helpfull, but generates XML output
        (default: 'false')
      --[no]only_check_args: Set to true to validate args and exit.
        (default: 'false')
      --[no]pdb: Alias for --pdb_post_mortem.
        (default: 'false')
      --[no]pdb_post_mortem: Set to true to handle uncaught exceptions with PDB post mortem.
        (default: 'false')
      --profile_file: Dump profile information to a file (for python -m pstats). Implies --run_with_profiling.
      --[no]run_with_pdb: Set to true for PDB debug mode
        (default: 'false')
      --[no]run_with_profiling: Set to true for profiling the script. Execution will be slower, and the output format might change over
        time.
        (default: 'false')
      --[no]use_cprofile_for_profiling: Use cProfile instead of the profile module for profiling. This has no effect unless
        --run_with_profiling is set.
        (default: 'true')
    
    absl.logging:
      --[no]alsologtostderr: also log to stderr?
        (default: 'false')
      --log_dir: directory to write logfiles into
        (default: '')
      --logger_levels: Specify log level of loggers. The format is a CSV list of 'name:level'. Where 'name' is the logger name used
        with 'logging.getLogger()', and 'level' is a level name  (INFO, DEBUG, etc). e.g. 'myapp.foo:INFO,other.logger:DEBUG'
        (default: '')
      --[no]logtostderr: Should only log to stderr?
        (default: 'false')
      --[no]showprefixforinfo: If False, do not prepend prefix to info messages when it's logged to stderr, --verbosity is set to INFO
        level, and python logging is used.
        (default: 'true')
      --stderrthreshold: log messages at this level, or more severe, to stderr in addition to the logfile.  Possible values are
        'debug', 'info', 'warning', 'error', and 'fatal'.  Obsoletes --alsologtostderr. Using --alsologtostderr cancels the effect of
        this flag. Please also note that this flag is subject to --verbosity and requires logfile not be stderr.
        (default: 'fatal')
      -v,--verbosity: Logging verbosity level. Messages logged at this level or lower will be included. Set to 1 for debug logging. If
        the flag was not set or supplied, the value will be changed from the default of -1 (warning) to 0 (info) after flags are
        parsed.
        (default: '-1')
        (an integer)
    
    absl.testing.absltest:
      --test_random_seed: Random seed for testing. Some test frameworks may change the default value of this flag between runs, so it
        is not appropriate for seeding probabilistic tests.
        (default: '301')
        (an integer)
      --test_randomize_ordering_seed: If positive, use this as a seed to randomize the execution order for test cases. If "random",
        pick a random seed to use. If 0 or not set, do not randomize test case execution order. This flag also overrides the
        TEST_RANDOMIZE_ORDERING_SEED environment variable.
        (default: '')
      --test_srcdir: Root of directory tree where source files live
        (default: '')
      --test_tmpdir: Directory for temporary testing files
        (default: '/tmp/absl_testing')
      --xml_output_file: File to store XML test results
        (default: '')
    
    tensorflow.python.ops.parallel_for.pfor:
      --[no]op_conversion_fallback_to_while_loop: DEPRECATED: Flag is ignored.
        (default: 'true')
    
    tensorflow.python.tpu.client.client:
      --[no]hbm_oom_exit: Exit the script when the TPU HBM is OOM.
        (default: 'true')
      --[no]runtime_oom_exit: Exit the script when the TPU runtime is OOM.
        (default: 'true')
    
    absl.flags:
      --flagfile: Insert flag definitions from the given file into the command line.
        (default: '')
      --undefok: comma-separated list of flag names that it is okay to specify on the command line even if the program does not define
        a flag with that name.  IMPORTANT: flags in this list that have arguments MUST use the --flag=value format.
        (default: '')

## FAQ

Q. I'm seeing the message "RuntimeError: Resource exhausted: Out of
memory"

A. make sure you have the following two lines in your job script

    export SINGULARITYENV_TF_FORCE_UNIFIED_MEMORY=1  
    export SINGULARITYENV_XLA_PYTHON_CLIENT_MEM_FRACTION=4.0

-----

Q. I'm seeing the message: raise ValueError('The number of positions
must match the number of atoms')

A. See this [bug
report](https://github.com/deepmind/alphafold/issues/246)

-----

Q. How do I view the contents of a .pkl file such as
result\_model\_2.pkl?

A. Use python to view the contents. More code needed to save to a file.

    module purge
    module load GCC/10.2.0  CUDA/11.1.1  OpenMPI/4.0.5  AlphaPickle/1.4.1
    python
    >>> import pandas as pd
    >>> myresults=pd.read_pickle('/path/to/your/result_model_2.pkl')
    >>> print(myresults)

-----

Q. How do I create graphs of the .pkl model files

A. Use AlphaPickle which can be run on the login node after an AlphaFold
job is complete since AlphaPickle takes less than a minute to complete.

    module purge
    module load GCC/10.2.0  CUDA/11.1.1  OpenMPI/4.0.5  AlphaPickle/1.4.1
    
    # run AlphaPickle to create a graph for each model .pkl file.
    # Name the -od directory based on how you named --output_dir and --fasta_paths in the run_alphafold.py command
    run_AlphaPickle.py -od out_alphafold/T1050

-----

Q. How can I extract ptm, iptm and ranking\_confidence values from a
pickle file such as result\_model\_2.pkl?

A. Use pickle2csv.py to extract the values for ptm, iptm and
ranking\_confidence when using --model\_preset=monomer\_ptm

    If you used --model\_preset=monomer then only ranking\_confidence
will be extracted

    module purge
    module load GCC/10.2.0  CUDA/11.1.1  OpenMPI/4.0.5  AlphaPickle/1.4.1
    pickle2csv.py -i path/to/pickle/file/result_model_2.pkl -o output.csv

-----

### Citation

  - If you use an AlphaFold prediction in your work, please cite the
    following papers:

Jumper, J et al. Highly accurate protein structure prediction with AlphaFold. Nature (2021).

Varadi, M et al. AlphaFold Protein Structure Database: massively expanding the structural coverage of protein-sequence space with high-accuracy models. Nucleic Acids Research (2021).

  - In addition, if you use the AlphaFold-Multimer mode, please cite:

Evans, R et al. Protein complex prediction with AlphaFold-Multimer, [doi.org/10.1101/2021.10.04.463034](https://doi.org/10.1101/2021.10.04.463034)

  - AlphaPickle

Arnold, M. J. (2021) AlphaPickle, [doi.org/10.5281/zenodo.5708709](https://doi.org/10.5281/zenodo.5708709)

## ParallelFold

[ParallelFold](https://github.com/Zuricho/ParallelFold) can help you
accelerate AlphaFold when you want to predict multiple sequences. After
dividing the CPU part and GPU part, users can finish feature step by
multiple processors.

Using ParallelFold, the first three steps, jackhammer, jackhammer and
HHblits are supposed to run as three separate processes in parallel but
currently this parallelization step is not implemented in the
ParallelFold [repo](https://github.com/Zuricho/ParallelFold/issues/17).
When this step is parallelized, it will require 20 cores; 8 cores each
for the two jackhammer steps and 5 cores for the HHblits step.

Using ParallelFold, you can run AlphaFold 2~3 times faster than
DeepMind's procedure.

Example T1050.fasta file took 6 hrs 6 min to complete the CPU step and
39 minutes for the GPU step

### first step on CPU

Currently recommended to use 8 cpus-per-task and 60G memory until
ParallelFold is parallelized.

    #!/bin/bash  
    #SBATCH --export=NONE                # do not export current env to the job  
    #SBATCH --job-name=parallelfold      # job name  
    #SBATCH --time=1-00:00:00            # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1          # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24           # CPUs (threads) per command  
    #SBATCH --mem=180G                   # total memory per node  
    #SBATCH --output=stdout.%x.%j        # save stdout to file  
    #SBATCH --error=stderr.%x.%j         # save stderr to file  
      
    module load ParallelFold/2.1.1  
    source activate /sw/hprc/sw/Anaconda3/2021.11/envs/parallelfold_2.1.1  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.1  
      
    # First, you need CPUs to run get features, run only feature step on CPU by using option: -f  
    run_alphafold.sh **-f** -d $DOWNLOAD_DIR -o out_parallelfold_monomer -p monomer -t 2022-01-01 -i T1050.fasta

### second step on GPU

Add the \#SBATCH --gres line to run this part on a GPU compute node.

    #!/bin/bash  
    #SBATCH --export=NONE                # do not export current env to the job  
    #SBATCH --job-name=parallelfold      # job name  
    #SBATCH --time=08:00:00              # max job run time dd-hh:mm:ss  
    #SBATCH --ntasks-per-node=1          # tasks (commands) per compute node  
    #SBATCH --cpus-per-task=24           # CPUs (threads) per command  
    #SBATCH --mem=180G                   # total memory per node  
    **#SBATCH 
    --gres=gpu:a100:1**            # request 1 A100 GPU  
    #SBATCH --output=stdout.%x.%j        # save stdout to file  
    #SBATCH --error=stderr.%x.%j         # save stderr to file  
      
    module load ParallelFold/2.1.1  
    source activate /sw/hprc/sw/Anaconda3/2021.11/envs/parallelfold_2.1.1  
      
    export TF_FORCE_UNIFIED_MEMORY=1  
    export XLA_PYTHON_CLIENT_MEM_FRACTION=4.0  
      
    DOWNLOAD_DIR=/scratch/data/bio/alphafold_2.1.1  
      
    # second step runs on GPU  
    run_alphafold.sh -d $DOWNLOAD_DIR -u $CUDA_VISIBLE_DEVICES -o out_parallelfold_monomer -p monomer -t 2022-01-01 -i T1050.fasta

### third step visualize

This step does not work yet. It is still in development by ParallelFold
group

    module purge
    module load ParallelFold/2021.10.28
    module load GCC/9.3.0 OpenMPI/4.0.3 matplotlib/3.2.1-Python-3.8.2
    module load pymol-open-source/2.5.0-Python-3.8.2
    
    run_figure.py [SystemName]
