# Start an interactive job with X11 windows on the HPC cluster; PyCharm example

I use pycharm for debugging python modules under specific pre-built python environments. I directly submit jobs in the pycharm terminal and python console, which runs on the
cluster node on which I am running PyCharm.

1. [ssh to the cluster login node from a command shell](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-with-keypairs.md)


1. Once you are on the login node, open an interactive shell with X11 forwarding on a GPU node by submitting a PBS job with `qsub`:

     `qsub -IX -l select=1:ncpus=1:mem=2G:ngpus=1 -l walltime=60 -q workq`

     `-IX`: submitting an interactive job with X forwarding

     `-l`: resource list

     `walltime`: listed in seconds

     `-q`: specify which queue to use

     [PBS quickstart](https://help.nscc.sg/pbspro-quickstartguide/) and [quick reference](https://help.nscc.sg/wp-content/uploads/2016/08/PBS_Professional_Quick_Reference.pdf)

    Then PBS will give you an interactive shell on a GPU node (because of `ngpus=1`. If you do not need a GPU, use `ngpus=0`

1. If you have PyCharm installed in your home directory, then open pycharm: `~/pycharm-2021.3.2/bin/pycharm.sh`
