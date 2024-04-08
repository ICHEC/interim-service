# ABINIT

```{admonition} Versions Installed
:class: note

`Kay: 8.10.1/8.10.2`

`LXP: 9.10.5`
```

## Description

ABINIT is a package whose main program allows one to find the total
energy, charge density and electronic structure of systems made of
electrons and nuclei (molecules and periodic solids) within Density
Functional Theory (DFT), using pseudopotentials and a planewave basis.

## License

ABINIT is available under the [GNU General Public License](http://www.gnu.org/copyleft/gpl.html).

## Benchmarks

N/A.

## Job Submission Example


### For Kay

```bash -l
#!/bin/bash
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
#SBATCH --job-name=myjobname

# Charge job to myproject
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myemailaddress@universityname.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

# Load the module for the specific version
module load abinit/8.10.2
mpirun -np 80 abinit < MyInputFile > MyOutputFile
```

### For Meluxina

```bash -l
#!/bin/bash
# Slurm flags
#SBATCH -p cpu
#SBATCH -N 1
#SBATCH --qos default
#SBATCH -t 02:00:00
#SBATCH --job-name=myjobname
# Charge job to myproject
#SBATCH -A myproject
# Write stdout+stderr to file
#SBATCH -o output.txt
# Mail me on job start & end
#SBATCH --mail-user=myemailaddress@universityname.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

# Load the module for the specific version
module load abinit
mpirun -np 128 abinit < MyInputFile > MyOutputFile
```

## Additional Notes

Further information can be obtained
at [www.abinit.org/about/](http://www.abinit.org/about/).

