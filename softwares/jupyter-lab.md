# JupyterLab

```{admonition} Versions Installed
:class: note

`LXP: 4.0.5`
```

## Description

JupyterLab is the a web-based interactive development environment for notebooks, code, and data. Its flexible interface allows users to configure and arrange workflows in data science, scientific computing and machine learning.

## Running Jupyter Notebooks on MeluXina

LuxProvide offers JupyterLab as SaaS on the MeluXina Cloud, with native Python support and capability for custom Jupyter kernels.

JupyterLab can be accessed [here](https://jlab.lxp-prod.cloud.lxp.lu). You can refer to the MeluXina documentation page for JupyterLab for additional info [here](https://docs.lxp.lu/cloud/jlab/jlab/).

## Detailed steps

1. The first step before requesting a job on the MeluXina Cloud page is to upload the notebook(s) you wish to run to MeluXina.

2. The second step is to set up a Python virtual environment(s) on MeluXina for you to use as your Python kernel for the notebook(s).

    You can do this by requesting an interactive job via:
    ```bash
    $ salloc -A <project_id> -t <time> --qos=dev --res cpudev -p cpu -N 1
    ```
    Now load your desired version of Python (here we just use the default version of the MeluXina 2023.1 software stack, Python 3.11.3):
    ```bash
    $ module load Python
    ```
    ```{note}
    The Python version of the Python kernel will be the same as the Python version used to create the environment, and this cannot be changed. If you require a specific Python version, make sure to load the correct version. If it is a version older than 3.10.8 you will have to load older    MeluXina software stacks before you are able to load them.
    ```
    Suppose you want to create an environment called *my_env* and you want to download numpy, scipy and matplotlib. 
    
    First, create a directory to store your virtual environments. I will create one called *venvs* in my home directory:
    ```bash
    $ mkdir ~/venvs
    ```
    Then create your environment:
    ```bash
    python -m venv my_env 
    ```
    Then activate it:
    ```bash
    $ source ~/venvs/my_env/bin/activate
    ```
    Your environment will now be activated and you will see *(my_env)* preceding your username. The first thing to do whenever you create a new environment is to upgrade *pip*:
    ```bash
    (my_env) $ python -m pip install --upgrade pip
    ```
    And now I can install the desired packages as follows:
    ```bash
    (my_env) $ python -m pip install numpy scipy matplotlib
    ```

3. Still inside your interactive job session, and with your environment still activated, you must install the *ipykernel* package in your environment - without this package, the environment cannot be used by JupyterLab as a python kernel.
```bash
(my_env) $ python -m pip install ipykernel
```

4. Still inside your interactive job session, and with your environment still activated, you must register your environment as a Jupyter kernel - else, your environment will not be listed as an avaiable kernel later in your JupyterLab session.
```bash
(my_env) $ python -m ipykernel install --name my_env --display-name "my_env" --user
``` 
At this point, you can exit your interactive session via
```bash
(my_env) $ exit
```
unless there are any pther packages you wish to install, although you can also do this at a later time.

Now you are ready to start a JupyterLab session and run your notebooks.

5. Following MeluXina instructions, request a session via the MeluXina cloud. Once your job begins, the page will take you to an online Jupyter Lab session, where your notebooks and any Python environments that have been registered as kernels will be available.

```{note}
If you have troubles with the MeluXina cloud, we have a script that allows you to start a JupyterLab session on your browser and guides you through the instructions to achieve this. If you need this script, please request it by opening a ticket with us at [support@ichec.ie](mailto:suport@ichec.ie).
```