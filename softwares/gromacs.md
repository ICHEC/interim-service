#  GROMACS

```{admonition} Versions Installed
:class: note

`Kay: 2018.3`

`LXP: `

```

## Description

GROMACS is a versatile package to perform molecular dynamics, i.e., simulate the Newtonian equations of motion for systems with hundreds to millions of particles. It is primarily designed for biochemical molecules like proteins and lipids that have a lot of complicated bonded
interactions, but as GROMACS is fast at calculating the non-bonded interactions there is also much research on non-biological systems, e.g., polymers.

## License

GROMACS is available under the [GNU General Public License](http://www.gnu.org/copyleft/gpl.html "GPL homepage").

## Benchmarks

N/A

## Job Submission Example to CPU-only nodes:

To run the code in parallel on Kay, please follow the below example. 

```bash
#!/bin/sh
#SBATCH -p ProdQ
#SBATCH -N 2
#SBATCH -t 02:00:00
#SBATCH --job-name=gromacsjob

# Charge job to myproject 
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=my@email.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load gromacs/2018.3

mpirun -np 80 gmx_mpi_d mdrun -deffnm prod
```

## Job submission to GPU nodes

One can experience significant performance boost when using Gromacs in GPU nodes.

In the following section, we describe a few guideline to use Gromacs with GPU in the Kay supercomputer.

First of all, Gromacs is implemented with external MPI library (Intel MPI) and it is built to use in multiple nodes. So, the current installations in Kay do not support thread-mpi. Please do not use `-ntmpi` and `-nt` flags (even if you are running your job in 1 node) otherwise they will result in "Fatal Error". Instead one can control number of MPI threads using MPI variables.

### Some important flags that you may need to submit your jobs to GPU nodes:

<table data-border="1" data-cellpadding="1" data-cellspacing="1"
style="width: 500px;">
<tbody>
<tr class="odd">
<td style="width: 92px">-np</td>
<td style="width: 395px">used to set total number of MPI ranks for the
job</td>
</tr>
<tr class="even">
<td style="width: 92px">-npme</td>
<td style="width: 395px">used to set total number of ranks that will be
working on PME calculations</td>
</tr>
<tr class="odd">
<td style="width: 92px">-dlb</td>
<td style="width: 395px">used to set dynamic load balancing
(auto/no/yes)</td>
</tr>
<tr class="even">
<td style="width: 92px">-ntomp</td>
<td style="width: 395px">used to set number of OpenMP threads per MPI
rank</td>
</tr>
<tr class="odd">
<td style="width: 92px">-ntomp_pme</td>
<td style="width: 395px">used to set number of OpenMP threads per MPI
rank for the PME job</td>
</tr>
<tr class="even">
<td style="width: 92px">-nb</td>
<td style="width: 395px">Used to set where to execute the short-range
non-bonded interactions (auto/cpu/gpu)</td>
</tr>
<tr class="odd">
<td style="width: 92px">-pme</td>
<td style="width: 395px">Used to set where to execute the long-range
non-bonded interactions (auto/cpu/gpu)</td>
</tr>
<tr class="even">
<td style="width: 92px">-bonded</td>
<td style="width: 395px">Used to set where to execute the bonded
interactions that are part of the PP workload for a domain
(auto/cpu/gpu)</td>
</tr>
<tr class="odd">
<td style="width: 92px">-gpu_id</td>
<td style="width: 395px">this specifies the ID numbers of the GPUs (
-gpu_id 01 )</td>
</tr>
<tr class="even">
<td style="width: 92px">-gputasks</td>
<td style="width: 395px">this flag accepts a string value that specifies
the ID numbers of the GPUs to be used by corresponding GPU tasks on this
node</td>
</tr>
</tbody>
</table>

 

### A few examples

Below are a few examples shown below to demonstrate how these flags can be used in Kay to submit your job to GPU nodes. 

#### Example 1:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=20
mpirun -np 2 gmx_mpi mdrun -ntomp 20 -nb gpu -pme cpu -gpu_id 01 -deffnm prod
```

In this case, you have initiated 2 MPI ranks and 2 GPUs with id 0 and 1. Each MPI rank will use 20 OpenMP threads. The particle mesh Ewald (PME) calculations for the long-range forces will be performed on the CPUs, while the non-bonded short-ranged force calculations will be done on the
GPUs.

#### Example 2:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=20
mpirun -np 2 gmx_mpi mdrun -ntomp 20 -nb gpu -gpu_id 01 -deffnm prod
```

In this case, you have initiated 2 MPI ranks and 2 GPUs with id 0 and 1
in a single node. Each MPI rank will use 20 OpenMP threads. The non-bonded short-ranged force calulations will be done on the GPUs.Please note that we have not chosen any value for the `-pme` flag which means that it will be set to the default "auto". This uses a
compatible GPU for PME if available.

#### Example 3:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=6
mpirun -np 2 gmx_mpi mdrun -ntomp 6 -nb gpu -gpu_id 01 -deffnm prod
```

This is similar to the example 2 shown above with the only difference in number of OpenMP threads per MPI rank. Note that you also need to set the `OMP_NUM_THREADS` to an appropriate value. In this case, it is set to six.


#### Example 4:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 2
#SBATCH -t 24:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH --reservation=GROMACS
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=20
mpirun -np 4 -ppn 2 gmx_mpi mdrun -ntomp 20 -nb gpu -pme gpu -npme 1 -ntomp_pme 1 -gputasks 01 -deffnm prod
```

This script submits the job to two nodes using 4 MPI ranks and 4 GPUs in total. There are two different kind of GPU jobs defined here: non-bonded (`-nb`) and PME (`-pme`). PME job has been set to be performed by 1 MPI rank (`-npme 1`) and 1 OpenMp thread (`-ntomp_pme 1`) since the decomposition of PME rank is not currently supported by Gromacs. `-gputask` flag accepts a string value that specifies the ID numbers of the GPUs to be used by corresponding GPU tasks on this node. For the non-PME job the number of OpenMP threads is set to 20 per MPI rank.

#### Example 5:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 48:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=39
mpirun -np 2 -ppn 2 gmx_mpi mdrun -ntomp 39 -nb gpu -pme gpu -npme 1 -ntomp_pme 1 -gputasks 01 -deffnm prod
```

In this case, the job is submitted to 1 node with 2 MPI ranks, and 2 GPUs. For the PME job, the number of OpenMP threads is set to 1 (`-ntomp_pme 1`) and for the non-PME job this is set to 39
(`-ntomp 39`). One GPU with id 1 is fully dedicated to do the PME calculations in this case, while the other GPU is doing the non-bonded force calculations.

#### Example 6: ----------------

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 48:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH --reservation=GROMACS
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=20
mpirun -np 2 -ppn 2 gmx_mpi mdrun -ntomp 20 -nb gpu -pme gpu -npme 1 -ntomp_pme 1 -gputasks 01 -deffnm prod
```

This is similar to example 5 with the only exception is in number of OpenMP threads per MPI-rank handling the non-bonded force calculation. This is set to twenty in this case.

#### Example 7:

```bash
#!/bin/sh
#SBATCH -p GpuQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=benchmark
#SBATCH -A sci_test
#SBATCH --reservation=GROMACS
#SBATCH -o output.txt
#SBATCH --mail-user=prithwish.nandi@ichec.ie
#SBATCH --mail-type=BEGIN,END
cd $SLURM_SUBMIT_DIR

module load gromacs/2019.3_gpu
export OMP_NUM_THREADS=4
mpirun -np 2 -ppn 2 gmx_mpi mdrun -ntomp 4  -nb gpu -pme gpu -npme 1 -ntomp_pme 1 -gputasks 01 -deffnm prod
```

This is also similar to example 5 with the only exception is in number of OpenMP threads per MPI-rank handling the non-bonded force calculation. This is set to four in this case.

### Expected speed-up when using these settings:

A GROMACS job of solvated Lysozyme in a box (326064 atoms in total) is simulated for a period of 2 ns in each case.

<table data-border="1" data-cellpadding="1" data-cellspacing="1"
style="width: 500px;">
<tbody>
<tr class="odd">
<td>job type</td>
<td>number of nodes</td>
<td>performance (ns/day)</td>
<td>speed-up</td>
</tr>
<tr class="even">
<td>cpu-only</td>
<td>1</td>
<td>19.75</td>
<td>1</td>
</tr>
<tr class="odd">
<td>GPU example 1</td>
<td>1</td>
<td>33.52</td>
<td>1.70</td>
</tr>
<tr class="even">
<td>GPU example 2</td>
<td>1</td>
<td>33.56</td>
<td>1.70</td>
</tr>
<tr class="odd">
<td>GPU example 3</td>
<td>1</td>
<td>16.67</td>
<td>0.84</td>
</tr>
<tr class="even">
<td>GPU example 4</td>
<td>2</td>
<td>61.87</td>
<td>3.13</td>
</tr>
<tr class="odd">
<td>GPU example 5</td>
<td>1</td>
<td>30.13</td>
<td>1.53</td>
</tr>
<tr class="even">
<td>GPU example 6</td>
<td>1</td>
<td>29.02</td>
<td>1.50</td>
</tr>
<tr class="odd">
<td>GPU example 7</td>
<td>1</td>
<td>15.14</td>
<td>0.77</td>
</tr>
</tbody>
</table>

From the above table, one can notice that depending on the settings the speed-up gained from a GPU node can vary a lot. The above settings are tentative only to demonstrate the usage. Users are recommended to perform thorough optimisation  to get optimal values of these settings for availing maximum possible speedup for their production runs.


### Additional Notes

Further information can be obtained at [www.gromacs.org](http://www.gromacs.org/ "GROMACS homepage").

