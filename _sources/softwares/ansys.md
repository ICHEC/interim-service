# ANSYS - CFX, Fluent, Mechanical

```{admonition} Versions Installed
:class: note

`Kay: 19.2 / 2019R3 / 2020R1 / 2021R1`

`LXP: `

```

## Description

Ansys suite of software provides multi-disciplinary modelling and simulation tools. It includes popular solvers such as Fluent, CFX. More information can be found [here](https://www.ansys.com/products).

## License

In order to use any Ansys software a user must contact the [Helpdesk](https://rt.ichec.ie) and request to be added in the respective user group.

## Benchmarks

N/A.

## CFX Job Submission Example

Like other jobs on ICHEC systems, CFX jobs must be submitted using a Slurm submission script. The following is an example Slurm submission script for running a CFX job on 2 nodes for 1 hour wall time (the CFX definition file is called `test.def`):

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
#SBATCH -N 2
#SBATCH -t 1:00:00
#SBATCH --job-name=myjobname

# Charge job to myproject
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myemailaddress@universityname.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

#Create a list of available nodes for the CFX executable:
hostnames=`scontrol show hostnames $SLURM_JOB_NODELIST`
hostnames=`echo $hostnames | sed -e 's/ /,/g'`

#Load the ansys module - CFX is then accessible
version=19.2
module load ansys/$version

#Partition + Solve:
cfx5solve -def test.def -par-dist $hostnames -start-method 'HP MPI Distributed Parallel'
```

This job can be submitted using the command

```bash
sbatch scriptname.sh
```

where `scriptname.sh` is the filename of the sample Slurm submission script.


## Fluent Job Submission Example

Like other jobs on ICHEC systems, Fluent jobs must be submitted using a Slurm submission script. The Slurm submission script should launch the Fluent executable with the Graphical User Interface (GUI) disabled. This can be achieved by specifying the `-g` argument on the command line. When the GUI is disabled, Fluent commands can be issued using the Fluent Text User Interface (TUI). A series of TUI commands can be saved to a text file, which can subsequently read by the Fluent solver using the `-i` command line argument. The following is a minimal example Slurm submission script for running a steady-state 3D Fluent job on 2 nodes for a wall time of 1 hour (the Fluent case file is called "example.cas.gz"):

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
#SBATCH -N 2
#SBATCH -t 1:00:00
#SBATCH --job-name=myjobname

# Charge job to myproject
#SBATCH -A myproject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=me@mydom.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

#Load the ansys module - Fluent is then accessible
version=19.2
module load ansys/$version

# Load intel module for using the Intel MPI libraries
module load intel

# Get hostnames of the allocated nodes
scontrol show hostnames $SLURM_JOB_NODELIST > hostNamesFile.txt

#Run the fluent executable:
fluent 3ddp -t80 -cnf=hostNamesFile.txt -g -i fluentCommandsFile.txt -platform=intel -mpi=intel
```

The following is a summary of Fluent command line parameters used in the above Slurm submission script:

| parameters                  | Description                                                                  |
|:---------------------------:|:-----------------------------------------------------------------------------|
| `3ddp`                      | Run a 3D simulation in double precision (remove dp for single precision).    |
| `-t80`                      | Use 80 cores (i.e. 2 nodes of 40 cores each)                                 |
| `-cnf=hostNamesFile.txt`    | Provides the Fluent solver with the list of nodes allocated to the Slurm job |
| `-g`                        | Run Fluent without the GUI                                                   |
| `-i fluentCommandsFile.txt` | Read Fluent commands from fluentCommandsFile.txt [^cmd].                     |
| `-platform=intel`           | Use the Fluent executable optimized for Intel processors                     |
| `-mpi=intel`                | Use the Intel MPI for communication among Fluent processes                   |

[^cmd]: This is a plain text file containing the TUI commands that will be executed by the Fluent solver.

For this example, fluentCommandsFile.txt contains the following Fluent commands (comments in this file begin with a semicolon `;`):

```ansys
; Read the Fluent case file
/file/read-case/ example.cas.gz
; Initialise the flow field
/solve/initialize/initialize-flow
; Run the solver for 200 iterations
/solve/iterate 200
; Write the results to a data file
/file/write-data example.dat
; Exit Fluent
/exit yes
```

This job can be submitted using the command

```bash
sbatch scriptname.sh
```
where scriptname.sh is the filename of the sample Slurm script.

## Mechanical Job Submission Example

Like other jobs on ICHEC systems, Ansys Mechanical jobs must be submitted using a Slurm submission script. The following is an example Slurm submission script for running a Ansys Mechanical job on 1 node for 1 hour wall time (the input file is `./myinput.inp`):

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
#SBATCH --partition=ProdQ
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=40
#SBATCH --time=1:00:00
#SBATCH --job-name=myjobname

# Charge job to myproject
#SBATCH --account=myproject

# Write stdout+stderr to file
#SBATCH --output=log_slurm.txt

# Mail me on job start & end
#SBATCH --mail-user=me@mydom.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

#Load the ansys module - Ansys Mechanical is then accessible
version=19.2
module load ansys/$version

# Get hostnames of the allocated nodes
MYMACHINES=$(srun hostname | sort | uniq -c | \awk '{print $2 ":" $1}' | \paste -s -d ":" -)

# Run Ansys MAPDL
mapdl -dis -mpi INTELMPI \
      -machines $MYMACHINES \
      -j "file" \
      -s noread \
      -b list \
      -i ./myinput.inp \
      -o ./file.out
```

This job can be submitted using the command

```bash
sbatch scriptname.sh
```
where `scriptname.sh` is the filename of the sample Slurm submission script.
