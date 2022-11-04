# BUSCO

[GCATemplates](/kb3/Software/useful-tools/SW@GCATemplates/ "wikilink") available: [terra
(busco 4.0.5)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/terra/run_busco_4.0.5_genome_terra.sh)
    [grace
(busco 4.1.2)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_4.1.2_genome_grace.sh)
    [grace (busco 5.1.2
metaeuk)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_5.1.2_genome_metaeuk_grace.sh)
    [grace (busco 5.1.2
augustus)](https://github.tamu.edu/cmdickens/GCATemplates/blob/master/templates/grace/run_busco_5.1.2_genome_augustus_grace.sh)

BUSCO [homepage](http://busco.ezlab.org/)

#### version 5.0.x

Version 5.0.0+ now uses Metaeuk as the default gene predictor instead of
Augustus so you don't need to rsync the AUGUSTUS directory unless you
want to use Augustus.

Databases for v5.0.0+ are found on Grace in the directory:

`/scratch/data/bio/busco5/lineages`

Contact the HPRC helpdesk if you need additional databases downloaded to
the shared busco5 lineages directory.

#### version 4.0.x

To use BUSCO you need to copy the augustus config files (about 1000
files) to your $SCRATCH directory (only need to do once). Make sure you
load the BUSCO module successfully by running 'module list' after the
module load command.

` module purge`  
` module load BUSCO/4.0.5-foss-2019b-Python-3.7.4`  
` module list`  
` mkdir $SCRATCH/my_augustus_config`  
` rsync -r /sw/eb/software/AUGUSTUS/3.3.3-foss-2019b/  $SCRATCH/my_augustus_config`  
` chmod -R 755 $SCRATCH/my_augustus_config`

You need to add the following in your job script:

` export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config/config"`

The lineages for version 4.0.x use odb10. Contact HPRC helpdesk if there
is not a lineage for your organism in the odb10 directory.

`Grace: /scratch/data/bio/busco4/lineages/`  
`Terra: /scratch/data/bio/BUSCO/odb10/lineages/`

#### version 3.0.2b

To use BUSCO you need to copy the augustus config files (about 1000
files) to your $SCRATCH directory (only need to do once). Make sure you
load the BUSCO module successfully by running 'module list' after the
module load command.

` module purge`  
` module load BUSCO/3.0.2b-intel-2015B-python-2.7.6-generic`  
` module list`  
` mkdir $SCRATCH/my_augustus_config`  
` rsync -r $EBROOTAUGUSTUS/ $SCRATCH/my_augustus_config`  
` chmod -R 755 $SCRATCH/my_augustus_config`

You need to add the following in your job script:

` export AUGUSTUS_CONFIG_PATH="$SCRATCH/my_augustus_config/config"`

A list of available augustus species can be found here:

` /software/easybuild/software/AUGUSTUS/3.3-intel-2015B/config/species/`

A list of available busco lineages for version 3.0.2b can be found here:

` /scratch/datasets/BUSCO/v3.0.2/`

Run BUSCO in transcriptome mode:

`python $EBROOTBUSCO/scripts/run_BUSCO.py --mode transcriptome`

If you are processing transcriptome data, use **--mode trans** instead
of **--mode Trans** for BUSCO version 1.2
