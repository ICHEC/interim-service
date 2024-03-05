# ORCA


```{admonition} Versions Installed
:class: note

`Kay: 5.0.0 / 5.0.2 / 5.0.3`

`LXP: `

```

## Description

**ORCA** is an ab initio quantum chemistry program package that contains
modern electronic structure methods including density functional theory,
many-body perturbation, coupled cluster, multireference methods, and
semi-empirical quantum chemistry methods. Its main field of application
is larger molecules, transition metal complexes, and their spectroscopic
properties. ORCA is developed in the research group of Frank Neese.

## License

ORCA, Academic (Computer Center).

## Benchmarks

N/A

## Job Submission Example

Like other jobs on ICHEC systems, ORCA jobs must be submitted using a
Slurm submission script. The following is an example Slurm submission
script for allocating 1 node of Kay (40 cores) for 24h , then running
ORCA on an example input file.  Jobs that use ORCA would typically be
submitted to the ProdQ.

The ORCA module is loaded as follows (this is a key part of the sbatch
script):
```bash
module load orca/5.0.3
```

Create the submission script (and name it orca\_calc.sh) for the SLURM
Workload Manager and modify it with your parameters

```bash
#!/bin/bash

#SBATCH -p ProdQ
#SBATCH -N 1
#SBATCH -t 24:00:00
#SBATCH --job-name=test
#SBATCH -A yourproject
#SBATCH -o test.stdout
#SBATCH -e test.stderr

module load orca/5.0.3

# Location of the local scratch.

scratchlocation=/scratch/local 

# Usage:
#sbatch -J jobname orca_calc.sh -where jobname is the name of your ORCA inputfile (jobname.inp) without the .inp extension


# Set jobname here manually or use as first argument when doing sbatch -J argument job-orca.sh -N argument where "argument" becomes $SLURM_JOBNAME
export job=$SLURM_JOB_NAME
export job=$(basename $job .inp)

echo "SLURM_NODELIST is $SLURM_NODELIST"

#Create scratch

if [ ! -d $scratchlocation/$USER ]
then
  mkdir -p $scratchlocation/$USER
fi
tdir=$(mktemp -d $scratchlocation/$USER/orcajob__$SLURM_JOBID-XXXX)
chmod +xr $tdir

if [ ! -d "$tdir" ]; then
echo "Scratch dir  does not exist on this node"
echo "Maybe because scratchlocation $scratchlocation does not exist on node??"
echo "Or because permissions did not allow creation of folder?"
echo "Exiting..."
exit
fi

# Copy only the necessary stuff in submit directory to scratch directory.
#Explicit files here instead of general

#Copying submitted inputfile

cp $SLURM_SUBMIT_DIR/$job.inp $tdir/
cp $SLURM_SUBMIT_DIR/*.xyz $tdir/

#Copying possible basis file

cp $SLURM_SUBMIT_DIR/*.basis $tdir/

#Copying xyzfile if referenced in inputfile

xyzfilename=`grep -i xyzfile $SLURM_SUBMIT_DIR/$job.inp | tr ' ' '\n' | tail -2 | grep .xyz`
cp $SLURM_SUBMIT_DIR/$xyzfilename $tdir/

#Copying GBWfile with same name as inputfile and GBW/LOC/MP2NAT if part of %moinp statement

cp $SLURM_SUBMIT_DIR/$job.gbw $tdir/
cp $SLURM_SUBMIT_DIR/*im*.gbw $tdir/

grep -i "%moinp" $SLURM_SUBMIT_DIR/$job.inp
grep -i "%moinp" $SLURM_SUBMIT_DIR/$job.inp | awk '{print $2}'
grep -i "%moinp" $SLURM_SUBMIT_DIR/$job.inp | awk '{print $2}' | tr -d '"'
gbwfilefrommoinp=`grep -i "%moinp" $SLURM_SUBMIT_DIR/$job.inp | awk '{print $2}' | tr -d '"'`
cp $SLURM_SUBMIT_DIR/$gbwfilefrommoinp $tdir/

# Hess file if found in such command

prevhessfile=`grep -i 'InHessName' $SLURM_SUBMIT_DIR/$job.inp | awk '{print $2}' | tr -d '"'`
cp $SLURM_SUBMIT_DIR/$job.*hess $tdir/
cp $SLURM_SUBMIT_DIR/$prevhessfile $tdir/
cp $SLURM_SUBMIT_DIR/*.hess $tdir/

#cp $SLURM_SUBMIT_DIR/*.inp $tdir/
#cp $SLURM_SUBMIT_DIR/*.gbw $tdir/
#cp $SLURM_SUBMIT_DIR/*.xyz $tdir/
#cp $SLURM_SUBMIT_DIR/*.loc $tdir/
#cp $SLURM_SUBMIT_DIR/*.qro $tdir/
#cp $SLURM_SUBMIT_DIR/*.hess $tdir/


echo ${SLURM_NODELIST} > $tdir/$job.nodes

# cd to scratch
cd $tdir
ls

which mpirun
#Start ORCA job. ORCA is started using full pathname (necessary for parallel). Output file is written directly to submit directory

$orcadir/orca $job.inp  >> $SLURM_SUBMIT_DIR/$job.out

# ORCA has finished. Now copy important stuff back (xyz files, GBW files etc.). Add files here as required

cp $tdir/*.gbw $SLURM_SUBMIT_DIR
cp $tdir/*.engrad $SLURM_SUBMIT_DIR
cp $tdir/*.xyz $SLURM_SUBMIT_DIR
cp $tdir/*.trj $SLURM_SUBMIT_DIR
cp $tdir/*.loc $SLURM_SUBMIT_DIR
cp $tdir/*.qro $SLURM_SUBMIT_DIR
cp $tdir/*.uno $SLURM_SUBMIT_DIR
cp $tdir/*.unso $SLURM_SUBMIT_DIR
cp $tdir/*.uco $SLURM_SUBMIT_DIR
cp $tdir/*.hess $SLURM_SUBMIT_DIR
cp $tdir/*.cis $SLURM_SUBMIT_DIR
cp $tdir/*.dat $SLURM_SUBMIT_DIR
cp $tdir/*.mp2nat $SLURM_SUBMIT_DIR
cp $tdir/*.nat $SLURM_SUBMIT_DIR
cp $tdir/*.scfp_fod $SLURM_SUBMIT_DIR
cp $tdir/*.scfp $SLURM_SUBMIT_DIR
cp $tdir/*.scfr $SLURM_SUBMIT_DIR
cp $tdir/*.nbo $SLURM_SUBMIT_DIR
cp $tdir/FILE.47 $SLURM_SUBMIT_DIR
cp $tdir/*_property.txt $SLURM_SUBMIT_DIR
cp $tdir/*.allxyz $SLURM_SUBMIT_DIR
cp $tdir/*.log $SLURM_SUBMIT_DIR
cp $tdir/*.interp $SLURM_SUBMIT_DIR
cp $tdir/*spin* $SLURM_SUBMIT_DIR
cp $tdir/*lastscf* $SLURM_SUBMIT_DIR
cp $tdir/*.spectrum $SLURM_SUBMIT_DIR

rm -rf $tdir
```

Submit the job with the following command

```bash
sbatch -J jobname orca_calc.sh 
```

## Additional Notes

Further information can be obtained from the [ORCA Forum](https://orcaforum.kofo.mpg.de/).

