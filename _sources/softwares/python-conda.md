# Python/Conda

```{admonition} Versions Installed
:class: note

Kay: `2.7.5 (System), 2.7.15 (Conda), 3.7.0 (Conda)`

LXP: `2.7 (System), 3.6 (System), 3.8 (System), 3.10 (module), 3.11 (module)`

Note: Here system indicates usual path in `/usr/bin/`, module indicates that it can be loaded from available modules.
```


## Description

Python is one of the most widely used language of modern time due to it's ease of use and rich ecosystem of libraries in areas ranging from traditional physics, chemistry, computational biology to datascience, machine learning and quantum computing. It has also started replacing the bash scripts in linux distributions over the years, and as result every HPC cluster has a few versions of python installed at system level.

## License

Available under Python Software Foundation (PSF) License.

## Python on Kay

On Kay, we provide the Python interpreters and packages using two methods:

### 1. System Install (Python 2 Only)

It provides the default Python interpreter on Kay, which only supports
Python 2.

### 2. Conda (Python 2 and 3)

[Conda](https://conda.io/docs/) is our preferred method to provide Python 2 and 3 interpreters, and some commonly used packages to users. You can use these by loading the Conda module and then activating the desired Conda environment.


### Useful Conda Commands

``````{dropdown} Click to expand for Conda Commands
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
``````

### Installing Python Packages

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

### Jupyter Notebooks

To use Jupyter Notebooks on Kay, refer to our documentation [here](/academic/national-hpc/documentation/tutorials/using-jupyter-notebook-kay-jupyter-hub)


## Python on Meluxina

On Meluxina, we have 2.7, 3.6, and 3.8 versions of python available at system level. Also, 3.10 and 3.11 can be used by loading modules:

- For 3.10
```bash
module load Python/3.10.8-GCCcore-12.3.0
```
- For 3.11
```bash
module load Python/3.11.3-GCCcore-12.3.0
```

On Meluxina, it is discouraged creating large number of files, hence the quota on number of files created on each users/projects. As a result they do not recommend using Conda, and also do not support Conda.

There are two alternatives ICHEC users can follow:

### Using venv environments

Python usually comes with built-in module called `venv` that can create a virtual environment with `pip` installed within it, so that user can install further packages via `pip` in the evironment.

```bash
python3 -m venv /path/to/env
```

The above creates a virtual environment in the path provided, which is essentially a folder with file `pyvenv.cfg` and folders `bin  include  lib  lib64  pyvenv.cfg`.

For general management, it's a good idea to create environments 1. in the same place, or 2. inside folder where most of your source code is. Say, you create a folder called `venvs` in your `$HOME` or `$PROJECT` folder, and create environments using the above command.

```bash
cd $HOME/venvs # create this folder if it doesn't exist using mkdir
python3 -m venv tf
```

The above creates a virtual enviroment in `$HOME/venvs/tf`. Now there will be a file `$HOME/venvs/tf/bin/activate`, which is used to activate the environment by sourcing it.

```bash
source $HOME/venvs/tf/bin/activate
```

Once activated, `which python` and `which pip` will point to `$HOME/venvs/tf/bin/python` and `$HOME/venvs/tf/bin/pip` respectively, and anything you install using pip will be installed in the environment.

Once you are done using it, you can just deactivate the environment by `deactivate` command.

In order to delete the environment, simply delete the environment folder `$HOME/venvs/tf/`.

### Using micromamba

The `venv` approach is fast, lightweight and simple. However, it has two limitations.

- The python version in the environment is tied to the python interpeter that created it.
- You can only use pip to install packages, and hence only python packages.

Conda is usually popular alternative, as its a package manager for python as well as non-python packages, and has systematic commands to create and manage environments. However it tends to create lot's of files, so not a good choice for meluxina.

A slightly better alternative that works like conda is [micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html). It comes as single binary file from [here](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html), which you can put in your `$PATH`, such as `$HOME/bin`. Then you can use the micromamba similar to conda.

```bash
$ micromamba --help

Subcommands:
  shell                       Generate shell init scripts
  create                      Create new environment
  install                     Install packages in active environment
  update                      Update packages in active environment
  repoquery                   Find and analyze packages in active environment or channels
  remove                      Remove packages from active environment
  list                        List packages in active environment
  package                     Extract a package or bundle files into an archive
  clean                       Clean package cache
  config                      Configuration of micromamba
  info                        Information about micromamba
  constructor                 Commands to support using micromamba in constructor
  env                         List environments
  activate                    Activate an environment
  run                         Run an executable in an environment
  ps                          Show, inspect or kill running processes
  auth                        Login or logout of a given host
  search                      Find packages in active environment or channels
```

## Additional Information

For more information see [here](http://www.python.org). 

