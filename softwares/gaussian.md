# Gaussian

```{admonition} Versions Installed
:class: note

`Kay: 09e01 / 16b01`

`LXP: `

```

## Description

Starting from the basic laws of quantum mechanics, Gaussian predicts the
energies, molecular structures, and vibrational frequencies of molecular
systems, along with numerous molecular properties derived from these
basic computation types.

## License

Gaussian is available for use. Please contact the [Helpdesk](/academic/national-hpc/user-support "ICHEC Helpdesk") to gain access.

## Benchmarks

N/A.

## Thin Component

Gaussian jobs on Kay are run via shared memory (**without Linda**) on
a **single** compute node. Users should specify 40 processes in their
Gaussian input file (.com or .gjf)

`%nproc=40`

or

`%cpu=0-39`

For good performance use the %mem directive. A good compromise would be
100GB. If needed at expense of I/O caches one can go as high as 150GB,
but expect a few percentages lost in performance compared with the 100GB
case. Of course you can fine tune these values.

`%mem=100000mb`

An example of submission slurm script:

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
#SBATCH -t 120:00:00
#SBATCH --job-name=myjobname
    
# Charge job to myproject 
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myemailaddress@universityname.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR
echo $GAUSS_SCRDIR

module load gaussian/16b01

g16 < input.gjf > output.log   
```

## Additional notes

The Gaussian module sets the **GAUSS_SCRDIR** to the correct location
for that node type. Jobs can use very large RWF files as the scratch
space is provided by a large high-performance shared volume including
the follow in your submission script:

```bash
export GAUSS_SCRDIR=/scratch/local/
```

Further information can be obtained at [www.gaussian.com](http://www.gaussian.com/ "Gaussian homepage").

