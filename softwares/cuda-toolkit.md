# NVIDIA CUDA Toolkit

```{admonition} Versions Installed
:class: note

`Kay: 10 / 10.1.243 / 11.2 / 11.3 / 11.4`

`LXP: `

```

## Description

The NVIDIA CUDA Toolkit provides command-line and graphical tools for
building, debugging and optimizing the performance of applications
accelerated by NVIDIA GPUs, runtime and math libraries, and
documentation including programming guides, user manuals, and API
references.

## License

The CUDA toolkit is available under the CUDA Toolkit End User License
Agreement (see CUDA Toolkit [documentation](https://docs.nvidia.com/cuda/eula/index.html)).

## Benchmarks

N/A

## Job Submission Example

Like other jobs on ICHEC systems, CUDA Toolkit jobs must be submitted
using a Slurm submission script. The following is an example Slurm
submission script for allocating 1 node of Kay (40 cores) for 30
minutes, then running a CUDA-compiled tutorial program matmul, which
multiplies large matrices using gpu acceleration.  Since CUDA takes
advantage only of gpus, all CUDA jobs must be submitted to the GpuQ.

Load the desired version of the toolkit module:

```bash
version=11.4
module load cuda/$version
```

Following the ICHEC [tutorial](https://www.ichec.ie/academic/national-hpc/documentation/tutorials/compiling-program-cuda),
we compile the CUDA source file matmul.cu using nvcc as follows:

```bash
nvcc matmul.cu -o matmul -arch=sm_70 -O3
```

Create the submission script (and name it myjob.sh) for the SLURM Workload Manager and modify it with your parameters

```bash
#!/bin/sh
#SBATCH -p GpuQ
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
version=11.4
module load cuda/$version

./matmul 10000 
```

Submit the job with the following command

```bash
sbatch myjob.sh
```

## Additional Notes

Further information can be obtained from the CUDA Toolkit [website](https://developer.nvidia.com/cuda-toolkit).

