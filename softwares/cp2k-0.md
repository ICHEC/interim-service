# CP2K

```{admonition} Versions Installed
:class: note

`Kay: 6.1.0, 7.1`

`LXP: `

```

## Description

cp2k is a quantum chemistry and solid state physics software package
that can perform atomistic simulations of solid state, liquid,
molecular, periodic, material, crystal, and biological systems.

## License

cp2k is licensed to the public under the terms of the GNU Public
License (GPL).

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
#SBATCH --job-name=cp2kJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load cp2k/gfortran/7.1
source /ichec/packages/cp2k/gfortran/7.1/setup

ulimit -s unlimited

cp2k.psmp -i inputfile -o outputfile
```

## Notes

It is recommended to use the gfortran version of the cp2k module on Kay.
 We have had reports of memory leaks with the intel-compiled version.

Further information on cp2k can be obtained [here](https://www.cp2k.org/).

