# GAMESS-US

```{admonition} Versions Installed
:class: note

`Kay: aug02.R2.2018`

`LXP: `
```

## Description

GAMESS-US is a general purpose *ab initio* molecular electronic structure program for performing **SCF** and **MCSCF-gradient** calculations, together with a variety of techniques for post Hartree Fock calculations.

## License

Gamess-US is available for use. Please contact the [Helpdesk](https://rt.ichec.ie "ICHEC Helpdesk") to gain access.

## Benchmarks

N/A.

## Submission script example
```bash
#!/bin/sh
# All the informations about queues can be obtained by 'sinfo'
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
#SBATCH --job-name=jobname  
#SBATCH -t 60:00:00

# Charge job to myaccount
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=your@email.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load  gamess-us/aug02.R2.2018
export OMP_NUM_THREADS=1

# GAMESS needs folder $HOME/scr. Create it before submit the job
rungms   file.inp > file.log
```

### Additional Notes

Further information can be obtained at <http://www.msg.ameslab.gov/gamess/>.

