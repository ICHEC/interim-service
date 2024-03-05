# DL_POLY

```{admonition} Versions Installed
:class: note

`Kay: 4.09`

`LXP: `

```

## Description

`DL_POLY` is a package of subroutines, programs and data files, designed to facilitate molecular dynamics simulations of macromolecules, polymers, ionic systems and solutions on a distributed memory parallel computer. `DL_POLY` was developed at the STFC Daresbury Laboratory by W.
Smith, T.R. Forester and I.T. Todorov. Three versions of `DL_POLY` are currently available:

`DL_POLY_2` is the original version which has been parallelised using the Replicated Data strategy and is useful for simulations of up to 30,000 atoms on 100 processors.

`DL_POLY_3` is a version which uses Domain Decomposition to achieve parallelism and is suitable for simulations of order 1 million atoms on 8-1024 processors.

`DL_POLY_4`'s general design provides scalable performance from a single processor workstation to a high performance parallel computer. `DL_POLY_4` offers fully parallel I/O as well as a netCDF alternative (HDF5 library dependence) to the default ASCII trajectory file. It is also available as a CUDA+OpenMP port, developed in collaboration with ICHEC, to harness the power offered by NVIDIA® GPUs. A full description of the available `DL_POLY_4` functionality may be obtained from
the [DL_POLY_4 User Manual (PDF)](https://www.ehu.eus/sgi/ARCHIVOS/dlpoly_man.pdf "DL_POLY_4 User Manual").

### License

Currently, only one version of the DL_POLY software is available under an [STFC](https://www.stfc.ac.uk/files/stfc-intellectual-property-rights/ "STFC") license, DL_POLY_4, and with support provisioned to the UK's academia only. The former DL_POLY_2 version (authored by W. Smith, T.R. Forester and I.T. Todorov) is now transformed into [DL_POLY_CLASSIC](https://wiki.rc.ucl.ac.uk/wiki/DL_Poly_Classic_1.9_on_Legion "DL_POLY_CLASSIC") and available as open source under the BSD license.

Users should express their interest to the [Helpdesk](/academic/national-hpc/user-support "Helpdesk") to gain access to the executables.

### Additional Notes

To use a version of DL_POLY on Fionn load the relevant environment
module:
```bash
module load dlpoly/4.09
```

Assuming that the following SLURM script is saved as dlpoly.sub, the job
can be submitted to the queue by running the following command in the
same directory:

```bash
sbatch dlpoly.sub
```

### Job Submission Example on Fionn
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
#SBATCH -t 02:00:00
#SBATCH --job-name=dlpolyJob

# Charge job to myproject 
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load dlpoly/4.09
mpirun -np 4 DLPOLY.Z > output
```

## Further information

More information can be obtained [here](https://www.scd.stfc.ac.uk/Pages/DL_POLY.aspx).
