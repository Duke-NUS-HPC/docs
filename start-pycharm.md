# Run PyCharm on HPC Cluster

I use pycharm for debugging python modules under specific pre-built python environments. I can directly submit jobs in the pycharm terminal and python console, which is linked to what node I am current in.

- [Set up X11 forwarding, then ssh to the cluster login node](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-with-keypairs.md)


- Get an interactive shell with X11 forwarding on a GPU node by submitting a PBS job

  1. Once logged in to the cluster login node, submit a PBS job request on `workq` with `-IX` parameters and resources needed

     `qsub -IX -l select=1:ncpus=1:mem=2G:ngpus=1 -l walltime=60 -q workq`

     `-IX`: submitting an interactive job with X forwarding

     `-l`: resource list

     `walltime`: listed in seconds

     `-q`: specify which queue to use

     [PBS quickstart](https://help.nscc.sg/pbspro-quickstartguide/) and [quick reference](https://help.nscc.sg/wp-content/uploads/2016/08/PBS_Professional_Quick_Reference.pdf)

  2. job request will let me us a shell on the GPU node

- Open pycharm: `~/pycharm-2021.3.2/bin/pycharm.sh`
