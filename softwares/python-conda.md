# Python/Conda

```{admonition} Versions Installed
class: note

`Kay: 2.7.5 (System Install) / 2.7.15 (Conda) / 3.7.0 (Conda)`

`LXP: `

```


## Description

On Kay, we provide the Python interpreters and packages using two methods:

### 1. System Install (Python 2 Only)

It provides the default Python interpreter on Kay, which only supports
Python 2.

### 2. Conda (Python 2 and 3)

[Conda](https://conda.io/docs/) is our preferred method to provide Python 2 and 3 interpreters, and some commonly used packages to users. You can use these by loading the Conda module and then activating the desired Conda environment.

## License

Available under Python Software Foundation (PSF) License.

## Useful Commands

To load the environment module:

```bash
module load conda/2
```

To list the available Conda environments:

```bash
conda info --envs
```

The *base* environment provides Python 2 interpreter, while the *python3* Conda environment provides Python 3 interpreter. Both the Conda environments provide the following packages:

- matplotlib
- numpy
- opencv
- pandas
- scikit-learn
- scipy

To activate the base (default) Conda environment:

```bash
source activate
```

To activate any other Conda environment from the list of available environments:

```bash
# Activates python3 Conda environment
source activate python3
```

To list the software installed in the Conda environment:

```bash
# Lists all software installed in the python3 Conda environment
conda list --name python3
```

To deactivate the Conda environment:

```bash
source deactivate
```

## Installing Python Packages

To install any Python package or to use a different version of Python,
you can create a new Conda environment. Your Conda environments are
saved in your *$HOME* directory.

To create a new Conda environment:

```bash
# Creates a new Conda environment called myenv with Python (version 3.4)
# and package Biopython (default: latest version for python 3.4)
conda create --name myenv python=3.4 biopython
```

Since only one Conda environment can be activated at a time, mention all the python packages you want to use together when you create the environment.

To delete your Conda environment:

```bash
conda env remove --name myenv
```

## Jupyter Notebooks

To use Jupyter Notebooks on Kay, refer to our documentation [here](/academic/national-hpc/documentation/tutorials/using-jupyter-notebook-kay-jupyter-hub)

## Additional Notes

For more information see [here](http://www.python.org). 

