(slurm-workload-manager)=
# Slurm Workload Manager

## Typical Cluster overview

A typical layout of any HPC system looks like following -

```{mermaid}
:align: center
graph LR
login[(Login node)]

subgraph CPU
direction LR
c1
c2
c3
c4
c5["..."]
c1 <--> c2 <--> c3 <--> c4 <--> c5
end

subgraph GPU
direction LR
g1
g2
g3
g4
g5["..."]
g1 <--> g2 <--> g3 <--> g4 <--> g5
end

subgraph LargeMem
direction LR
m1
m2
m3
m4
m5["..."]
m1 <--> m2 <--> m3 <--> m4 <--> m5
end
c1 <--> g1 <--> m1
c2 <--> g2 <--> m2
c3 <--> g3 <--> m3
c4 <--> g4 <--> m4
c5 <--> g5 <--> m5
login --"ssh/slurm
access"--> CPU & GPU & LargeMem
```

There is a **login node** which you `ssh` to. Then there are a number of what we call computational nodes, shown in the figure above in groups as CPU, GPU and LargeMem. The dual arrows indicate high speed network connection between nodes.

- **CPU**: Typically, CPU nodes are standard or default machines with a certain number of server grade cores available, and relatively 1-2GB RAM per core. These are the machines that are used largely for CPU based computations, with parallelism implemented through either OpenMP or MPI.
- **GPU**: These nodes are similar to CPU, as they have similar number of CPU cores (sometimes lower) as CPU nodes, but in addition they usually have at least 1 high performance GPU cards, though in practice 2 or more. One uses these to run programs that can leverage parallization of GPUs. Usually programs with large parallel loops can be accelerated very well on GPUs, so that their wall time can be upto 20-100 times shorter than when run on CPUs using MPI/OpenMP.
- **LargeMem**: These are nodes configured to address usecases or programs that require unusually high RAM to run. They can be of either type CPU/GPU in terms of compute capability, however they have an order of magnitude larger RAM than usual machines. On Meluxina, for example CPU/GPU nodes have 512GB RAM per node, but large memory nodes have 4TB RAM per node.


## SLURM Overview
The standard usage model for a HPC cluster is that you log into a front-end server or web portal and from there launch applications to run on one of more back-end servers. The software tool which manages this is called a workload manager or batch scheduler. Most HPC systems give direct user access only on login node, from where you delegate/run your computation/simulation to compute nodes.

