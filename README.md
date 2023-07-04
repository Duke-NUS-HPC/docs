# Documents for the Duke-NUS Office of Research HPC Cluster
Discord for questions: https://discord.gg/eZntxgUyav

## Queue information

To get a list of avaible queues, at the command line do

`qstat -Q`

To get full information on one queue, at the command line do

`qstat -Qf <queue_name>`

Maximum wallclock time is at `resources_max.walltime`

## Sample batch job submission resource request
If not specified, default resources assigned per job is: 1 cpu, 4gb mem, 5min walltime
```
#!/bin/bash
#PBS -l select=1:ncpus=1:mem=4gb
#PBS -l walltime=00:05:00
#PBS -q workq
#PBS -N jobname
#PBS -o path/my.out
#PBS -e path/my.err

scripts
```

## [ssh to the cluster login node](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-to-hpc.md)

## [Start an interactive PBSpro job with X11 windows](https://github.com/Duke-NUS-HPC/docs/blob/main/start-interactive-shell-with-X11.md)
(PBSpro is the job scheduler)

## [Set up ssh key pairs for loging into the cluster](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-with-keypairs.md)

## [How to install R packges in your personal R library](https://github.com/Duke-NUS-HPC/docs/blob/main/install-R-package-in-personal-library.md)

## [Add customized conda environment to jupyter notebook kernel](https://github.com/Duke-NUS-HPC/docs/blob/main/Add%20customized%20conda%20environment%20to%20jupyter%20notebook%20kernel.md)

## [Install tensorflow-gpu via conda](https://github.com/Duke-NUS-HPC/docs/blob/main/Install%20tensorflow-gpu%20via%20conda.md)

## [Use GPU enabled singularity container in PyCharm and Jupyter Notebook](https://github.com/Duke-NUS-HPC/docs/blob/main/use%20singularity%20container%20in%20PyCharm%20and%20Jupyter%20Notebook.md)
(pre-installed packages including tensorflow-gpu=2.8 and torch=1.11 are provided)
