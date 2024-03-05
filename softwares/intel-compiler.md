# Intel Compiler

```{admonition} Versions Installed
:class: note

`Kay: 2017u8 / 2019 / 2019u3 / 2019u5 / 2018u4 / 2019u1 / 2019u4 / 2020u4`

`LXP: `

```

## Description

The Intel compiler icc/icpc/ifortran is the flagship C/C++/Fortran compiler from Intel.

## License

The Intel compiler license is proprietary and ICHEC have a license for all the installed versions.

## Benchmarks

N/A.

## Job Submission Example on Kay

The following example shows how to compile a simple C++ 'Hello world'-style program and run it on a compute node on Kay.

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

We save this in the C++ file named helloworld.cpp.  The program is compiled as follows:
```bash
-bash-4.2$ module load intel/2020u4
-bash-4.2$ icpc helloworld.cpp -o helloworld -O3
```

This outputs an executable file called helloworld.  Here we have shown how to compile on the login node (i.e. at the command prompt when logged in to Kay), but be aware for very intensive compilations you should compile in a script and submit a job for this.  However, for most
situations it is fine to compile on the login node.  Next, we show a script that can be used to run the program on Kay, on a single node.

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

module load intel/2020u4

./helloworld
```

## Notes

Some of the installed versions have known (Intel) bugs.  In general you should aim to use the latest installed version, or at least the latest installed version for a given year, as this will have no known bugs.

Further information on the Intel software suites can be obtained
[here.](https://software.intel.com/content/www/us/en/develop/home.html) 

