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

