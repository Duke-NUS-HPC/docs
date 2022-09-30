# Use singularity container in PyCharm and Jupyter Notebook
Singularity container is a pre-built immutable distributable environment.<br>

Once entered the container, the system recognized two home paths: one for pre-installed packages (can be accessed through `cd /`), and the other will be the default home directory for file sharing.<br>

More information for [Singularity](https://github.com/sylabs/singularity)

Current available containers (python=3.8) contains packages listed below.
- ubuntu distribution:
```
tensorflow-gpu==2.8.0
tensorboard==2.8.0
torch==1.11.0+cu113
bert-tensorflow==1.0.4
biopython==1.79
flair==0.10
h5py==3.6.0
hmmlearn==0.2.7
huggingface-hub==0.4.0
igraph==0.9.9
keras==2.8.0
jupyter
jupyterlab
louvain==0.7.1
matplotlib==3.5.1
nltk==3.7.0
numpy==1.21.5
pandas==1.4.1
pattern3==2.6
scikit-learn==1.0.2
scipy==1.8.0
scanpy==1.8.2
seaborn==0.11.2
umap-learn==0.5.2
transformers==4.17.0
accelerate==0.6.1
dm-sonnet==2.0.0
kipoiseq==0.5.2
tensorflow-hub==0.12.0
anndata==0.8.0
scikit-multilearn
```
They are built with different environments.
- ***py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu18-04.sif***
     ```
    cudatoolkit=11.4.2
    cudnn=8.2.4.15
    tensorRT=8.2.3
    ubuntu 18.04
    python 3.8
    ```
- ***py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu20-04.sif***
    ```
    cudatoolkit=11.4.2
    cudnn=8.3.3.40
    tensorRT=8.2.3
    ubuntu 20.04
    python 3.8
    ```
    cudnn 8.3.x is optimized for transformer-based models.

- centos7 distribution
```
tensorflow-gpu==2.9.1
tensorboard==2.9.1
torch==1.11.0+cu113
bert-tensorflow==1.0.4
biopython==1.79
flair==0.11.3
h5py==3.6.0
hmmlearn==0.2.7
huggingface-hub==0.4.0
igraph==0.9.11
keras==2.9.0
jupyter
jupyterlab
louvain==0.7.1
matplotlib==3.5.1
nltk==3.7.0
numpy==1.22.4
pandas==1.4.2
pattern3==2.6
scikit-learn==1.1.1
scipy==1.8.1
scanpy==1.9.1
seaborn==0.11.2
transformers==4.20.0
tqdm==4.64.0
umap-learn==0.5.2
accelerate==0.10.0
dm-sonnet==2.0.0
kipoiseq==0.5.2
tensorflow-hub==0.12.0
anndata==0.8.0
scikit-multilearn==0.2.0
biotite==0.33.0
fuzzywuzzy==0.18.0
```
- ***py38_cuda11-6-2_nodriver_cudnn8-4-0_torch-1-11_tf-2-9-1_centos7.sif*** (18G)
     ```
     cudatoolkit=11.6.2
     cudnn=8.4.0.27
     tensorRT=8.4.1.5
     CentOS 7
     python 3.8
     ```
     ***need special trick to use this container, contact `enol` through discord if you need***
## Why should use this container
- need most up-to-date version of most packages but don't want to solve pip dependencies
- do some natural languages processing trainings
- maximize the utilization of NVIDIA A100 40GB GPU (which cannot be accelerated with tensorflow-gpu==2.2.0)
- explore singularity
- run batch jobs

## Why may not need this container
- your scripts can run within conda environment without dependency issues
- your project does not rely heavily with GPU (run fast with conda distributed tensorflow-gpu already)<br>
Related resources for how to [set up conda environment for jupyter notebook](https://github.com/Duke-NUS-HPC/docs/blob/main/Add%20customized%20conda%20environment%20to%20jupyter%20notebook%20kernel.md)
and [how to install tensorflow-gpu using conda](https://github.com/Duke-NUS-HPC/docs/blob/main/Install%20tensorflow-gpu.md)


***Replace following `$image` with the container needed, example: `/data/rozen/home/e0833634/py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu20-04.sif` (15G)<br>***

Distributed Version: https://mynbox.nus.edu.sg/u/tirFLFuqxQGkKsUJ/0ef6dd75-1755-4a6d-8b0f-836d9a0960ce?l, and here is the [source code](https://github.com/ynuozhang/BuildContainer/blob/master/tf2v10.def) if you are interested.
## Optional: Install new packages
1. Login hpc via dashboard or ssh
2. `module load singularity` 
4. Enter singularity container

    `singularity exec $image bash` 
3. New packages can be installed via `python3.8 -m pip install xxxx` in the singularity shell. Packages will be installed in the host home directory within folder `.local/bin/` or `.local/lib/python3.8/site-packages`.<br>
   However, these newly installed packages cannot be distributed to others together with the container.
5. Please **don't install conda**<br>
6. All python commands in bash or in batch jobs should start with **python3.8** instead of **python**.
7. For those who need `torch_geometric.nn` [info](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html), you can install within the container via `python3.8 -m pip install torch-scatter torch-sparse torch-cluster torch-spline-conv torch-geometric -f https://data.pyg.org/whl/torch-1.11.0+cu113.html`

## Use singularity container in jupyter lab/jupyter notebook (all notebook listed below can be switched to lab)
1. Login hpc via dashboard or ssh
2. `module load singularity` 
3. Set up passwords for forwarded jupyter notebook window (this is a one-time setting)
    
    `singularity exec $image jupyter notebook --generate-config`
    
    `singularity exec $image jupyter notebook password`
    
5. Enter singularity container

    `singularity exec $image bash` 
7. Add singularity kernel to jupyter python environment, <env_name> can be anything customized. (this is a one-time setting)

    `ipython kernel install --name <env_name> --user`
7. Exit the container by typing `exit`
9. Two ways to open jupyter notebook
- First way<br>
     start an interactive job with `qsub -I`. Caution: interactive jobs are only applicable for `workq` and `gpu` queue.
    
   `singularity exec $image jupyter notebook --no-browser --port=8889 --ip=0.0.0.0`
    
    `port` number can be changed to any other number except 8888 if other people are using the same port. example: 8889
    
    can add `--nv` flag to monitor GPU usage<br/>
    
- Second way: use alternative job.sh (can submit to any queue)
```
#!/bin/sh
#PBS -N yourjobname
#PBS -q workq
#PBS -l walltime=6000
#PBS -l select=1:ncpus=9:mem=10gb:ngpus=0
#PBS -koe

HOME_LOC=/data/rozen/home/e0833634/whatever
cd $PBS_O_WORKDIR
image="/data/rozen/home/e0833634/py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu20-04.sif"
module load singularity
printf "activate singularity successful\n" >>$PBS_O_WORKDIR/logs/tensorflow_cmd.log

singularity exec $image jupyter notebook --no-browser --port=8889 --ip=0.0.0.0 << EOF > stdout.$PBS_JOBID 2> stderr.$PBS_JOBID

exit 0
```
In the end, submit an batch job with x-forwarding: `qsub -V job.sh`
    
8. On local computer, open a **new Mobaxterm tab** with:
    
    `ssh -L 8888:host:8889 nusstu\\xxxx@172.25.138.10` 
    
    for `host` please check which node is assigned for the job unless specified with `vnode`
    
9. On your local computer, open a browser from Chrome or FireFox and browse to `http://localhost:8888`. Enter password.
10. Switch to singularity kernel within jupyter notebook.
11. Open a new python script and test with:
    ```python
    import tensorflow as tf
    print(tf.__version__)
    ```
    
    should return `2.8.0`
    
12. Test wether using GPU

```
import torch
torch.cuda.is_available()
>>> True

torch.cuda.current_device()
>>> 0

torch.cuda.device(0)
>>> <torch.cuda.device at 0x7efce0b03be0>

torch.cuda.device_count()
>>> 1

torch.cuda.get_device_name(0)
>>> 'NVIDIA A100-PCIE-40GB'
```

## Use singularity container in PyCharm
1. Login hpc with ssh -X
2. `qsub` an interactive job with `-X` forwarding, allocate necessary resources. [Instructions](https://github.com/Duke-NUS-HPC/docs/blob/main/start-interactive-shell-with-X11.md)
3. `module load singularity` 
4. Enter singularity container
    
    `singularity exec $image bash` 
    
    can add `--nv` flag to monitor GPU usage
    
5. Open PyCharm
    
    `~/pycharm-2021.3.2/bin/pycharm.sh`
    
6. Select `Add Interpreter` on the right bottom corner
7. Select  `system interpreter` or create `virtualenv environment` with the system interpreter. 
  If the path is written as `/usr/bin/python3.8`, the correct interpreter is selected.
9. Check if singularity container is used:

    ```python
    import tensorflow as tf
    print(tf.__version__)
    ```
    
    should return `2.8.0`


## Batch job submission
1. For testing
```
#!/bin/sh
#PBS -N your_job_namee
#PBS -q gpu
#PBS -l walltime=6000
#PBS -l select=1:ncpus=10:mem=100gb:ngpus=1
#PBS -koe

HOME_LOC=/data/pi_name/home/your_id
touch $PBS_O_WORKDIR/logs/test_load_container.log
echo $PBS_O_WORKDIR >>$PBS_O_WORKDIR/logs/tensorflow_cmd.log
cd $PBS_O_WORKDIR
image="/data/rozen/home/e0833634/py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu18-04.sif"
module load singularity
printf "activate singularity successful\n" >>$PBS_O_WORKDIR/logs/test_load_container.log

singularity exec $image bash << EOF > stdout.$PBS_JOBID 2> stderr.$PBS_JOBID

python3.8 -c "import pandas as pd; print(pd.__version__)" > $PBS_O_WORKDIR/logs/test.log 2>&1

printf "finish testing container\n" >>$PBS_O_WORKDIR/logs/test_load_container.log

EOF
```
2. Batch job script example `job.sh`
```
#!/bin/sh
#PBS -N your_job_namee
#PBS -q gpu
#PBS -l walltime=6000
#PBS -l select=1:ncpus=10:mem=100gb:ngpus=1
#PBS -koe

HOME_LOC=/data/pi_name/home/your_id
cd $PBS_O_WORKDIR
image="/data/rozen/home/e0833634/py38_cuda11-4-2_nodriver_cudnn8-2-4_torch-1-11_tf-2-8-0_ubuntu18-04.sif"
module load singularity

singularity exec $image bash << EOF > stdout.$PBS_JOBID 2> stderr.$PBS_JOBID

python3.8 yourscript.py > $PBS_O_WORKDIR/your_logs/your_log.log 2>&1

EOF

```
3. submit job with `qsub job.sh`

***For questions, please email yzhang@u.duke.nus.edu***
