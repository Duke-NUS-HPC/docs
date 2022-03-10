# Start an interactive job with X11 windows

A lot of Linux / Unix program use X windows. We need a program running
on a cluster node to pop up a window on your local desktop or laptop.

1. [ssh to the cluster login node from a command shell](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-with-keypairs.md)

Make sure you used the `-X` flag in `ssh` and make sure you have
an X windows server running on your local machine.


1. Once you are on the login node, open an interactive shell with X11 forwarding on a GPU node by submitting a PBS job with `qsub`:

     `qsub -IX -l select=1:ncpus=1:mem=2G:ngpus=10 -l walltime=6000 -q workq`

     `-IX`: submitting an interactive job with X forwarding

     `-l`: resource list

     `walltime`: listed in seconds

     `-q`: specify which queue to use, currently only `workq` exists.

     [PBS quickstart](https://help.nscc.sg/pbspro-quickstartguide/) and [quick reference](https://help.nscc.sg/wp-content/uploads/2016/08/PBS_Professional_Quick_Reference.pdf)

    Then PBS will give you an interactive shell on a GPU node (because of `ngpus=1`. If you do not need a GPU, use `ngpus=0`

1. You can test this by opening an `xterm` window; at the command line:

`xterm &`

The xterm window should pop up.