HPC systems are essentially multi-user environments, where several users asynchronously and frequently login and run their codes. It is the scheduler or the workload manager, that monitors which compute nodes are free to use, and the ones that are occuppied running code, how long will they be in that state. It monitors the workload, and assigns to work submitted by the user to idle nodes. The scheduler used on Kay and Meluxina both, and widely used in HPC systems is [Slurm](https://slurm.schedmd.com/) workload manager.

SLURM provides command line tools to launch your code to appropriate compute nodes, monitor their progress, stop or manipulate the running codes in a number of ways. We look into some of those aspect below.

## Basic Usage

There are two modes a user can run a code on pretty much any HPC system on the planet, as illustrated in the flowchart below, the **Interactive** mode, and **Batch** mode.

```{mermaid}
graph LR
subgraph Interactive
direction LR
login["Login Node"] --"Allocate Compute
node & ssh to it"--> comp(["Compute node"]) --> run((("Execute code"))) -->done(("Done"))
end

subgraph Batch
direction LR
login1["Login Node"] --"Prepare job script
and submit to slurm"--> comp1(["Compute node"]) --> run1((("slurm runs
the code"))) -->done1(("Done"))
end

desk[("Local machine")] --"ssh to
login node"--> Batch & Interactive
```





The typical way a user will interact with compute resources managed by a workload manager is as follows:

- Write a job script which describes the resources required (e.g how many CPUs and for how long), instructions such as where to print standard out and error, and the commands to run once the job starts.

- Submit the job to the workload manager which will then start the job once the requested resources are available.

- Once the job completes, the user will see all results as well as output that would normally appear on screen in previously specified files.

The two types of job commonly used are:

- **Interactive** : Request a set of nodes to run an interactive bash shell on. This is useful for quick tests and development work. These type of jobs should only be used with the with resource requested appropriately.

In Kay, we had a specific partition called `DevQ` queue, restricted with maximum wall time of 1 hour. For example, the following command will submit an interactive job requesting 1 node for 1 hour to be charged to myproj_id:

On Kay:

```bash
salloc -p DevQ -N 1 -A myproj_id -t 1:00:00
```

The similar command for Meluxina will be 
On Meluxina:
```bash
salloc -p cpu -q test -N 1 -A myproj_id -t 1:00:00
```

- **Batch** : A script is submitted for later execution whenever the requested resources are available. Both within this script and on the commandline when submitting the job, a set of constraints, required information and instructions are given. The file must be a shell script (i.e start with `#!/bin/sh`) and Slurm directives must be preceeded by `#SBATCH`. A sample script is displayed below which request 4 nodes (each with 40 cores) for 48 hours to run an MPI application and could be submitted using the command:

```bash
sbatch mybatchjob.sh
```

Where the file `mybatchjob.sh` looks like -

```bash
#!/bin/sh 

#SBATCH --time=00:20:00
#SBATCH --nodes=4
#SBATCH -A myproj_id

module load intel/2019


mpirun -np 80 ./a.out
```

(slurm-commands)=
# Slurm Commands

``````{admonition} Slurm informational command summary
:class: note

- `sinfo`: It lists all partition/queues and limits. Run `man sinfo` for more details about the command and further arguments.

- `squeue`: It lists all queued jobs. Run `man squeue` for more details about the command and further arguments, such as 
    - `squeue -u $USER` prints jobs by the $USER.
    - `squeue -j jobid` shows info about a particular job with job-id `jobid`.
    - `squeue --start` shows estimated start time of the job.
    - `squeue -A myproj_id` lists all jobs using specific account.
- `mybalance`: Lists summary of core hour balances of all of the users's account.
``````


``````{admonition} Slurm job commands
:class: tip
Below is a table of some of the common slurm commands used in running jobs.
``````

```{table}
|Command | 	Description| 	Example|
|:---:   | :---:        |:---:      |
|sbatch  | Submit job script| `sbatch myjob.sh` |
|  	     | submit script to use 5 nodes| `sbatch -N 5 myjob.sh`|
|  	     | submit job with dependency on successful completion of other jobs|`sbatch -d afterok:job_id[:jobid...] myjob.sh`
|scancel | Cancel job | `scancel <jobid>`|
|sattach | Attach terminal to standard output of running job (job step 0)|`sattach <jobid>.0`|
|scontrol| Prevent a queued job from running |`scontrol hold <jobid>`|
|  	     | release a job hold | `scontrol release <jobid>`|
|  	     | display detailed info about specific job| `scontrol show jobid <jobid>`|
|srun 	 | Run a parallel job (mostly within an allocation created with a job script)||
|  	     | run a 2 node interactive job for 30 minutes| `srun -N 2 -A myproj_id -t 00:30:00 -p DevQ --pty bash`|
|  	     | run an MPI application within a Slurm submit script (using all cores allocated on all nodes)| `srun -n $[$SLURM_JOB_NUM_NODES * 40] ./my_mpi_app`|
|  	     | run a Hybrid MPI/OpenMP application using 1 MPI process per node | `srun -n $SLURM_JOB_NUM_NODES --ntasks-per-node=1 ./my_hybrid_mpi_app`|
|  	     | run a command on a job already running. e.g. to find out the CPU/Memory usage |`srun --jobid <jobid> ps u`|
```


## Further Information

For detailed understanding of Slurm, please see the official website of [Slurm](https://slurm.schedmd.com/).
