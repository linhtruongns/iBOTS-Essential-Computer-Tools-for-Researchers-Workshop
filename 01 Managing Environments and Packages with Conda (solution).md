# The Conda Package Manager and Environment Management

In this unit, we will learn how to use Conda to manage packages and environments. Conda allows you to create isolated environments, manage dependencies, and install packages seamlessly across platforms. This unit includes instructions for installing Conda via Miniforge and covers core Conda commands for creating, managing, and sharing environments. 

## Installation

### Visual Studio Code (VSCode)
[Download Link](https://code.visualstudio.com/download)

### Miniforge

Miniforge provides a streamlined approach to Conda installation with a minimal environment and access to the conda-forge community repository, which is popular for its extensive collection of data science and scientific computing packages. Miniforge is available for all major operating systems, making it a flexible choice for cross-platform development.



### Installation Instructions

 **If you do not already have Conda installed** please follow these instructions to install Miniforge. 

#### macOS & Linux

1. Download the Miniforge installer for your platform from [Miniforge releases](https://github.com/conda-forge/miniforge/releases).
2. Open a terminal and navigate to the download location.
3. Run the installer:
   ```bash
   bash Miniforge3-Linux-x86_64.sh  # or the macOS equivalent
   ```
4. Follow the prompts to complete installation.

#### Windows

1. Download the Miniforge installer for Windows from [Miniforge releases](https://github.com/conda-forge/miniforge/releases).
2. Open the installer and follow the prompts.
3. Once installed, open a new terminal or Command Prompt.

After installation, verify that Conda is installed by running:
```bash
conda --version
```





## Section 1: Creating and Managing Environments

One of the key advantages of Conda is its ability to create isolated environments, which are essentially self-contained workspaces with their own packages and dependencies. This allows you to experiment, develop, and analyze data without worrying about conflicts between different package versions, which can often disrupt workflows. This is especially helpful for reproducible research: by keeping dependencies organized, you ensure that your projects are replicable across systems.

This section covers the basics of creating, inspecting, activating, and deactivating Conda environments.


| Command                         | Description                                      |
|---------------------------------|--------------------------------------------------|
| `conda create -n env_name`      | Create a new environment named `env_name`        |
| `conda create -p dir_name`      | Create a new environment in the specified directory `dir_name`        |
| `conda env list`                | List all existing Conda environments             |
| `conda activate env_name`       | Activate the environment `env_name`              |
| `conda deactivate`              | Deactivate the current Conda environment         |
| `conda info --envs`             | Show paths and basic info about all environments |



 **Exercises**

1. Creating an environment by name
   1. Create a new empty Conda environment named `test_env`.
      ```bash
      conda create -n test_env
      ``` 
   2. List all environments to verify that `test_env` was created.
      ```bash
      conda info --envs
      ``` 
   3. Activate `test_env` and confirm activation.
      ```bash
      conda activate test_env
      ``` 
   4. Deactivate the environment.
      ```bash
      conda deactivate
      ``` 

2. Creating an environment at a specific path
   1. Create a new empty Conda environment in the directory `test_env2`.
      ```bash
      conda create -p test_env2
      ``` 
   2. List all environments to verify that `test_env2` was created.
      ```bash
      conda info --envs
      ``` 
   3. In the File Explorer, verify that `test_env2` folder exists.
   4. Activate `test_env2` and confirm activation.
      ```bash
      conda activate test_env2
      ``` 
   5. Deactivate the environment.
      ```bash
      conda deactivate
      ``` 
---



## Section 2: Installing Packages in Environments

Managing packages within Conda environments allows you to install libraries and dependencies specific to each project. This helps avoid the challenges of "dependency hell" where incompatible package versions interfere with each other. For researchers, Conda's ability to install non-Python packages (like r-base or system libraries) provides flexibility and power, especially for complex data workflows involving multiple languages.

Other tools, such as pip, are primarily designed for Python packages, while Conda can handle cross-language dependencies. This makes it especially useful for mixed-language research workflows involving Python and R.

`conda-forge` contains a wealth of scientific packages for download.  Here is their list: https://conda-forge.org/packages/


| Command                                | Description                                      |
|----------------------------------------|--------------------------------------------------|
| `conda install package_name`           | Install `package_name` into the active environment |
| `conda install -c conda-forge package_name`           | Install `package_name` from the `conda-forge` channel into the active environment. |
| `conda install -n env_name package_name` | Install `package_name` into `env_name`            |
| `conda list`                           | List all installed packages in the active environment |


**Exercises**

1. Creating an environment and installing Python.
   1. Create and activate new environment named `py_env`.
      ```bash
      conda create -n py_env
      conda activate py_env
      ``` 
   2. Install `python=3.9` in `py_env`.
      ```bash
      conda install python=3.9
      ``` 
   3. List all installed packages and verify that you see Python with version 3.9.xx installed.
      ```bash
      conda list
      ``` 
   4. (Alternative) Type `python --version` to verify Python was installed. 
      ```bash
      python --version
      ```  
   6. Deactivate the environment
      ```bash
      conda deactivate
      ``` 
   

2. Install `r-base` in `r_env` environment and verify the installation.
      ```bash
      conda create -n r_env
      conda activate r_env
      conda install r-base
      conda list
      conda deactivate
      ``` 
   


3. (**Optional**) Install `python=2.7` in `py_env2` environment and verify the installation.
      ```bash
      conda create -n py_env2
      conda activate py_env2
      conda install python=2.7
      conda deactivate
      ``` 
   

---



## Section 3: Exporting and Importing Environments

A powerful feature of Conda is the ability to share environment configurations with collaborators. By exporting an environment to a file, you can create a "snapshot" of all installed packages and dependencies. This is essential for reproducibility in research, as others can recreate the exact environment to ensure consistency in analyses and results. Using Conda environment files can save time and reduce errors, especially when working on collaborative projects.  

Removing unused environments and packages helps keep your Conda installation clean and organized, conserving storage space and reducing potential conflicts. Conda makes it easy to remove entire environments or individual packages, allowing you to focus only on the active dependencies you need for your current work.

This section shows how to save an environment configuration to a file and recreate it later.  

| Command                                     | Description                                              |
|---------------------------------------------|----------------------------------------------------------|
| `conda env export > environment.yml`        | Save active environment configuration to `environment.yml` |
| `conda remove -n env_name --all`     | Remove the environment `env_name` completely |
| `conda remove package_name`          | Remove `package_name` from the active environment |
| `conda env create -f environment.yml`       | Create an environment from the file `environment.yml`    |
| `conda env update --file environment.yml`   | Update the environment from `environment.yml`            |


**Exercises**

1. Export the `test_env` environment to a file named `test_env.yml`.
      ```bash
      conda activate test_env
      conda env export > test_env.yml
      conda deactivate
      ``` 
2. Deactivate and remove `test_env` using `conda remove -n test_env --all`. List all the environments to verify that it has been removed.
      ```bash
      conda remove -n test_env --all
      conda info --envs
      ``` 
3. Recreate `test_env` from the `test_env.yml` file.
      ```bash
      conda env create -f test_env.yml
      conda info --envs
      ``` 
4. Verify the recreation by activating `test_env` and listing the installed packages.
      ```bash
      conda activate test_env
      conda list
      ``` 
5. Remove all the environments you don't want to keep after this session.

