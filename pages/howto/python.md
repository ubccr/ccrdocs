# Using Python at CCR

## Python and HPC

When you run python code on CCR's resources, you are using a High Performance Computing system. Our system is made up of many computing nodes with vastly different hardware resources. Compiling and running software across many different computers with different hardware configurations is a non-trivial task. Ensuring software continues to work as HPC hardware and software evolves over time is even harder.

All this is to say, what works on your local machine is not guaranteed to work on an HPC system. Assuming you can use python identically to how you'd use it on your local machine will lead to massive headaches.

## Using Python at CCR Course  

UB faculty, staff, and students have access to self-enroll in the ["Using Python at CCR"](https://ublearns.buffalo.edu/d2l/le/discovery/view/course/288741) course in UB Learns.  This is a self-paced course that steps CCR users through the proper usage of Python in CCR's HPC environment.  The short and easily digestible course modules cover a variety of topics to provide a basic overview of how to best use Python depending on your use case.  This includes what Python packages are available via CCR's Python software modules, installing additional Python packages using virtual environments, and container usage for packages not conducive to virtual environments. The "Python Pitfalls" module covers many of the pain points previous CCR users have hit when using Python on our systems.  Optional modules in this course include using Python with VSCode, Jupyter, and RStudio, and using Easybuild to install your own Python bundles.  We highly recommend this course to all CCR users that would like to save time and headaches when using Python in their workflows.  If you're an external collaborator or industry cluster user without access to UB Learns, you'll find some of the course content on our [YouTube channel](https://www.youtube.com/@ubccr).

## Python at CCR

Check out this video for an overview of using Python, virtual environments, and Jupyter kernels in CCR's HPC environment:
![type:video](https://www.youtube.com/embed/uS85S-odkRk)

!!! Danger ""
    Before you run any Python code or tools on the cluster, you **MUST** run `module load gcc python`

The way Python is installed and configured at CCR can be a little confusing. When you ssh into a login or compile node, you may find Python already installed. However, this version of python **SHOULD NOT** be used to install or run any of your code. The method CCR uses to load and run software on the cluster depends on Python, so a version will come preinstalled on nodes for compatibility purposes. When you run `module load gcc python`, a new version of Python is loaded which _is_ configured to run programs on the cluster:

```
CCRusername@login:~$ which python
/<version-info>/compat/usr/bin/python 

CCRusername@login:~$ module load gcc python
CCRusername@login:~$ which python
/<version-info>/easybuild/<toolchain-info>/python/<version>/bin/python
```

### Installing Python Packages

The standard tool used to install new Python packages is called pip. However, you cannot just load python and then immediately install new software with pip (as many tutorials will instruct you to do). Pip is not designed to configure software to run in an HPC environment, therefore software installed with pip is not guaranteed to run across different jobs and nodes.

EasyBuild is the preferred and supported way to build new python packages for the cluster. EasyBuild is the only way to guarantee your software is properly configured to run on CCR's computing hardware. For example, if you try to install PyTorch (GPU-enabled packages) via pip, you will not be able to configure PyTorch to detect or run code on GPU resources. Software built with EasyBuild is also easier to maintain through software version updates as all you will need to do is rerun your EasyBuild recipe.  For instructions on creating an Easybuild Python bundle see [here](../software/modules.md#python).

Unfortunately, EasyBuild is not a drop in replacement for pip. It lacks the ability to automatically manage package dependencies and conflicts. If an EasyBuild recipe does not exist for the python package you are trying to install, creating one yourself can be a lengthy, trial and error process. For this reason, things like PyTorch are difficult to build without an existing EasyBuild recipe.  For more information on using Easybuild see our documentation [here](./easybuild.md).  Alternatively, you can submit a request to CCR to build the software for you following [these instructions](../software/building.md#software-build-requests).  

If the EasyBuild path is impossible, you can try to use virtual environments, though we cannot guarantee they will work for every use case. 

### Virtual Environments

Typical python workflows involve creating virtual environments and installing packages into them. There are many reasons why virtual environments are the preferred way to run your python projects. However, using virtual environments on CCR's resources comes with tradeoffs.  

!!! Danger ""
    Do not proceed without running `module load gcc python`

#### Using Virtual Environments

To create a virtual environment run the following commands:

```
module load gcc python

python3 -m venv /projects/academic/[YourGroupName]/venv_name
source /projects/academic/[YourGroupName]/venv_name/bin/activate 
```

where venv_name can be whatever you'd like to call your new virtual environment. We recommend creating this environment in your group's project directory as you have limited space to install packages in your home directory. Reminder: this is just an example; you'll need to set the path name to your group's shared project directory, which may not be in /projects/academic.

#### Installing Packages inside the Virtual Environment

Once you have activated your virtual environment, you will be able to use pip to install new packages. You can also load additional modules, such as scipy-bundle, to avoid reinstalling already available python packages.
```
source /projects/academic/[YourGroupName]/venv_name/bin/activate
(venv_name) pip install new_package
```

Installing Python packages this way will only work for a subset of all available packages. **Any package that depends on many pre-installed libraries, especially C libraries, or requires GPU enabling, will most likely need EasyBuild to compile properly.**

#### Sharing Virtual Environments  

Theoretically, you can share your virtual environments with members of your research group by storing them in your project directory.  In reality, this can be a cause of problems if not setup properly and if not all members of your group are aware of how to properly use them.  If sharing your virtual environment with other users, we highly recommend creating a `pip.conf` file in the virtual environment directory.  Within this you should set the `[site]` target variable and point to the virtual environment's site-packages directory to ensure that all packages are installed in this contained environment.  It would look something like this:  

```
[site]
target = /projects/academic/[YourGroupName]/venv_name/lib/python3.X/site-packages/
```
You must use additional caution with this and ensure that you do not already have a `pip.conf` file in your home directory.   Pip will first look at the global site-packages directory, then any defined for the user in the default location `~/.config/pip/pip.conf`, and then any defined for the virtual environment.  To ensure you have no conflicts with package installations in your virtual environment, make sure you have no packages installed in your home directory under a matching version of python.   

### Jupyter Kernels

Once you have a virtual environment set up properly, you may want to use this environment when running a Jupyter session. To do this, you will need to install the ipykernel package and use it to create an interactive Python kernel:

```
module load gcc python
source /projects/academic/[YourGroupName]/venv_name/bin/activate
(venv_name) pip install ipykernel
(venv_name) python3 -m ipykernel install --user --name kernel_name
```

This will create a new Jupyter kernel called "kernel_name", which you can change.  

Once this is done, you should be able to see your new kernel in the list of kernels within Jupyter (you may have to reload your session before it appears).  If you used additional software modules (i.e., PyTorch) when creating your virtual environment, you will need to load these prior to starting a Jupyter session.  See the "Jupyter Interactive Apps" section [here](../portals/ood.md#jupyter-notebook-apps) for instructions.

## Python for AI and Machine Learning 

Check out this video for an overview of using Python in containers, virtual environments and containers, and containers from NVIDIA:
![type:video](https://www.youtube.com/embed/ILS1uLsZsio)  

Do not just try to run `pip install torch`, it will not go well. To install things like PyTorch or Huggingface Transformers properly, you will need to use [EasyBuild](#installing-new-packages) and not pip. If it is imperative to use the latest versions of these packages and EasyBuild has not worked, you should try using prebuilt containers provided by NVIDIA ([see our documentation here](containerization.md)).

The preferred method for running ML is to use training scripts submitted to the cluster as [batch scripts](../hpc/jobs.md) rather than Jupyter notebooks. When you request a GPU for a Jupyter notebook, this GPU may sit idle for the life of the job depending on how the notebook is being used. Opting to use a training script in a job helps with GPU utilization by automatically freeing GPU resources when training jobs are done.

## Common Issues

Check out this video for a few common Python pitfalls we'd like to help you avoid:
![type:video](https://www.youtube.com/embed/ALlicxP0nZQ)  

- I cannot connect to a Jupyter kernel I created from a virtual environment!
    - You probably used the system python to build the environment. It will look like the first example [here](#python-at-ccr).  You will have to delete the environment and kernel and rebuild both once you have run `module load gcc python`

- I saved my virtual environment to my /projects directory, but my packages are being installed into my home directory and I'm running out of space!  This may be caused by a few things:  
    - You used the system python to build your venv and now pip is saving downloaded packages to `~/.local`. Delete this directory and your current venv and rebuild it after you run `module load gcc python`  
    - You may have a pip configuration file in your home directory telling pip where to install packages.  Look at `~/.config/pip/pip.conf` and edit to point to the location you want your packages installed to.  This can be tricky so we recommend you follow the [pip documentation](https://pip.pypa.io/en/stable/topics/configuration/)

- I'm trying to download a model from huggingface but running out of space.
    - You can set new cache directories when running `from_pretrained()` to download your model. You can also set paths in your job scripts to change your cache directories. An example for the latter method can be found in our huggingface example submission script: `/util/software/examples/huggingface/torch-run-sample.sh`.  This is accessible on the login and cluster compute nodes.
