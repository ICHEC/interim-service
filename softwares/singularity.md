# Singularity

## 


```{admonition} Versions Installed
class: note

`Kay: 2.6.0`

`LXP: `

```

## Description

Singularity enable users to use containers on HPC systems such as Kay.
Using singularity you can make complicated software stacks portable. For more information about singularity refer [here](https://sylabs.io/guides/2.6/user-guide/index.html)

### Workflow

Singularity provide multiple workflows for building, deploying and using
containers. In the following text, we have presented a generic workflow
suitable to most users.

In this workflow you should build singularity images on your local
computer (where you have sudo rights) and then copy the singularity
images to Kay to run your simulations. To install singularity on your
local computer refer [here](https://sylabs.io/guides/2.6/user-guide/installation.html)

Some examples are given below

#### Examples

#### 1. Serial code

**On Local Computer**: Create a singularity definition file (e.g. serial.def) with the contents

```Singularity
BootStrap: docker
From: centos:7

%environment
    LC_ALL="en_US.UTF-8"
    LC_CTYPE="en_US.UTF-8"
    LANGUAGE="en_US.UTF-8"
    export LC_ALL LC_CTYPE LANGUAGE

%post
    yum -y update
    yum -y install epel-release
    yum repolist
    yum -y install cowsay
```
 

Create the singularity image (e.g. serial.simg) from the singularity
definition file (serial.def), using the command

```bash
sudo singularity build serial.simg serial.def
```

Copy the singularity image (serial.simg) to Kay (e.g. home directory)
 

**On Kay**

In the same directory as the singularity image (e.g. home directory),
create a Slurm submission file (e.g. submit_serial.sh) with the
contents

```bash
#!/bin/sh

#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --account=MY_PROJECT_ID
#SBATCH --partition=DevQ
#SBATCH --job-name=serial
#SBATCH --output=log_slurm.txt

module load singularity/2.6.0

cd $SLURM_SUBMIT_DIR
singularity exec serial.simg cowsay 'Hello!'
```

Make sure to replace the MY_PROJECT_ID with your project ID in the
slurm submission file (submit_serial.sh)

Submit a job, using the command

```bash
sbatch submit_serial.sh
```

Once the job finishes, the output (in the log_slurm.txt) will look like

```
     ________
    < Hello! >
     --------
            \   ^__^
             \  (oo)\_______
                (__)\       )\/\
                    ||----w |
                    ||     ||
-------------------/ \----/ \---
``` 


#### 2. MPI code within a single node (using container MPI)

**On Local Computer**

Create a C file (e.g. hello_world.c) with the contents

```c++
#include <mpi.h>
#include <stdio.h>
#include <utmpx.h>

int main(int argc, char** argv) {
    // Initialize the MPI environment
    MPI_Init(NULL, NULL);

    // Get the number of processes
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    // Get the rank of the process
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    // Get the name of the processor
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);

    // Get the id of the core
    int core_id;
    core_id = sched_getcpu();

    // Print off a hello world message
    printf("host=%s, size=%d, rank=%d, core=%d\n", processor_name, world_size, world_rank, core_id);

    // Finalize the MPI environment.
    MPI_Finalize();
}
```


Create a singularity definition file (e.g. mpi\_container.def) with the contents

```Singularity
BootStrap: docker
From: centos:7

%post
    yum -y update
    yum -y install openmpi3-devel
    ln -s /usr/lib64/openmpi3/bin/mpicc /usr/bin/mpicc
    ln -s /usr/lib64/openmpi3/bin/mpirun /usr/bin/mpirun

%files
    hello_world.c /var/tmp/hello_world.c

%post
    mpicc -o /usr/local/bin/hello_world /var/tmp/hello_world.c
```

Create the singularity image (e.g. mpi\_container.simg) from the
singularity definition file (mpi\_container.def), using the command

```bash
sudo singularity build mpi_container.simg mpi_container.def
```

Copy the singularity image (mpi\_container.simg) to Kay (e.g. home directory)

**On Kay**

In the same directory as the singularity image (e.g. home directory), create a Slurm submission file (e.g. submit_mpi_container.sh) with the contents

```bash
#!/bin/sh

#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --account=MY_PROJECT_ID
#SBATCH --partition=DevQ
#SBATCH --job-name=mpi_container
#SBATCH --output=log_slurm.txt

module load singularity/2.6.0

cd $SLURM_SUBMIT_DIR
singularity exec mpi_container.simg /usr/bin/mpirun -np 40 /usr/local/bin/hello_world
```

Make sure to replace the MY_PROJECT_ID with your project ID in the slurm submission file (submit_mpi_container.sh)

Submit a job, using the command

```bash
sbatch submit_mpi_container.sh
```

Once the job finishes, the output (in the log_slurm.txt) will look like

```
    host=n1, size=40, rank=10, core=2
    host=n1, size=40, rank=16, core=12
    host=n1, size=40, rank=24, core=14
    host=n1, size=40, rank=37, core=33
    host=n1, size=40, rank=38, core=11
    host=n1, size=40, rank=5, core=28
    host=n1, size=40, rank=6, core=17
    host=n1, size=40, rank=17, core=22
    host=n1, size=40, rank=20, core=15
    host=n1, size=40, rank=26, core=13
    host=n1, size=40, rank=27, core=34
    host=n1, size=40, rank=30, core=0
    host=n1, size=40, rank=36, core=3
    host=n1, size=40, rank=39, core=30
    host=n1, size=40, rank=0, core=7
    host=n1, size=40, rank=1, core=26
    host=n1, size=40, rank=2, core=19
    host=n1, size=40, rank=3, core=36
    host=n1, size=40, rank=4, core=8
    host=n1, size=40, rank=7, core=35
    host=n1, size=40, rank=8, core=18
    host=n1, size=40, rank=9, core=20
    host=n1, size=40, rank=12, core=16
    host=n1, size=40, rank=13, core=32
    host=n1, size=40, rank=14, core=5
    host=n1, size=40, rank=15, core=24
    host=n1, size=40, rank=18, core=8
    host=n1, size=40, rank=19, core=24
    host=n1, size=40, rank=21, core=23
    host=n1, size=40, rank=22, core=10
    host=n1, size=40, rank=23, core=37
    host=n1, size=40, rank=25, core=38
    host=n1, size=40, rank=28, core=17
    host=n1, size=40, rank=29, core=29
    host=n1, size=40, rank=31, core=21
    host=n1, size=40, rank=32, core=4
    host=n1, size=40, rank=33, core=36
    host=n1, size=40, rank=34, core=1
    host=n1, size=40, rank=35, core=20
    host=n1, size=40, rank=11, core=22
```


#### 3. MPI code over multiple nodes (using host and container MPI)

To run singularity containers with MPI over multiple nodes, the host MPI
and the container MPI should be compatible. To simplify the preparation
of singularity containers, you can use HPCCM on your local computer. For
more information about HPCCM refer [here](https://github.com/NVIDIA/hpc-container-maker/blob/master/docs/getting_started.md).

**On Local Computer**

Create a C file (e.g. hello\_world.c) with the contents

```c++
#include <mpi.h>
#include <stdio.h>
#include <utmpx.h>

int main(int argc, char** argv) {
    // Initialize the MPI environment
    MPI_Init(NULL, NULL);

    // Get the number of processes
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    // Get the rank of the process
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    // Get the name of the processor
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);

    // Get the id of the core
    int core_id;
    core_id = sched_getcpu();

    // Print off a hello world message
    printf("host=%s, size=%d, rank=%d, core=%d\n", processor_name, world_size, world_rank, core_id);

    // Finalize the MPI environment.
    MPI_Finalize();
}
```

Create a HPCCM recipe file (e.g. mpi\_host\_container.py) with the contents

```python
"""
MPI Bandwidth
Contents:
    CentOS 7
    GNU compilers (upstream)
    Mellanox OFED
    OpenMPI version 3.1.2
"""

Stage0 += comment(__doc__, reformat=False)

# CentOS base image
Stage0 += baseimage(image='centos:7')

# GNU compilers
Stage0 += gnu()

# Mellanox OFED
Stage0 += mlnx_ofed()

# OpenMPI
Stage0 += openmpi(configure_opts=['--with-slurm'], infiniband=False, cuda=False, version='3.1.2')

# MPI Hello World
Stage0 += copy(src='hello_world.c', dest='/var/tmp/hello_world.c')
Stage0 += shell(commands=['mpicc -o /usr/local/bin/hello_world /var/tmp/hello_world.c'])
```

Create the singularity definition file (e.g. mpi_host_container.def) from the HPCCM recipe file (mpi_host_container.py)

```bash
    hpccm --format singularity --recipe ./mpi_host_container.py --singularity-version=2.6 > mpi_host_container.def
```
 
Create the singularity image (e.g. mpi_host_container.simg) from the
singularity definition file (mpi_host_container.def), using the command

```bash
sudo singularity build mpi_host_container.simg mpi_host_container.def
```

Copy the singularity image (mpi_host_container.simg) to Kay (e.g. home directory)


**On Kay**

In the same directory as the singularity image (e.g. home directory),
create a Slurm submission file (e.g. submit_mpi_host_container.sh)
with the contents

```bash
#!/bin/sh

#SBATCH --time=01:00:00
#SBATCH --nodes=2
#SBATCH --account=MY_PROJECT_ID
#SBATCH --partition=DevQ
#SBATCH --job-name=mpi_host_container
#SBATCH --output=log_slurm.txt

module load singularity/2.6.0
module load openmpi/gcc/3.1.2

cd $SLURM_SUBMIT_DIR

mpirun -np 80 singularity exec mpi_host_container.simg /usr/local/bin/hello_world
```

Make sure to replace the MY_PROJECT_ID with your project ID in the
slurm submission file (submit_mpi_host_container.sh)


Submit a job, using the command

```bash
sbatch submit_mpi_host_container.sh
```

Once the job finishes, the output (in the log_slurm.txt) will look like

```
    host=n1, size=80, rank=6, core=5
    host=n1, size=80, rank=27, core=25
    host=n1, size=80, rank=8, core=0
    host=n1, size=80, rank=19, core=21
    host=n1, size=80, rank=24, core=11
    host=n1, size=80, rank=37, core=26
    host=n2, size=80, rank=66, core=2
    host=n2, size=80, rank=45, core=31
    host=n2, size=80, rank=47, core=28
    host=n2, size=80, rank=62, core=15
    host=n2, size=80, rank=64, core=5
    host=n2, size=80, rank=69, core=38
    host=n2, size=80, rank=77, core=30
    host=n2, size=80, rank=79, core=34
    host=n2, size=80, rank=44, core=16
    host=n2, size=80, rank=50, core=7
    host=n2, size=80, rank=53, core=27
    host=n2, size=80, rank=57, core=20
    host=n2, size=80, rank=59, core=39
    host=n2, size=80, rank=60, core=4
    host=n2, size=80, rank=71, core=37
    host=n2, size=80, rank=78, core=3
    host=n2, size=80, rank=48, core=6
    host=n2, size=80, rank=49, core=36
    host=n2, size=80, rank=51, core=35
    host=n2, size=80, rank=52, core=9
    host=n2, size=80, rank=55, core=31
    host=n2, size=80, rank=67, core=23
    host=n2, size=80, rank=73, core=33
    host=n2, size=80, rank=40, core=17
    host=n2, size=80, rank=42, core=15
    host=n2, size=80, rank=54, core=8
    host=n2, size=80, rank=56, core=0
    host=n2, size=80, rank=61, core=21
    host=n2, size=80, rank=63, core=38
    host=n2, size=80, rank=72, core=10
    host=n2, size=80, rank=74, core=12
    host=n2, size=80, rank=76, core=14
    host=n2, size=80, rank=41, core=26
    host=n2, size=80, rank=43, core=27
    host=n2, size=80, rank=46, core=9
    host=n2, size=80, rank=58, core=11
    host=n2, size=80, rank=65, core=28
    host=n2, size=80, rank=68, core=0
    host=n2, size=80, rank=70, core=19
    host=n2, size=80, rank=75, core=25
    host=n1, size=80, rank=0, core=10
    host=n1, size=80, rank=1, core=35
    host=n1, size=80, rank=2, core=12
    host=n1, size=80, rank=3, core=39
    host=n1, size=80, rank=4, core=1
    host=n1, size=80, rank=5, core=33
    host=n1, size=80, rank=7, core=37
    host=n1, size=80, rank=9, core=29
    host=n1, size=80, rank=10, core=15
    host=n1, size=80, rank=11, core=31
    host=n1, size=80, rank=12, core=19
    host=n1, size=80, rank=13, core=32
    host=n1, size=80, rank=14, core=16
    host=n1, size=80, rank=15, core=36
    host=n1, size=80, rank=16, core=6
    host=n1, size=80, rank=17, core=24
    host=n1, size=80, rank=18, core=4
    host=n1, size=80, rank=20, core=3
    host=n1, size=80, rank=21, core=23
    host=n1, size=80, rank=22, core=17
    host=n1, size=80, rank=23, core=22
    host=n1, size=80, rank=25, core=27
    host=n1, size=80, rank=26, core=11
    host=n1, size=80, rank=28, core=8
    host=n1, size=80, rank=29, core=39
    host=n1, size=80, rank=30, core=9
    host=n1, size=80, rank=31, core=33
    host=n1, size=80, rank=32, core=5
    host=n1, size=80, rank=33, core=38
    host=n1, size=80, rank=34, core=13
    host=n1, size=80, rank=35, core=38
    host=n1, size=80, rank=36, core=2
    host=n1, size=80, rank=38, core=18
    host=n1, size=80, rank=39, core=25
```

## License

Singularity is released under a standard 3 clause BSD license.

## Benchmarks

N/A.

## Additional Notes

To use singularity load the relevant environment module:

```bash
module load singularity/2.6.0
```

Further information can be found [here](https://sylabs.io/guides/2.6/user-guide/index.html).  

