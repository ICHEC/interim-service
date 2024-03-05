# VASP

```{admonition} Versions Installed
class: note

`Kay:  5.4.4`

`LXP: `

```


## Description

VASP (Vienna Ab-initio Simulation Package) is a package for performing *ab-initio* quantum-mechanical molecular dynamics (MD) using pseudopotentials and a plane wave basis set.

## License

ICHEC has a site license that allows us to provide access to binary versions of VASP (v. 4.6 and 5.4.4) to users who already have their own VASP license. In order to be allowed access to these versions users must contact the [Helpdesk](/academic/national-hpc/user-support "ICHEC Helpdesk") with their own VASP license number. Once we have confirmed these details with the authors we can grant access.

Custom versions can be installed only on a project basis. Contact the [Helpdesk](/academic/national-hpc/user-support) for details.

## Benchmarks

N/A.

### Job Submission Example 5.4.4

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
#SBATCH -N 2
#SBATCH -t 02:00:00
#SBATCH --job-name=vaspJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load vasp/5.4.4

mpirun -np 80 vasp_std > MyLogFile
```

## Additional Notes

Further information can be found [here](https://vasp.at/).