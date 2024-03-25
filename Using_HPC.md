# High-Performance Computing (TSCC) Usage Guide

## Introduction

Welcome to the Triton Shared Computing Cluster (TSCC) Usage Guide! This manual is crafted to assist students in effectively harnessing the power of TSCC for computational needs.

## Getting Started

### Accessing the Cluster

#### Step 1: Account Activation
- Confirm the activation of your account by consulting with the TAs for your username.
- Your password aligns with your active directory credentials.
- Duo authentication is a prerequisite.

#### Step 2: Cluster Connection via SSH
- **Windows Users:** Utilize MobaXTerm for SSH connectivity.
  - **Hostname:** login.tscc.sdsc.edu
  - **Username:** Please refer to the TAs for this information.

- **Command Line Users (Mac/Linux):**
  - Initiate a connection with: `ssh yourUsername@login.tscc.sdsc.edu`

### Step 3: Anaconda Installation
#### Download
- Retrieve the Anaconda installation script using: 
  `curl -O https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh`

#### Installation
- Execute the script: `bash Anaconda3-2024.02-1-Linux-x86_64.sh`
- Follow the on-screen prompts to install anaconda into an "anaconda3" folder in your local directory.
- Do you want to automatically initialize > yes
- type "conda" to verify installation

### Step 4: Creating an Anaconda Environment
- **Command:** `conda create -n python_3_8 python=3.8`
  - **Explanation:** This command creates a new environment named "python_3_8" with Python 3.8.
- **Command:** `conda activate python_3_8`
  - **Explanation:** This command activates the environment "python_3_8".
- **Command:** `conda deactivate`
  - **Explanation:** This command deactivates the current environment.

### Step 5: Job Submission
- Example: Executing a "Hello World" Python script.
1. `mkdir scripts`
2. `cd scripts`
3. `mkdir hello_world`
4. Let's practice transferring files onto TSCC.
  Download the files `hello.py` and `run_hello.sb` from the `scripts/hello_world` folder in the repository.

  **Windows users:**
  - Go to your MobaXTerm.

  **Mac users:**
  - Go to your terminal.

  We will use the command `scp` to transfer the files to TSCC.

  Challenge: Change directories to your downloads folder using the command line.

  To copy the hello.py file to TSCC, use the following command:
  `scp hello.py user@login.tscc.sdsc.edu:/tscc/nfs/home/yourtsccusername/scripts/hello_world`

  For instance, my command is `scp drives/c/Users/amonell/Downloads/hello.py etrain104@login.tscc.sdsc.edu:/tscc/nfs/home/etrain104/scripts/hello_world`

  Challenge: Copy the run_hello.sb file to TSCC using the same method.

5. Go back to TSCC and navigate to the `scripts/hello_world` directory.
6. Submit the job using the command: `sbatch run_hello.sb`
7. Type `ls` to see the folders in this directory. (Hint) there is a file that was not there before.
8. Check the contents of the file using the `head` command followed by the name of this new file.

### Step 6: Interactive Node Request
- Command: `srun --partition=hotel --pty --nodes=1 --ntasks-per-node=1 -t 00:30:00 --qos=hotel --wait=0 --export=ALL /bin/bash`
  - **Explanation of Parameters:**
    - `--partition=hotel`: Assigns the debug partition.
    - `--pty`: Engages a pseudo-terminal.
    - `--nodes=1`: Designates one node.
    - `--ntasks-per-node=1`: Sets the task count per node to 1.
    - `-t 00:30:00`: Limits the time to 30 minutes.
    - `-A xyz123`: Defines the account.
    - `--wait=0`: Eliminates waiting time.
    - `--export=ALL`: Exports all environmental variables.
    - `--qos=hotel`: Sets the Quality of Service.
    - `/bin/bash`: Initiates a Bash shell post-allocation.

### Step 7: Launching Jupyter on an Interactive Node to run Python code

On your TSCC account in your base directory:

`module load shared`

`module load galyleo`

TSCC utilizes a bash script “Galyleo” to serve Jupyter notebooks more securely.

`module load python3essential`

`galyleo launch --account htl179 --qos hotel --cpus 1 --memory 8 --time-limit 00:30:00 --partition hotel --conda-env python3essential-1.99.0 --env-modules slurm/tscc/23.02.7 --conda-init /tscc/projects/ps-yeolab4/software/miniconda_tscc2/etc/profile.d/conda.sh`

We are opening a Jupyter notebook in a conda environment with a bunch of important Python packages preinstalled. If you want to run Jupyter in your own environment, you would need to change the paths associated with 'conda' in the galyleo command. 

Create a new notebook called hello_notebook in your hello_world scripts folder from inside jupyter. 

Specify that you are using a Python3 kernel.

Type `print('Hello, World')` in the first cell and run the cell.

Save your work.
     
### Creating a conda environment to run R code.

1. **Create a New Conda Environment for R (Optional):**
   - If you want a separate environment for R, create a new one using: `conda create -n r_env`
   - Activate the new environment: `conda activate r_env`

2. **Install R Base:**
   - To install the R base package, run: `conda install -c r r-base`
   - This command installs the R language in your Conda environment.

3. **Verify R Installation:**
   - After installation, you can verify the installation by running: `R --version`
   - This command should show the R version installed, confirming that the installation is successful.

4. **Installing R Packages:**
   - To install an R package, you can start R in the terminal by just typing: `R`
   - Once in the R console, install packages using: `install.packages('package_name')`

5. **Exiting R:**
   - To exit the R console, type: `quit()`
   - Save workspace image? [y/n/c]: Choose 'n' if you do not want to save or 'y' to save.

6. **Deactivate Conda Environment:**
   - Once you are done, you can deactivate your Conda environment by typing: `conda deactivate`

### Step 8: Running R code in a Jupyter notebook

#### Install the R Kernel:
- Inside your Conda environment with r-base installed, install the IRkernel package by running `conda install -c r r-irkernel`.
- This will allow Jupyter to run R code in addition to Python.

#### Install Jupyter:
- `pip install jupyter`.

#### Hook R up to Jupyter.
- Run R with `R`.
- Link R up to Jupyter with `IRkernel::installspec()`
- Quit R with `q()`.

#### Launch Jupyter in your r environment.
- `galyleo launch --account htl179 --qos hotel --cpus 1 --memory 8 --time-limit 00:30:00 --partition hotel --conda-env r_env --env-modules slurm/tscc/23.02.7 --conda-init /tscc/nfs/home/etrain104/anaconda/etc/profile.d/conda.sh`

#### Create a New R Notebook:
- Create a new notebook and name it `hello_world_r.ipynb`.
- Set the kernel to an R kernel.

#### Running R Code:
- In the first cell of the new R notebook, try entering
  `x <- 'Hello, World \n print(x)`
- Run the cell to execute the R code and observe the output.

#### Install R Packages:
- If you need additional R packages, you can install them directly in the notebook.
- Use the command `install.packages('package_name')` in a cell to install a package.
- Load the package using `library(package_name)`.

#### Save Your Work:
- Regularly save your notebook to prevent losing your work.
- Jupyter notebooks autosave, but it's a good habit to manually save as well.

