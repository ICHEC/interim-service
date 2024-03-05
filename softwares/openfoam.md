# OpenFOAM

```{admonition} Versions Installed
:class: note

`Kay: 6`

`LXP: `

```

## Description

OpenFOAM is an open source package for finite-volume based solution of problems in continuum mechanics, primarily Computational Fluid Dynamics (CFD). OpenFOAM is supplied with several standard solvers for different classes of flow problems, including multiphase flow and combustion. The object-oriented C++ implementation of OpenFOAM facilitates the development of custom flow solvers.

## License

OpenFOAM is available under the terms of the GNU General Public License.

## Benchmarks

N/A

## Job Submission Example

Like other jobs on ICHEC systems, OpenFOAM jobs must be submitted using a Slurm submission script. The following is an example Slurm submission script for allocating 1 node of Kay (40 cores) for 30 minutes, then running the channel395 tutorial in parallel over 4 cores within that
allocation. Note that OpenFOAM employs domain decomposition for parallel runs which is defined geometrically by *decomposeParDict* in the *system* directory. Each processor must be assigned a portion of the mesh on which to operate. For the case below, the corresponding
*decomposeParDict*, the default shipped with the source, defines 4 regions. The solvers can therefore only be run over 4 cores.

To vary this, the *decomposeParDict* must be edited accordingly (both numberOfSubdomains, and the (nx ny nz) "n" coeffs). More detailed information on running OpenFOAM in parallel can be
found [here](http://www.openfoam.org/docs/user/running-applications-parallel.php#x12-820003.4 "Running applications in parallel").

Load the desired version of openfoam using the *environment module*

```bash
version=6
module load openfoam/$version
source $OPENFOAM_ROOT/etc/bashrc
```

Copy the tutorial
```bash
cp -r $FOAM_TUTORIALS/incompressible/pimpleFoam/LES/channel395 ./
cd ./channel395
```

Create the submission script (and name it myjob.sh) for the SLURM Workload Manager and modify it with your parameters

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
#SBATCH -t 00:30:00
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
version=6
module load openfoam/$version
source $OPENFOAM_ROOT/etc/bashrc

# Generate mesh
blockMesh
# Decompose mesh
decomposePar
# Run simulation in parallel
srun -n 4 pimpleFoam -parallel
# Reconstruct solution
reconstructPar
# Postprocess
postChannel
```

Submit the job with the following command

```bash
sbatch myjob.sh
```

## Setting Environment Variables

Frequent OpenFOAM users will know that the custom linux environment is
set by sourcing the bashrc contained within the source code. Since the
bashrc file is sourced manually, unloading the module doesn't revert
back to the original environment state

## Post-Processing

On Kay, OpenFOAM usually is not compiled with the included Paraview
package due to performance considerations. We advise users to simply
create the reader module using

```bash
paraFoam -touch
```

and then, to transfer their case data to their local machine for further
post-processing.
 

## Additional Notes

Further information can be obtained from the OpenFOAM Foundation [Website](http://www.openfoam.org).

