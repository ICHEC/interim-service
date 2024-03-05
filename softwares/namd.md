# NAMD


```{admonition} Versions Installed
:class: note

`Kay: 2.13b1`

`LXP: `

```

## Description

NAMD is a molecular dynamics application designed specifically for the simulation of large biomolecular systems using modern parallel architectures. NAMD was developed by the Theoretical and Computational Biophysics Group in the Beckman Institute for Advanced Science and Technology at the University of Illinois at Urbana-Champaign using object-oriented techniques. NAMD can read X-PLOR, CHARMM, AMBER, and GROMACS input files.

NAMD only uses the GPU for non-bonded force evaluation. Energy evaluation is done on the CPU. To benefit from GPU acceleration you should set outputEnergies to 100 or higher in the simulation config file. Some features are unavailable in CUDA builds, including alchemical free energy perturbation. As this is a new feature you are encouraged to test all simulations before beginning production runs. Forces evaluated on the GPU differ slightly from a CPU-only calculation, an effect more visible in reported scalar pressure values than in energies.

VMD is a molecular visualization program for displaying, animating, and analyzing large biomolecular systems using 3-D graphics and built-in scripting.

## License

The NAMD package is available for use by all ICHEC users. Contact the Helpdesk to gain access to this package.

## Job Submission Example on Kay

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
#SBATCH -N 10
#SBATCH --job-name=jobname  
#SBATCH -t 60:00:00

# Charge job to myaccount
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=my@email.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load namd/2.13b1
module load intel/2019

mpirun -np 400 namd2 input.namd > output.out
```

```{tip}
For the namd/2.13 module which is also on Kay, the name of the binary is `namd2_mpi`, not `namd2`. Make sure to check you are using the correct one.
```

## Further Information

More information can be obtained at the NAMD user guide available from
the NAMD [webpage](https://www.ks.uiuc.edu/Research/namd/).

