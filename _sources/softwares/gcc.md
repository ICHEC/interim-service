# gcc: Gnu C/C++ compiler

```{admonition} Versions Installed
:class: note

`Kay: 8.2.0, 9.4.0`

`LXP: 12.3`

```

## Description

gcc is the flagship c/c++ compiler from Gnu.

## License

gcc is licensed to the public under the terms of the GNU Public License (GPL).

## Benchmarks

N/A.

## Job Submission Example on Kay

The following example shows how to compile a simple C++ 'Hello world' style program and run it on a compute node on Kay.

The program listing is simply the following:
```c++
#include <iostream>

using std::cout;
using std::endl;

int main(int argc, char** argv)
{
    cout << "Hello world!" << endl;

    return 0;
}
```

We save this in the C++ file named `helloworld.cpp`.  The program is compiled as follows:
```bash
-bash-4.2$ module load gcc/9.4.0
-bash-4.2$ g++ helloworld.cpp -o helloworld -O3
```

This outputs an executable file called helloworld.  Here we have shown how to compile on the login node (i.e. at the command prompt when logged in to Kay), but be aware for very intensive compilations you should compile in a script and submit a job for this.  However, for most
situations it is fine to compile on the login node.  Next, we show a script that can be used to run the program on Kay, on a single node.

## Job submission example

### On Kay

```bash
#!/bin/bash -l
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
#SBATCH -t 00:05:00
#SBATCH --job-name=gccrun

# Charge job to myproject
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load gcc/9.4.0

./helloworld
```

### On Meluxina

```bash
#!/bin/bash -l
# Slurm flags
#SBATCH -p cpu
#SBATCH --qos default
#SBATCH --hint=nomultithread
#SBATCH -N 1
#SBATCH -t 00:05:00
#SBATCH --job-name=gccrun

# Charge job to myproject
#SBATCH -A MyProject

# Write stdout+stderr to file
#SBATCH -o output.txt

# Mail me on job start & end
#SBATCH --mail-user=myEmail@domain.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load gcc/12.3.0

./helloworld
```
 

## Notes

The above was a sample case, which shows only minimalistic features of the compiler, and does not do any justice to it's real capabilities, such as optimization of the code. Further information on gcc can be obtained [here.](https://gcc.gnu.org/) 

