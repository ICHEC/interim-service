# Siesta

```{admonition} Versions Installed
class: note

`Kay: 4.0.2/4.1.5`

`LXP: `

```


## Description

SIESTA is both a method and its computer program implementation, to
perform efficient electronic structure calculations and ab initio
molecular dynamics simulations of molecules and solids. SIESTA's
efficiency stems from the use of strictly localised basis sets and from
the implementation of linear-scaling algorithms which can be applied to
suitable systems. A very important feature of the code is that its
accuracy and cost can be tuned in a wide range, from quick exploratory
calculations to highly accurate simulations matching the quality of
other approaches, such as plane-wave and all-electron methods.

The possibility of treating large systems with some first-principles
electronic-structure methods has opened up new opportunities in many
disciplines. The SIESTA program is distributed freely to academics and
has become quite popular, being increasingly used by researchers in
geosciences, biology, and engineering (apart from those in its natural
habitat of materials physics and chemistry). Currently there are several
thousand users all over the world, and the paper describing the method
(J. Phys. Cond. Matt. 14, 2745 (2002)) has had more than 9000 citations.

## License

Starting in the Spring of 2016, with the 4.0 version, SIESTA is released
under the terms of the GPL open-source license. The source can be
downloaded from [here](https://launchpad.net/siesta). Other versions of
SIESTA are distributed to academics free of charge (please see the
detailed conditions in the licence text), and can be installed by
computer centres to be used only by academics. These are not open source
versions. They cannot be redistributed. They can be accessed from
[here](https://departments.icmab.es/leem/siesta/CodeAccess/selector.html).

## Benchmarks

N/A.

## Additional Notes

To use siesta load the relevant environment module:

```bash
module load siesta/4.0.2
```

Further information can be obtained from [Siesta: Home](http://departments.icmab.es/leem/siesta/ "Siesta Homepage").

Siesta is a fully parallel application, below is an example of how to submit a job.

### Job Submission Example

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
#SBATCH --job-name=SiestaJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load siesta/4.0.2

mpirun -np 40 siesta < fe.fdf > fe.out
```

### How to cite Siesta:

The SIESTA method for ab-initio order-N materials simulation J. M.
Soler, E. Artacho,J. D. Gale, A. García, J. Junquera, P. Ordejón, and D.
Sánchez-Portal, J. Phys.: Condens. Matt. **14**, 2745-2779 (2002).

## Version 4.1.5

This version is not MPI enabled but can use OMP threads. Thus it is
restricted to a single node only. Below is an example of how to submit
this version of siesta. You can change the number of OMP threads being
used up to a maximum of 40.

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
#SBATCH --job-name=SiestaJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

export OMP_PLACES=cores
export OMP_PROC_BIND=close
export OMP_NUM_THREADS=10

module load siesta/4.1.5

siesta < fe.fdf > fe.out
```
