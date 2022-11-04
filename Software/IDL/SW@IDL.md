# IDL

## Description

IDL stands for Interactive Data Language. It is a scientific programming
language used across disciplines to extract meaningful visualizations
from complex numerical data.. It is popular in particular areas of
science, such as astronomy, atmospheric physics and medical imaging.

## Access

The IDL package is restricted by license. Individuals or groups have
purchased licenses for these packages and manage the list of users that
may access them.

## Interactive Run

`   module load IDLENVI/IDL`  
`   idl`

## Sample job file on Ada

`   #BSUB -J idl-test`  
`   #BSUB -L /bin/bash`  
`   #BSUB -W 0:10 -M 400 -n 1 -R "span[ptile=1]" -R "rusage[mem=400]"`  
`   #BSUB -o stdout.%J`  
`   `  
`   module load IDLENVI/IDL`  
`   idl<<!heredoc                     # use here doc to pass interactive commands`  
`   .r test_idl.pro`  
`   TEST_RPOC`  
`   !heredoc`

## Sample job file on Terra

`   #!/bin/bash`  
`   #SBATCH --export=NONE   `  
`   #SBATCH --get-user-env=L    `  
`   #SBATCH --job-name=test`  
`   #SBATCH --time=01:30:00         `  
`   #SBATCH --ntasks=1              `  
`   #SBATCH --mem=2560M             `  
`   #SBATCH --output=stdout.%j `  
`   `  
`   module load IDLENVI/IDL`  
`   idl<<!heredoc                     # use here doc to pass interactive commands`  
`   .r test_idl.pro`  
`   TEST_RPOC`  
`   !heredoc`

## Links

<http://www.atmos.umd.edu/~gcm/usefuldocs/IDL.html>

<http://www.harrisgeospatial.com/SoftwareTechnology/IDL.aspx>
