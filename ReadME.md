```markdown
# Introduction to Machine Learning and Artificial Intelligence with High Performance Computing

## Workshop Overview
This workshop aims to equip participants with the skills to train AI models using High Performance Computing (HPC). Through hands-on examples, you will learn how to:
- Set up and manage Jupyter Notebooks from Google Colab on an HPC system.
- Identify and install library dependencies for seamless execution.
- Transition workflows from Jupyter Notebooks to Python scripts and execute them as Slurm jobs.
- Use efficient resource management techniques on HPC.

We will work with two datasets:
- **IRIS Dataset**: Demonstrates Random Forest classification and parameter tuning using multiprocessing.
- **CIFAR-10 Dataset**: Introduces a CNN-based image classification pipeline.

---

## Workshop Steps

### Download the Jupyter Notebooks
Access the provided links for the **Random Forest** and **CNN with CIFAR-10** notebooks in Google Colab, and save the notebooks locally as `.ipynb` files.

---

### Extract Libraries and Versions
Upload the notebook to ChatGPT with the following prompt to extract library dependencies:
```

Please extract the list of libraries imported in the attached Jupyter Notebook. Additionally, provide a Jupyter Notebook cell command to display the version of each imported library along with the Python version in a professional format.

```
Append the generated list to the notebook for future reference. Use an additional prompt to convert the extracted libraries into a pip install format:
```

Provide this in pip install format.

```

> **Note:** For some libraries, such as PyTorch, refer to the [PyTorch installation guide](https://pytorch.org/get-started/locally/) to ensure compatibility with your environment.

---

### Transfer Notebooks to the HPC
Transfer the downloaded `.ipynb` files to your HPC home directory using a secure copy tool (e.g., `scp`):
```bash
scp <notebook_name>.ipynb <username>@<hpc_address>:/home/<username>/
```

---

### Set Up a Conda Environment

- Log into the HPC system:

  ```bash
  ssh <username>@<hpc_address>
  ```
- Request an interactive node:

  ```bash
  salloc -N 1 -n 10 -p <partition_name>
  ```
- Clean up old environments (if needed):

  ```bash
  conda clean --all
  ```
- Load the Miniconda module:

  ```bash
  module load miniconda3
  ```
- Create a new Conda environment:

  ```bash
  conda create --prefix /home/<username>/<environment_name> python=3.10.12
  ```

  OR
  ```bash
  conda create -n <environment_name> python=3.10.12
  ```
- Activate the environment:

  ```bash
  conda activate <environment_name>
  ```
- Install required packages:

  ```bash
  conda install -c conda-forge ipykernel
  conda install notebook
  ```
- Register the environment for JupyterLab:

  ```bash
  python3 -m ipykernel install --user --name <environment_name>
  ```

---

### Access JupyterLab on HPC

Follow the [Iowa State JupyterLab Guide](https://www.hpc.iastate.edu/guides/jupyterlab) to access JupyterLab on the HPC system. Verify that your new Conda environment is listed as an available kernel.

---

### Export Jupyter Notebooks to Python Scripts

- Export directly from JupyterLab:
  - Go to **File > Export Notebook As... > Export Notebook to Executable Script**.
- OR use the command line:
  ```bash
  jupyter nbconvert --to script <notebook_name>.ipynb
  ```

---

### Run Python Scripts Locally

Execute Python scripts directly in your HPC environment:

```bash
python <script_name>.py
```

---

### Submit as a Slurm Job

- Generate a Slurm job script using the [Nova Slurm Script Generator](https://www.hpc.iastate.edu/guides/nova/slurm-script-generator-for-nova).
- Example Slurm script:
  ```bash
  #!/bin/bash
  #SBATCH --job-name=<job_name>
  #SBATCH --output=<output_file>.log
  #SBATCH --ntasks=1
  #SBATCH --cpus-per-task=4
  #SBATCH --time=01:00:00
  #SBATCH --partition=<partition_name>

  module load miniconda3
  conda activate <environment_name>
  python <script_name>.py
  ```
- Submit the job:
  ```bash
  sbatch <script_name>.slurm
  ```

---

## Resources

- **HPC JupyterLab Access:** [Iowa State JupyterLab Guide](https://www.hpc.iastate.edu/guides/jupyterlab)
- **Slurm Script Creation:** [Slurm Script Generator](https://www.hpc.iastate.edu/guides/nova/slurm-script-generator-for-nova)
- **PyTorch Installation:** [PyTorch Installation Guide](https://pytorch.org/get-started/locally/)

---

## Deliverables

Participants should complete the following:

- A Random Forest Slurm job script and execution logs.
- A CIFAR-10 Python script and Slurm submission for training a CNN.

If you encounter any challenges during the workshop, please reach out for assistance. Happy computing!

```

```
