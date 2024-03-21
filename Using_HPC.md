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

### Step 4: Job Submission
- Example: Executing a "Hello World" Python script.
1. `mkdir scripts`
2. `cd scripts`
3. `mkdir hello_world`
3. `vim hello.py`
4. Go into insert mode by pressing "i".
5. Type `print("Hello, World!")`.
6. Press "esc" to exit insert mode.
7. Type `:wq` to save and exit the file.
8. 

### Step 5: Interactive Node Request
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

### Step 6: Launching Jupyter on your interactive node.