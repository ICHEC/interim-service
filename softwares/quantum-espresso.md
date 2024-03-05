# Quantum Espresso

```{admonition} Versions Installed
class: note

`Kay: 6.3`

`LXP: `

```

## Description

Quantum ESPRESSO is an integrated suite of computer codes for
electronic-structure calculations and materials modeling at the
nanoscale. It is based on density-functional theory, plane waves, and
pseudopotentials (both norm-conserving and ultrasoft).

## License

Quantum Espresso is licensed to the public under the terms of the GNU
Public License (GPL) Version 2.

## Benchmarks

N/A.

## Job Submission Example on Kay

```bash
#!/bin/sh
# All the information about queues can be obtained using 'sinfo'
# PARTITION AVAIL  TIMELIMIT  
# DevQ         up    1:00:00   
# ProdQ*       up 3-00:00:00    
# LongQ        up 6-00:00:00    
# ShmemQ       up 3-00:00:00    
# PhiQ         up 1-00:00:00   
# GpuQ         up 2-00:00:00    

# Slurm flags
#SBATCH -p ProdQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=QEJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load qe/6.3

mpirun -np 40 pw.x < MyInputFile > MyOutputFile
```

Further information can be obtained [here.](https://www.quantum-espresso.org/).

