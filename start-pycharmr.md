# Run Pycharm on HPC Cluster

I use pycharm for debugging python modules under specific pre-built python environments (environment name is shown as 3.8 @ ubuntu at the right corner). Sometimes I directly submit jobs in the pycharm terminal, which is linked to what node I am current in.

![img](https://tidal-vibraphone-993.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7543f979-c9a5-44f9-84ba-4c3d7024c1ed%2FUntitled.png?table=block&id=72460185-3a70-40c1-8027-91b60afed41f&spaceId=487f6bbc-aed5-46da-afc4-02bb4aa10be9&width=2000&userId=&cache=v2)

- [Set up X11 forwarding, then ssh to the cluster login node](https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-with-keypairs.md)


- Get an interactive shell with X11 forwarding on a GPU node by submitting a PBS job

  1. Once logged in to the cluster login node, submit a PBS job request on `workq` with `-XI` parameters and resources needed

     `qsub -IX -l select=1:ncpus=1:mem=2G:ngpus=1 -l walltime=60 -q workq`

     `-IX`submitting an interactive job with X forwarding

     `-l`: resource list

     `walltime`: listed in seconds

     `-q`: specify which queue to use

     [PBS quickstart](https://help.nscc.sg/pbspro-quickstartguide/) and [quick reference](https://help.nscc.sg/wp-content/uploads/2016/08/PBS_Professional_Quick_Reference.pdf)

  2. job request will let me us a shell on the GPU node

- Open pycharm: `~/pycharm-2021.3.2/bin/pycharm.sh`
