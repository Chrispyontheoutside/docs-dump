# SWAN

## Description

SWAN is a third-generation wave model, developed at Delft University of
Technology, that computes random, short-crested wind-generated waves in
coastal regions and inland waters.

Homepage: <http://swanmodel.sourceforge.net>

## Access

Currently, SWAN is only available on Ada, and comes in three module
versions.

  - SWAN/delft3d-5.01.00.2163-intel-2015B
  - SWAN/delft3d-5.01.00.5520-intel-2015B
  - SWAN/delft3d-6.02.01.5425-intel-2015B

To load one of the modules:

`module load SWAN/delft3d-6.02.01.5425-intel-2015B`

Or:

`ml SWAN/delft3d-6.02.01.5425-intel-2015B`

## Example Job Files

The example loads scripts which can be found on Ada at
/sw/hprc/Delft3D/6.02.01.5425/examples.

### Parallel Job File Example

`#BSUB -J wave`  
`#BSUB -n 20`  
`#BSUB -R "span[ptile=20]"`  
`#BSUB -M 2000`  
`#BSUB -o output.%J`  
`#BSUB -L /bin/bash`  
`#BSUB -W 03:00`  
  
`module load SWAN/delft3d-6.02.01.5425-intel-2015B`  
`export OMP_NUM_THREADS=20`  
`./run_flow2d3d.sh`
