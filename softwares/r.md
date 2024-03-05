# R programming

```{admonition} Versions Installed
:class: note

`Kay: 3.4.4 / 3.5.1`

`LXP: `

```

## Description

R is a language and environment for statistical computing and graphics. It provides a wide variety of statistical (linear and nonlinear modelling, classical statistical tests, time-series analysis,
classification, clustering, ...) and graphical techniques, and is highly extensible.

## License

R is free software distributed under a [GNU-style copyleft](http://www.r-project.org/COPYING).

## Benchmarks

N/A.

## Additional Notes

#### Job Submission example on Kay

```bash
#!/bin/sh

#SBATCH --partition=ProdQ
#SBATCH --nodes=1
#SBATCH --time=00:20:00
#SBATCH --job-name=myjobname
#SBATCH --account=myprojectname
#SBATCH --output=output.txt
#SBATCH --mail-user=myemailaddress@universityname.ie
#SBATCH --mail-type=BEGIN,END

cd $SLURM_SUBMIT_DIR

module load r/3.5.1
Rscript ./script.r
```

#### Example script.R

```r
XX <- rnorm(10000,10.0,2.0)
XX[500]
save(XX,file='Ex.Rdata')
```

Further information can be obtained at [The R Project for Statistical Computing](http://www.r-project.org/ "R homepage").

