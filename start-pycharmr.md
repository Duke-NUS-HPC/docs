# Initiate Pycharm on Cluster

I use pycharm for debugging python modules under specific pre-built python environments (environment name is shown as 3.8 @ ubuntu at the right corner). Sometimes I directly submit jobs in the pycharm terminal, which is linked to what node I am current in. I will use PBS in the future.

![img](https://tidal-vibraphone-993.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7543f979-c9a5-44f9-84ba-4c3d7024c1ed%2FUntitled.png?table=block&id=72460185-3a70-40c1-8027-91b60afed41f&spaceId=487f6bbc-aed5-46da-afc4-02bb4aa10be9&width=2000&userId=&cache=v2)

- Forwarding X11 on local terminal from mobaxterm

  1. `ssh-keygen -t rsa`
  2. save as `/home/nuozhang/.ssh/id_rsa_hpc`
  3. enter passward
  4. less `.ssh/id_rsa_hpc.pub` and paste in remote server `.ssh/authorized_keys` file
  5. edit local `.ssh/config` file

  ```bash
  Host dukehpc
  HostName 172.25.138.10
  User e0833634
  ForwardX11 yes
  IdentityFile /home/nuozhang/.ssh/id_rsa_hpc
  ```

  6. in mobaxterm terminal, enter `ssh -X dukehpc` to enter `login-10-03` node

- Open Pycharm on GPU node through submitting PBS job

  1. in mobaxterm terminal, submit a job request on `workq` with `-XI` parameters and resources needed

     `qsub -IX -l select=1:ncpus=1:mem=2G:ngpus=1 -l walltime=60 -q workq`

     `-IX`submitting an interactive job with X forwarding

     `-l`: resource list

     walltime: listed in seconds

     `-q`: specifying queue destination

     [other PBS resources](https://help.nscc.sg/pbspro-quickstartguide/) and [parameter checklist](https://help.nscc.sg/wp-content/uploads/2016/08/PBS_Professional_Quick_Reference.pdf)

  2. job request will let me enter GPU node

  3. to open pycharm, enter `~/pycharm-2021.3.2/bin/pycharm.sh`

