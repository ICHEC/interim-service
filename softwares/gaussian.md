# Gaussian

```{admonition} Versions Installed
:class: note

`Kay: 09e01 / 16b01`

`LXP: 16c02`

```

## Description

Starting from the basic laws of quantum mechanics, Gaussian predicts the
energies, molecular structures, and vibrational frequencies of molecular
systems, along with numerous molecular properties derived from these
basic computation types.

## License

Gaussian is available for use by all ICHEC users.

## Benchmarks

N/A.

## Thin Component

Gaussian jobs on Kay and MeluXina are run via shared memory (**without Linda**) on
a **single** compute node. Users should specify up to 40 processes on Kay/128 on MeluXina in the
Gaussian input file (.com or .gjf)

`%nproc=40` (Kay) or `%nproc=128` (MeluXina)

or

`%cpu=0-39` (Kay) or `%cpu=0-127` (MeluXina)

For good performance use the %mem directive. A good compromise would be
100GB. If needed at expense of I/O caches one can go as high as 150GB,
but expect a few percentages lost in performance compared with the 100GB
case. Of course you can fine tune these values.

`%mem=100000mb`

```{note}
Further testing and user input is required to understand the optimal configuration for Gaussian jobs on MeluXina. If you are using Gaussian on MeluXina, please contact us at [support@ichec.ie](mailto:support@ichec.ie) with your findings.
```

## Job submission example
An example of submission slurm script:

### On Kay

```bash
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

### On Meluxina

```bash
#!/bin/bash -l
# Slurm flags
#SBATCH -p cpu
#SBATCH --qos=default
#SBATCH --hint=nomultithread
#SBATCH -N 1
#SBATCH -t 12:00:00
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

module load gaussian/16c02

g16 < input.gjf > output.log
```


## Additional notes

On Kay, the Gaussian module sets the **GAUSS_SCRDIR** o the correct location for that node type. Jobs can use very large RWF files as the scratch space is provided by a large high-performance shared volume including the follow in your submission script:

```bash
export GAUSS_SCRDIR=/scratch/local/
```

For MeluXina, the node's RAMDISK (/dev/shm) is automatically set as the scratch directory as there are no local disks on CPU nodes. Note that on CPU nodes on MeluXina, the RAM space is 512 GB, so if your scratch files require larger space, you should change the scratch directory to your project directory:

```bash
export GAUSS_SCRDIR="<your project directory>"
```

Further information can be obtained at [www.gaussian.com](http://www.gaussian.com/ "Gaussian homepage").

