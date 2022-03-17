# Use singularity container in PyCharm and Jupyter Notebook
Singularity container is a pre-built immutable distributable environment.<br>

Once entered the container, the system recognized two home paths: one for pre-installed packages (can be accessed through `cd /`), and the other will be the default home directory for file sharing.<br>

More information for [Singularity](https://github.com/sylabs/singularity)

Current available container contains packages listed below.
```
tensorflow-gpu==2.8.0
tensorboard==2.8.0
torch==1.11.0
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
nltk==3.7
numpy==1.21.5
pandas==1.4.1
pattern3==3.0.0
scikit-learn==1.0.2
scipy==1.8.0
scanpy==1.8.2
seaborn==0.11.2
umap-learn==0.5.2
transformers==4.17.0
```
## Why should use this container
- need most up-to-date version of most packages but don't want to solve pip dependencies
- do some natural languages processing trainings
- maximize the utilization of NVIDIA A100 40GB GPU (which cannot be accelerated with tensorflow-gpu==2.2.0)
- explore singularity
- running batch jobs

## Why should not use this container
- your scripts can run within conda environment without dependency issues
- your project does not rely heavily with GPU (run fast with conda distributed tensorflow-gpu already)<br>
Related resources for how to [set up conda environment for jupyter notebook](https://github.com/Duke-NUS-HPC/docs/blob/main/Add%20customized%20conda%20environment%20to%20jupyter%20notebook%20kernel.md)
and [how to install tensorflow-gpu using conda](https://github.com/Duke-NUS-HPC/docs/blob/main/Install%20tensorflow-gpu.md)


***Replace following `$image` with `/data/rozen/home/e0833634/py38_cuda11-4-4_nodriver_cudnn8-2-4_tf-gpu2-8-0_ubuntu18-04.sif` <br>***
## Optional: Install new packages
1. Login hpc via dashboard or ssh
2. `module load singularity` 
4. Enter singularity container

    `singularity exec $image bash` 
3. New packages can be installed via `python3.8 -m pip install xxxx` in the singularity shell. Packages will be installed in the host home directory within folder `.local/bin/`.<br>
   However, these newly installed packages cannot be distributed to others together with the container.
5. Please **don't install conda**<br>

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

## Use singularity container in jupyter lab/jupyter notebook (all notebook listed below can be switched to lab)
1. Login hpc via dashboard or ssh
2. `module load singularity` 
3. Set up passwords for forwarded jupyter notebook window
    
    `singularity exec $image jupyter notebook --generate-config`
    
    `singularity exec $image jupyter notebook password`
    
4. `qsub` an interactive job with `-X` forwarding, allocate necessary resources. [Instructions](https://github.com/Duke-NUS-HPC/docs/blob/main/start-interactive-shell-with-X11.md)
5. Enter singularity container

    `singularity exec $image bash` 
7. Add singularity kernel to jupyter python environment, <env_name> can be anything customized. (this is a one-time setting)

    `ipython kernel install --name <env_name> --user`
7. Exit the container by typing `exit`
8. Start to open jupyter notebook
    
    `singularity exec $image jupyter notebook --no-browser --port=8889 --ip=0.0.0.0`
    
    `port` number can be changed to any other number except 8888 if other people are using the same port. example: 8999
    
    can add `--nv` flag to monitor GPU usage
    
6. On local computer, open a **new Mobaxterm tab** with:
    
    `ssh -L 8888:targethost:8889 nusstu\\xxxx@172.25.138.10` 
    
7. On local computer, open a browser from Chrome or FireFox and browse to `http://localhost:8888`. Enter password.
8. Switch to singularity kernel within jupyter notebook.
9. Open a new python script and test with:
    ```python
    import tensorflow as tf
    print(tf.__version__)
    ```
    
    should return `2.8.0`
    
